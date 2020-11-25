## TypeScript小记

学习中，笔记较乱，待整理



参考来源：

[TypeScript入门教程](https://ts.xcatliu.com/)

[史上最全的TypeScript入门教程](https://blog.csdn.net/qq_40566547/article/details/100055437)



### 安装编译

**全局安装ts**

```shell
npm install typescript -g
```

**编译成js 再执行js**

```shell
tsc demo.js
node demo.js
```

**ts-node 直接执行**

```shell
npm install -g ts-node
ts-node  demo.ts
```

**生成```tsconfig.json```文件，这个文件是用来将ts编译成js代码的文件**

```shell
tsc --init
```



### 基本数据类型

js基本数据类型：boolean, number, string, undefined, null, symbol, BigInt



> [BigInt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt) 是一种内置对象，它提供了一种方法来表示大于 2**53 - 1 的整数。这原本是 Javascript中可以用 Number 表示的最大数字。BigInt 可以表示任意大的整数。
>
> 可以用在一个整数字面量后面加 n 的方式定义一个 BigInt ，如：10n，或者调用函数BigInt()。
>
> ```js
> const alsoHuge = BigInt(9007199254740991);
> // ↪ 9007199254740991n
> ```
>
> 它在某些方面类似于 Number ，但是也有几个关键的不同点：不能用于 Math 对象中的方法；不能和任何 Number 实例混合运算，两者必须转换成同一种类型。在两种类型来回转换时要小心，因为 BigInt 变量在转换成 Number 变量时可能会丢失精度。





### 对象类型

{}, Class, function, []

#### 数组类型

两种定义方式

```ts
let num: number[] = [1, 2]
let str: Array<string> = ['1', '2'];
// 推荐使用第一种字面量的形式
```

#### 函数类型

 ```ts
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
 ```

注意不要混淆了 TypeScript 中的 => 和 ES6 中的 =>。

在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。



##### 可选参数

```ts
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```

注意：可选参数必须接在必需参数后面



##### 返回值注解类型

```ts
function getTotal(firstNumber: number, secondNumber): number {
	return firstNumber + secondNumber;
}
```



### 空值void

`void`表示没有任何返回值的函数：

```ts
function sayHello(): void {
	console.log('hello');
}
```



### 任意值

任意值（Any）用来表示允许赋值为任意类型。 

如果是一个普通类型，在赋值过程中改变类型是不被允许的 

但如果是 any 类型，则允许被赋值为任意类型。

**变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型** 

**any 在数组中的应用**

一个比较常见的做法是，用 any 表示数组中允许出现任意类型：

```ts
let list: any[] = ['xcatliu', 25, { website: 'http://xcatliu.com' }];
```



### never：永远不可能执行完成

```ts
function errorEmitter(): never {
	throw new Error();
	console.log(123);
}
```



### 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种。 

```ts
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```



### 接口



#### 可选类型

```ts
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```



#### 任意属性

```ts
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};
```



**注意：一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集** 

```ts
interface Person {
    name: string;
    age?: number;
    [propName: string]: string;
}

let tom: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};

// index.ts(3,5): error TS2411: Property 'age' of type 'number' is not assignable to string index type 'string'.
// index.ts(7,5): error TS2322: Type '{ [x: string]: string | number; name: string; age: number; gender: string; }' is not assignable to type 'Person'.
//   Index signatures are incompatible.
//     Type 'string | number' is not assignable to type 'string'.
//       Type 'number' is not assignable to type 'string'.
```

上例中，任意属性的值允许是 string，但是可选属性 age 的值却是 number，number 不是 string 的子属性，所以报错了。



#### 只读属性

```ts
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    id: 89757,
    name: 'Tom',
    gender: 'male'
};

tom.id = 9527;

// index.ts(14,5): error TS2540: Cannot assign to 'id' because it is a constant or a read-only property.
```















### 类型注解

我们告诉ts，变量是什么类型

```ts
let count:number;
count = 123;
```



### 类型推断

ts会自动的去尝试分析变量的类型



如果ts能够自动分析变量类型，我们就什么也不需要做了

如果ts无法分析变量类型的话，我们就需要使用类型注解

```let countInference = 123;```

这个时候需要加类型注解

```ts
function getTotal(firstNumber: number, secondNumber) {
	return firstNumber + secondNumber;
}
const total = getTotal(1, 2);
```



**如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 `any` 类型而完全不被类型检查** 



**当字符串转对象时（JSON.parse），需要声明类型**

```ts
interface Person {
    name: 'string'
}
const rawData = '{"name": "dell"}';
const newData = JSON.parse(rawData);			// newData类型为any
const newData: Person = JSON.parse(rawData);  	// newData类型为Person
```





### 解构赋值类型注解

```ts
function add(
	{ first, second }: { first: nuber, second:number}
): number {
	return first + second;
}

const total = add({ first: 1, second: 2});
```



### 类型断言

