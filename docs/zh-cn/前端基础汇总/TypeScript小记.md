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



```ts
const arr: (number | string)[] = [1, '2', 3];
const stringArr: string[] = ['a', 'b', 'c'];
const undefinedArr: undefined[] = [undefined];
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



#### 函数重载

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



### 元组

其实元组类型是数组类型的子集。在数组类型中，我们的数组元素只能用定义好的一种类型的变量，但是在元组中，我们可以定义多个类型的变量的数组，但是这也限定了元组的数据量，不能多也不能少



用于csv或excel导出数据形式时

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

```ts
enum Color {
    blue = 3,
    red = 1
}
1234
```

  默认情况下，每一个元组key的value都是number，而且是从0开始计，而且都可以被指定新的value。
  但是我们可以认为改变这个value，value的改变规则如下。

1. 将第一个改变为number类型时，第二个以及以后的key他的value紧接着第一个key的value+1
2. 将第一个改变为string类型时，第二个必须指定为number类型或一个string类型，若指定为string类型，第三个和第二个的情况一样，依此类推。
3. 类似其他情况与第二种情况一样，若某一个改变为string类型其下一个的value必须指定为number或string，依此类推。

```ts
enum Color {
    blue = '5',
    red = 1,
    yellow = 'str'
}
12345
```

  获取元组类型的变量某一个值就只需要像对象一样取得就可以比如，但是比对象更灵活，你不仅可以取得他的key，而且可以取得他的value，不必像对象那样进行Object.keys操作

```ts
let yellowValue: Color = Color.yellow
let yellowKey: string = Color['str']
console.log(yellow)
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



#### 类实现接口

```ts
//	接口在定义的时候，不能初始化属性以及方法，属性不能进行初始化，方法不能实现方法体。
interface Ali{
  pay():void
  payName:string
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



#### 继承接口

```ts
// 接口继承
  interface Shape{
    color: string;
  }
  interface Square extends Shape{
    sideLength: number;
  }

//例子8 继承接口
    let square = <Square>{};
    square.color = 'blue';
    square.sideLength = 10;
```



一个接口可以继承多个接口，创建出多个接口的合成接口

```ts
 //例子9一个接口继承多个接口，创造出多个接口的合成接口
  interface PenStroke{
    penWidth: number;
  }
  interface ExpameSquare extends Shape, PenStroke{
    sideLength: number
  }
 //例子9 一个接口继承多个接口
    let example2 = <ExpameSquare>{};
    example2.color = 'red';
    example2.sideLength = 20;
```





#### 接口继承类

TypeScript接口可以继承类，规则如下:
（1）.继承类的成员，但不包括其实现。

```ts
// 类继承类的方式
// 接口继承类
class Control{
  private state: string;
  color: string
}

// 类只能单继承，为什么呢，是因为如果多个父类中有同一个方法，那么在子类中调用，是不知道调用哪一个的，因此只能单继承
class Button extends Control{
  name: string
  say(){
    console.log('输出color',this.color)
    // console.log('输出state',this.state)
  }
}
//接口继承类
//接口继承类
interface TableControl extends Control{
  click(): void
}

// 实现接口，需要实现接口中所定义的所有方法以及属性，由于state是private，所以不能在此实现会报错，解决方式如下 
class Image implements TableControl{
  click(){
  }
  color: string

}
// 解决方式如下
 因为 state是私有成员，所以只能够是Control的子类们才能实现。
因为子类继承父类，相当于拥有父类的所有属性以及方法，因此不用额外定义，这个是兼容的，但是如果是实现接口，接口中需要重新实现所有的成员以及方法，这对于private属性是不兼容的。所以这一点注意一下就可以了
class SelectDown extends Control implements TableControl{
  click(){
    console.log(this.color)
  }
```



#### 多态

```ts
//多态的例子
interface Animal{
  play():void
  name: string
}
class dog implements Animal{
  constructor(name: string){
    this.name = name
  }
  play(){
    console.log('输出name',this.name)
  }
  name: string
}
class cat implements Animal{
  constructor(name: string){
    this.name = name
  }
  play(){
    console.log('输出name', this.name)
  }
  name: string
}

 getAnimalPlay(animal: Animal){
    animal.play()
  }

let catt = new cat('一只小猫')
    let dogg = new dog('一个可爱的狗狗')
    this.getAnimalPlay(catt)
    this.getAnimalPlay(dogg)

```

总结

- 接口与接口之间可以直接进行多继承
- 类实现接口可以进行多实现，每个接口用 , 隔开即可





### type alias 类型别名

```ts
type User = {
    name: string;
    age: number;
};
```



#### 类型别名和接口的区别

类型别名可以代表基础类型  接口不可以

```ts
interface Person {
    name: string;
}
type Person = string;
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

语法：

值 as 类型   或  <类型>值





 

















