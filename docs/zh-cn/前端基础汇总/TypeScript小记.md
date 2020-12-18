## TypeScript小记

学习中，笔记较乱，待整理

------

2020.12.04  创建文档，更新TypeScript基础

2020.12.18  理了一遍基础知识点排列顺序

------

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
tsc demo.ts
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



```ts
// 1.布尔值
let isDone: boolean = false;
let createdByBoolean: boolean = Boolean(1);
// 注意使用构造函数 Boolean 创造的对象不是布尔值
// 事实上 new Boolean() 返回的是一个 Boolean 对象：
let createdByNewBoolean: boolean = new Boolean(1);

// 2.数值
let decLiteral: number = 6;

// 3.字符串
let myName: string = 'Tom';

// 4.undefined
let n: null = null;

// 5.null
let u: undefined = undefined;
// undefined可以赋值给任意类型
let num: number = undefined;
```



### void：空值

`void`表示没有任何返回值的函数：

```ts
function sayHello(): void {
	console.log('hello');
}
```



### any：任意值

任意值（Any）用来表示允许赋值为任意类型。 

如果是一个普通类型，在赋值过程中改变类型是不被允许的 

但如果是 any 类型，则允许被赋值为任意类型。

**变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型** 

切记：不要滥用any类型



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

**访问联合类型的属性或方法**

当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，**只能访问此联合类型的所有类型里共有的属性或方法**：

```ts
// 访问不是共有的属性
function getLength(something: string | number): number {
    return something.length;
}

// index.ts(2,22): error TS2339: Property 'length' does not exist on type 'string | number'.
//   Property 'length' does not exist on type 'number'.

// 访问共有属性
function getString(something: string | number): string {
    return something.toString();
}
```



联合类型的变量在被赋值的时候，会根据类型推论的规则推断出一个类型：

```ts
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
console.log(myFavoriteNumber.length); // 5
myFavoriteNumber = 7;
console.log(myFavoriteNumber.length); // 编译时报错

// index.ts(5,30): error TS2339: Property 'length' does not exist on type 'number'.
```

上例中，第二行的 `myFavoriteNumber` 被推断成了 `string`，访问它的 `length` 属性不会报错。

而第四行的 `myFavoriteNumber` 被推断成了 `number`，访问它的 `length` 属性时就报错了。





### 类型注解

我们告诉ts，变量是什么类型

```ts
let count: number;
count = 123;
```

解构赋值类型注解

```ts
function add(
	{ first, second }: { first: number, second: number}
): number {
	return first + second;
}

const total = add({ first: 1, second: 2});
```



### 类型推断

ts会自动的去尝试分析变量的类型

如果ts能够自动分析变量类型，我们就什么也不需要做了

```ts
let countInference = 123;
```

如果ts无法分析变量类型的话，我们就需要使用类型注解

```ts
function getTotal(firstNumber: number, secondNumber) {
	return firstNumber + secondNumber;
}
const total = getTotal(1, 2);
```



**如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 `any` 类型而完全不被类型检查** 

```ts
let num;
num = 123;
num = '123';
```



**当字符串转对象时（JSON.parse），需要声明类型**

```ts
interface Person {
    name: 'string'
}
const rawData = '{"name": "dell"}';
const newData = JSON.parse(rawData);			// newData类型为any
const newData: Person = JSON.parse(rawData);  	// newData类型为Person
```



### 数组类型

```ts
// 推荐使用第一种字面量的形式
let num: number[] = [1, 2]
// 数值泛型
let str: Array<string> = ['1', '2'];
// 接口
interface NumberArray {
    [index: number]: number;
}
let fibonacci: NumberArray = [1, 1, 2, 3, 5];

```



```ts
const arr: (number | string)[] = [1, '2', 3];
const stringArr: string[] = ['a', 'b', 'c'];
const undefinedArr: undefined[] = [undefined];
```



**any 在数组中的应用**

一个比较常见的做法是，用 any 表示数组中允许出现任意类型：

```ts
let list: any[] = ['xcatliu', 25, { website: 'http://xcatliu.com' }];
```



### 函数类型

```ts
// 函数声明（Function Declaration）
function sum(x, y) {
    return x + y;
}

// 函数表达式（Function Expression）
let mySum = function (x, y) {
    return x + y;
};
```



添加类型

 ```ts
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
 ```

注意不要混淆了 TypeScript 中的 => 和 ES6 中的 =>。

在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。



用接口定义

```ts
interface SearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
}
```



#### 可选参数

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



#### 剩余参数

```ts
function push(array: any[], ...items: any[]) {
    items.forEach(function(item) {
        array.push(item);
    });
}

let a = [];
push(a, 1, 2, 3);
```



#### 函数重载

（个人比较疑惑这个函数重载的意义是什么）

```ts
function css(el: string, value: Object): any;

function css(el: string, value: string): any;

function css(el: string, value: any): any {
    if (typeof value === 'string') {
        console.log('传入的时string')
    } else if ((value as object)){
        console.log('传入的是对象')
    }
}
```

前几次都是函数定义，最后一次是函数实现。在编辑器的代码提示中，可以正确的看到前两个提示。

注意，TypeScript 会优先从最前面的函数定义开始匹配，所以多个函数定义如果有包含关系，需要优先把精确的定义写在前面。



### 接口

在 TypeScript 中，我们使用接口（Interfaces）来定义对象的类型。 

#### 什么是接口

在面向对象语言中，接口（Interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implement）。

TypeScript 中的接口是一个非常灵活的概念，除了可用于**对类的一部分行为进行抽象**以外，也常用于对「对象的形状（Shape）」进行描述。

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

// 任意属性的值允许是 string，但是可选属性 age 的值却是 number，number 不是 string 的子属性，所以会报错
let tom: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};
```



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
// 会报错
tom.id = 9527;
```



#### 类实现接口

```ts
//	接口在定义的时候，不能初始化属性以及方法，属性不能进行初始化，方法不能实现方法体。
interface Ali{
  pay(): void
  payName: string
}
interface Tence{
  payNumber(): void
  name: string
}

//	类实现接口之后，必须声明接口中定义的属性以及方法。
class mySelf implements Ali, Tence{
  pay(){

  } 
  payName: string
  payNumber(){

  }
  name: string
}
```



#### 接口继承接口

```ts
interface Shape{
    color: string;
}
interface Square extends Shape{
    sideLength: number;
}

let square = <Square>{};
square.color = 'blue';
square.sideLength = 10;
```



### 类

基本概念可以看这里 :point_right: [ES6 中类的用法](https://csmsimona.github.io/myDocs/#/zh-cn/前端基础汇总/JavaScript小记?id=_13%e3%80%81class)



### 类型断言

语法：

值 as 类型   或  <类型>值



#### 将一个联合类型断言为其中一个类型

用于解决 **访问联合类型里不是共有的属性或方法会报错** 的问题

```ts
interface Cat {
    name: string;
    run(): void;
}
interface Fish {
    name: string;
    swim(): void;
}

function isFish(animal: Cat | Fish) {
    if (typeof (animal as Fish).swim === 'function') {
        return true;
    }
    return false;
}
```



#### 将一个父类断言为更加具体的子类

```ts
class ApiError extends Error {
    code: number = 0;
}
class HttpError extends Error {
    statusCode: number = 200;
}

function isApiError(error: Error) {
    if (typeof (error as ApiError).code === 'number') {
        return true;
    }
    return false;
}
```



#### 将任何一个类型断言为any

不能滥用！

`window` 上添加一个属性 `foo`，但 TypeScript 编译时会报错，提示我们 `window` 上不存在 `foo` 属性。

此时我们可以使用 `as any` 临时将 `window` 断言为 `any` 类型：

```ts
window.foo = 1 				// 报错
(window as any).foo = 1;
```



#### 将 any 断言为一个具体的类型

一般用于优化历史遗留代码， 通过类型断言及时的把 `any` 断言为精确的类型，亡羊补牢，使我们的代码向着高可维护性的目标发展 

```ts
// 原来返回值是any
function getCacheData(key: string): any {
    return (window as any).cache[key];
}

interface Cat {
    name: string;
    run(): void;
}

// 断言成Cat类型
const tom = getCacheData('tom') as Cat;
tom.run();
```



也可以用 [泛型](#_泛型) 来解决这个问题

```ts
function getCacheData<T>(key: string): T {
    return (window as any).cache[key];
}

interface Cat {
    name: string;
    run(): void;
}

const tom = getCacheData<Cat>('tom');
tom.run();
```



### type alias 类型别名

常用于联合类型

```ts
type User = {
    name: string;
    age: number;
};


type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
    if (typeof n === 'string') {
        return n;
    } else {
        return n();
    }
}
```



还可以用  type 定义一个字符串字面量类型  

```ts
type EventNames = 'click' | 'scroll' | 'mousemove';
function handleEvent(ele: Element, event: EventNames) {
    // do something
}

handleEvent(document.getElementById('hello'), 'scroll');  // 没问题
handleEvent(document.getElementById('world'), 'dblclick'); // 报错，event 不能为 'dblclick'

// index.ts(7,47): error TS2345: Argument of type '"dblclick"' is not assignable to parameter of type 'EventNames'.
```



**类型别名和接口的区别**

类型别名可以代表基础类型  接口不可以

```ts
interface Person {
    name: string;
}
type Person = string;
```



### 元组 （Tuple） 

其实元组类型是数组类型的子集。 数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象。 



```ts
let tom: [string, number];
tom = ['Tom', 25];
tom.push('male');		// 元组数据量不能多也不能少
tom.push(true);			// 不能添加元组中定义类型以外的类型数据
```



**用于csv或excel导出数据形式时**

```ts
// 元组 tuple
const teacherInfo: [string, string, number] = ['Dell', 'male', 18];
// csv
const teacherList: [string, string, number][] = [
    ['dell', 'male', 19],
    ['sun', 'female', 26],
    ['jeny', 'female', 38]
]
```



### 枚举类型

枚举类型是一种特殊的类型，主要用于状态码的取值

[直接看这里吧](https://ts.xcatliu.com/advanced/enum.html)

枚举成员会被**赋值为从 0 开始递增的数字**，同时也会对枚举值到枚举名进行**反向映射**

不仅可以取得他的key，而且可以取得他的value，不必像对象那样进行Object.keys操作

```ts
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};

console.log(Days["Sun"] === 0); // true
console.log(Days["Mon"] === 1); // true
console.log(Days["Tue"] === 2); // true
console.log(Days["Sat"] === 6); // true

console.log(Days[0] === "Sun"); // true
console.log(Days[1] === "Mon"); // true
console.log(Days[2] === "Tue"); // true
console.log(Days[6] === "Sat"); // true
```

事实上，上面的例子会被编译为：

```js
var Days;
(function (Days) {
    Days[Days["Sun"] = 0] = "Sun";
    Days[Days["Mon"] = 1] = "Mon";
    Days[Days["Tue"] = 2] = "Tue";
    Days[Days["Wed"] = 3] = "Wed";
    Days[Days["Thu"] = 4] = "Thu";
    Days[Days["Fri"] = 5] = "Fri";
    Days[Days["Sat"] = 6] = "Sat";
})(Days || (Days = {}));
```





### 泛型



### 模块化



### 命名空间



### 装饰器



### 迭代器、生成器



### 声明文件

























