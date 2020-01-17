## JavaScript小记（持续更新）

学习js遇到的疑问和js基础都记录在这里，持续更新中。

------

2019.12.11   更新this、继承，补充了一些方法，删除对象，创建对象的方法

2020.1.14     增加ES6部分新特性，转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

------

### 1、正则表达式

/b+/g    至少出现一次b（1~n次）

/b*/g    可以不出现b，也可以出现一次或多次（0~n次）

/b{n,m}/g   最少出现n次b，最多出现m次b（n~m次）

/colou?r/g  可以匹配color或colour，？表示前面的字符最多只出现一次（0次或1次）

#### 元字符

| 元字符 |                             作用                             |
| :----: | :----------------------------------------------------------: |
|   .    |                 匹配任意字符除了换行符和回车                 |
|   []   |   匹配方括号内的任意字符。比如[0-9]就可以用来匹配任意数字    |
|   ^    | ^9，这样使用代表匹配以9开头。[ ^9 ]，这样使用代表不匹配方括号内除了9的字符 |
| {n,m}  |                        匹配n~m位字符                         |
| (abc)  |                   只匹配和abc相同的字符串                    |
|   \|   |                      匹配\|前后任意字符                      |
|   \    |                             转义                             |
|   *    |                        匹配0~n位字符                         |
|   +    |                        匹配1~n位字符                         |
|   ?    |                    ？之前字符可选，0或1位                    |

#### 修饰语

| 修饰语 |    作用    |
| :----: | :--------: |
|   i    | 忽略大小写 |
|   g    |  全局搜索  |
|   m    |    多行    |

#### 字符简写

| 简写 |         作用         |
| :--: | :------------------: |
|  \w  | 匹配字母数字或下划线 |
|  \W  |      和上面相反      |
|  \s  |   匹配任意的空白符   |
|  \S  |      和上面相反      |
|  \d  |       匹配数字       |
|  \D  |      和上面相反      |
|  \b  | 匹配单词的开始和结束 |
|  \B  |      和上面相反      |

#### 检索规则

test()：检索字符串中的指定值。返回值是true或false

exec()：检索字符串中的指定值。返回值是被找到的值。如果没有发现匹配，则返回null

compile()：即可以改变检索规则，也可以添加或删除第二个参数

#### 创建方式

1、字面量语法：/pattern/ attributes

2、创建RegExp对象的语法：new RegExp(pattern, attributes)

attributes：g:全局匹配	i:大小写匹配	m:多行匹配

例一：删除一个字符串中所有的英文

`doc = doc.replace(/[A-Za-z]+/g, '');`

例二：验证一个字符串是否是电话号码

`/^[1][358][0-9]{9}$/`

### 2、replace(/\s/g,"")

"/ /"这个是固定写法，"\s"是转移符号用以匹配任何空白字符，包括空格、制表符、换页符等等，"g"表示全局匹配将替换所有匹配的子串，如果不加"g"当匹配到第一个后就结束了。

这个例子的意思就是**将原字符串中的所有空白字符替换成""**，比如"abc d efg "字样的字符串使用这个函数后将变成"abcdefg"

一般用来把字符串中所有的空格去掉

### 3、代码回收规则

1.全局变量不会被回收

2.局部变量会被回收，也就是函数一旦运行完以后，函数内部的东西都会被销毁

3.只要被另外一个作用域所引用就不会被回收

### 4、数据类型

另外可以看看这篇文章：[js中的值类型和引用类型的区别](https://www.cnblogs.com/leiting/p/8081413.html)

基本数据类型（值类型）：undefined、null、string、number、boolean、symbol

（占用空间固定，保存在栈中）

复杂数据类型：object

引用类型：array、function、object 

（占用空间不固定，保存在堆中。存储在栈中的是指向堆中的数组或者对象的地址）

### 5、堆区和栈区

栈区的特点：操作性能高，速度快，存储量小

​	所以：一般存储操作频率较高，生命周期较短，占用空间较小的数据。（基本数据类型）

堆区的特点：操作性能低（相对于栈区），速度慢，存储量大

​	所以：一般存储操作频率较低，生命周期较长，占用空间较大的数据。（复杂数据类型）

​	堆通常是一个可以被看做一棵完全二叉树的数组对象。  逻辑上：完全二叉树 存储上：数组（顺序存储） 

### 6、JS中数据类型的判断（ typeof，instanceof，constructor，Object.prototype.toString.call() ）

- **typeof**

  对一个值使用typeof操作符可能返回： 

  undefined、string、number、boolean、symbol、object（对象或null）、function

  ```js
  console.log(typeof 2);               // number
  console.log(typeof true);            // boolean
  console.log(typeof 'str');           // string
  console.log(typeof []);              // object  []数组的数据类型在 typeof 中被解释为object
  console.log(typeof function(){});    // function
  console.log(typeof {});              // object
  console.log(typeof undefined);       // undefined
  console.log(typeof null);            // object    null 的数据类型被 typeof 解释为 object
  ```

  typeof 对于基本类型，除了null都可以显示正确的类型；对于对象，除了函数都会显示object。

  对于null来说，虽然它是基本类型，但是会显示object，这是一个存在了很久的bug。

  因为在js的最初版本中，使用的是32位系统，为了性能考虑使用低位存储了变量的类型信息，000开头代表是对象，然而null表示为全零，所以将它错误的判断为object。虽然现在的内部类型 判断代码已经改变了，但是对于这个bug却是一直流传下来。

- **instanceof**

  只有引用数据类型（Array，Function，Object）被精准判断，其他（数值Number，布尔值Boolean，字符串String）字面值不能被instanceof精准判断。

  instanceOf可以正确的判断对象的类型，因为**内部机制是通过判断对象的原型链中是不是能找得类型的prototype**。

  ```js
  console.log(2 instanceof Number);                    // false
  console.log(true instanceof Boolean);                // false 
  console.log('str' instanceof String);                // false  
  console.log([] instanceof Array);                    // true
  console.log(function(){} instanceof Function);       // true
  console.log({} instanceof Object);                   // true    
  // console.log(undefined instanceof Undefined);
  // console.log(null instanceof Null);
  ```

  

  ```js
  function Person(name, age) {
      this.name = name;
      this.age = age;
  }
  function Dog(name, age) {
      this.name = name;
      this.age = age;
  }
  var p = new Person('zs', 18);
  var d = new Dog('小花', 8);
  
  console.log(p instanceof Person);       // true
  console.log(d instanceof Person);       // true
  console.log(p instanceof Object);		// false
  ```

  

- **constructor**

  ```js
  console.log((2).constructor === Number);  				// true
  console.log((true).constructor === Boolean);  			// true
  console.log(('str').constructor === String); 			// true
  console.log(([]).constructor === Array);  				// true
  console.log((function() {}).constructor === Function);  // true
  console.log(({}).constructor === Object);               // true
  ```

  用costructor来判断类型看起来是完美的，然而，如果我创建一个对象，更改它的原型，这种方式也变得不可靠了。

  ```js
  function Person(name, age) {
      this.name = name;
      this.age = age;
  }
  
  var p = new Person('csm', 21);
  
  console.log(p.constructor.name); 	// Person
  
  // 改变原型
  Person.prototype = {
      name: 'zs',
      age: 18
  };
  
  var p1 = new Person('csm', 21);
  
  console.log(p1.constructor.name); 	// Object
  ```

  因此，当要修改对象的proptotype时，一定要设置constructor指向其构造函数

  ```js
  function Person(name, age) {
      this.name = name;
      this.age = age;
  }
  Person.prototype = {
  	constructor: Person,
      name: 'zs',
      age: 18
  };
  var p = new Person('csm', 21);
  console.log(p.constructor.name); 	// Person
  ```

- **object.prototype.toString.call()**

  ```js
  console.log(Object.prototype.toString.call(2));    			// [object Number]
  console.log(Object.prototype.toString.call(true));			// [object Boolean]
  console.log(Object.prototype.toString.call('str'));			// [object String]
  console.log(Object.prototype.toString.call([]));			// [object Array]
  console.log(Object.prototype.toString.call(function(){}));	// [object Function]
  console.log(Object.prototype.toString.call({}));			// [object Object]
  console.log(Object.prototype.toString.call(undefined));		// [object Undefined]
  console.log(Object.prototype.toString.call(null));			// [object Null]
  ```


​        使用 Object 对象的原型方法 toString ，使用 call 进行狸猫换太子，借用Object的 toString  方法结果精准的显示我们需要的数据类型。就算我们改变对象的原型，依然会显示正确的数据类型。

### 7、JavaScript继承的六种方式

另外可以看看这两篇文章：

https://www.cnblogs.com/humin/p/4556820.html

https://www.cnblogs.com/Grace-zyy/p/8206002.html

继承就是让子类拥有父类的资源

#### 1.继承的方式

​    01-原型链继承

​    02-借用构造函数继承

​    03-组合继承

​    04-原型式继承

​    05-寄生式继承

​    06-寄生式组合继承

#### 2.继承的意义

​    减少代码冗余

​    方便统一操作

​    弊端

​      耦合性比较强

#### 3.原型链

1. 每个函数都能构建出一个对象, 这个对象内部有个属性指向着这个函数的原型对象

2. 原型对象本质也是一个对象,也是由另外一个构造函数构造出来, 也指向那个构造函数的原型对象以上，形成一个链式的结构，就称为是原型链

3. 以上，形成一个链式的结构，就称为是原型链

   ```js
   var arr = [1, 2, 3];
   
   console.log(arr.constructor.name); 								// Array
   
   console.log(arr.__proto__.constructor.name); 					// Array
   
   console.log(Array.__proto__.constructor.name);					// Function
   
   console.log(Function.__proto__.constructor.name);				// Function
   
   console.log(Function.prototype.__proto__.constructor.name);		// Object
   
   console.log(Object.prototype.__proto__);						// null
   console.log(Object.__proto__.constructor.name);					// Function
   
   console.log(Array.prototype.__proto__.constructor.name);		// Object
   ```

   数组的完整原型链图

https://www.processon.com/diagraming/5d808df6e4b0c5c942c450b1

![](..\picture\数组的完整原型链图.png)

由图可得Function构造函数处于原型链顶端，所有对象的原型对象都由Object构造函数产生

#### 4.继承方法

```js
	// 父类    
	function Person() {
       this.name = 'cc';
       this.pets = ['aa', 'bb'];
    }

    Person.prototype.run = function () {
        console.log('跑');
    };
```

​    **01-原型链继承**

核心：将父类的实例作为子类的原型 

```js
    // 子类        
    function Student() {
        this.num = '111';
    }
	// 让新实例的原型等于父类的实例
    Student.prototype = new Person();

    var stu = new Student();
    console.log(stu.num); // 111
    stu.run(); // 跑

	// 问题：类型问题
	console.log(stu.constructor.name); //Person  对象类型改变
```

优化：修复constructor指针

```js
    // 子类        
    function Student() {
       this.num = '111';
    }

    Student.prototype = new Person();
    // 修复constructor指针即可
    Student.prototype.constructor = Student;

    var stu = new Student();
    console.log(stu.num);   // 111
    stu.run(); 				// 跑
    console.log(stu.pets);  // ["aa", "bb"]
    console.log(stu.constructor.name);  // Student

	// 问题：继承过来的实例属性, 如果是引用类型, 会被多个子类的实例共享
	var stu1 = new Student();
    stu.pets.push('dd');
    console.log(stu.pets);		// ["aa", "bb", "dd"]
    console.log(stu1.pets);		// ["aa", "bb", "dd"]
```

​    **02-借用构造函数继承**

 核心：在子类型构造函数的内部调用父类构造函数，通过使用call()和apply()方法可以在新创建的对象上执行构造函数。

```js
    // 子类        
    function Student() {
       Person.call(this);
       this.num = '111';
    }
	var stu = new Student();
    console.log(stu.name);   // 111

	// 问题：没用到原型，只能继承父类的实例属性和方法，不能继承原型属性/方法
    stu.run(); 				// 报错：stu.run is not a function
```

​    **03-组合继承**

核心： 将原型链和借用构造函数的技术组合在一块，从而发挥两者之长的一种继承模式。(常用)

```js
    // 子类        
    function Student() {
       Person.call(this);
       this.num = '111';
    }

    Student.prototype = new Person();
    Student.prototype.constructor = Student;

    var stu = new Student();
    var stu1 = new Student();
    stu.pets.push('小花');
    console.log(stu.pets); 		// ["aa", "bb", "小花"]
    console.log(stu1.pets); 	// ["aa", "bb"]

	// 问题：调用了两次父类构造函数（耗内存）
```

​    **04-原型式继承**

核心：借助原型,然后基于已有的对象, 创建出新对象；同时不需要创建自定义类型

用一个函数包装一个对象，然后返回这个函数的调用，这个函数就变成了一个可以随意增添属性的实例或对象。object.create()就是这个原理。

```js
// 原型式继承
function content(obj) {
    function Temp() {}
    Temp.prototype = obj;
    return new Temp();
}
var p = new Person();
var stu1 = content(p);
console.log(stu1.name);
console.log(stu1.age);
```

​    **05-寄生式继承**

核心：在原型式基础上增强这个对象。所谓增加, 就是指, 再次给这个对象增加一些属性或者方法

```js
    // 子类        
    function Student() {
       this.num = '111';
    }

    function Temp() {}
    Temp.prototype = new Person();
    Student.prototype = new Temp();
    Temp.constructor = Student;

    var stu = new Student();
    console.log(stu);
```

​    **06-寄生式组合继承**

核心：通过借用函数来继承属性，通过原型链的混成形式来继承方法。（常用）

```js
    // 子类
	function Student(num, name, pets) {
        Person.call(this, name, pets);
        this.num = num;
    }

    function Temp() {}
    Temp.prototype = new Person();
    Student.prototype = new Temp();
    Temp.constructor = Student;

	var stu = new Student('001', '张三', ['小花']);
    var stu1 = new Student('002', '李四', ['小茂']);
    console.log(stu);
    console.log(stu1);
```

### 8、作用域

它是指对某一变量和方法具有访问权限的代码空间，分为全局作用域和块级作用域。

全局作用域：最外层函数定义的变量拥有全局作用域，即对任何内部函数来说，都是可以访问的。

块级作用域：存在于函数内部或块中（字符{和}之间的区域）

### 9、Ajax

Ajax 即“**A**synchronous **J**avascript **A**nd **X**ML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。

**Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。**

通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

  Ajax技术核心就是XMLHttpRequest对象。

（1）设置请求参数（请求方式，请求页面的相对路径，是否异步）

（2）设置回调函数，一个处理服务器响应的函数，使用 onreadystatechange ，类似函数指针

（3）获取异步对象的readyState 属性：该属性存有服务器响应的状态信息。每当 readyState 改变时，onreadystatechange 函数就会被执行。

（4）判断响应报文的状态，若为200说明服务器正常运行并返回响应数据。

（5）读取响应数据，可以通过 responseText 属性来取回由服务器返回的数据。

```js
var xhr = new XMLHttpRequest();    			// 创建Ajax对象
xhr.open('get', 'aabb.php', true);			// xhr发送请求
xhr.send(null);
xhr.onreadystatechange = function() { 		// xhr获取响应
    if(xhr.readyState == 4) {
        if(xhr.status == 200) {
            console.log(xhr.responseText);
        }
    }
}
 /* ajax返回的状态:
     0：（未初始化）请求还没有建立（open执行前） 
     1：（载入）请求建立了还没发送（执行了open） 
     2：（载入完成）请求正式发送,send()方法执行完成，已经接收到全部响应内容（执行了send） 
     3：（交互）请求已受理，有部分数据可以用，但还没有处理完成,正在解析响应内容
     4：（完成）响应内容解析完成，可以在客户端调用了 
*/ 
```

### 10、Ajax,jQuery ajax,axios和fetch的区别

#### Ajax：

​       ajax，最早出现的发送后端请求技术，隶属于原始js中，核心使用XMLHttpRequest对象，多个请求之间如果有先后关系的话，就会出现回调地狱。

#### Jquery Ajax：

是jQuery框架中的发送后端请求技术，由于jQuery是基于原始的基础上做的封装，所以，jquery Ajax自然也是对原始ajax的封装

```js
$.ajax({
   type: 'POST',
   url: url,
   data: data,
   dataType: dataType,
   success: function () {},
   error: function () {}
});
```

​      优缺点：

- 本身是针对MVC的编程,不符合现在前端MVVM的浪潮
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
- JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）

#### Fetch：

​	fetch号称是AJAX的替代品，是在ES6出现的，使用了ES6中的promise对象。Fetch是基于promise设计的。Fetch的代码结构比起ajax简单多了，参数有点像jQuery ajax。

​	但是，一定记住fetch不是ajax的进一步封装，而是原生js。Fetch函数就是原生js，没有使用XMLHttpRequest对象。

```js
try {
  let response = await fetch(url);
  let data = response.json();
  console.log(data);
} catch(e) {
  console.log("Oops, error", e);
}
```



```jsx
fetch(url).then(response => response.json())
  .then(data => console.log(data))
  .catch(e => console.log("Oops, error", e))
```

- 更酷的一点
  你可以通过Request构造器函数创建一个新的请求对象，你还可以基于原有的对象创建一个新的对象。 新的请求和旧的并没有什么不同，但你可以通过稍微调整配置对象，将其用于不同的场景。例如：

```jsx
var req = new Request(URL, {method: 'GET', cache: 'reload'});
fetch(req).then(function(response) {
  return response.json();
}).then(function(json) {
  insertPhotos(json);
});
```

##### fetch和ajax 的主要区别

1、fetch()返回的promise将不会拒绝http的错误状态，即使响应是一个HTTP 404或者500
2、在默认情况下 fetch不会接受或者发送cookies

##### fetch的配置

Promise fetch(String url [, Object options]);
Promise fetch(Request req [, Object options]);

##### fetch封装

```js
export default async(url = '', data = {}, type = 'GET', method = 'fetch') => {
    type = type.toUpperCase();
    url = baseUrl + url;

    if (type == 'GET') {
        let dataStr = ''; //数据拼接字符串
        Object.keys(data).forEach(key => {
            dataStr += key + '=' + data[key] + '&';
        })

        if (dataStr !== '') {
            dataStr = dataStr.substr(0, dataStr.lastIndexOf('&'));
            url = url + '?' + dataStr;
        }
    }

    if (window.fetch && method == 'fetch') {
        let requestConfig = {
            credentials: 'include',//为了在当前域名内自动发送 cookie ， 必须提供这个选项
            method: type,
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
            },
            mode: "cors",//请求的模式
            cache: "force-cache"
        }

        if (type == 'POST') {
            Object.defineProperty(requestConfig, 'body', {
                value: JSON.stringify(data)
            })
        }
        
        try {
            const response = await fetch(url, requestConfig);
            const responseJson = await response.json();
            return responseJson
        } catch (error) {
            throw new Error(error)
        }
    } else {
        return new Promise((resolve, reject) => {
            let requestObj;
            if (window.XMLHttpRequest) {
                requestObj = new XMLHttpRequest();
            } else {
                requestObj = new ActiveXObject;
            }

            let sendData = '';
            if (type == 'POST') {
                sendData = JSON.stringify(data);
            }

            requestObj.open(type, url, true);
            requestObj.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            requestObj.send(sendData);

            requestObj.onreadystatechange = () => {
                if (requestObj.readyState == 4) {
                    if (requestObj.status == 200) {
                        let obj = requestObj.response
                        if (typeof obj !== 'object') {
                            obj = JSON.parse(obj);
                        }
                        resolve(obj)
                    } else {
                        reject(requestObj)
                    }
                }
            }
        })
    }
}
```

#### Axios：

​	 axios不是原生JS的，需要进行安装，它不但可以在客户端使用，而且可以在nodejs端使用。Axios也可以在请求和响应阶段进行拦截。同样也是基于promise对象的。

https://blog.csdn.net/Roselane_Begger/article/details/88936818

```js
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});

```

优缺点：

- 从 node.js 创建 http 请求
- 支持 Promise API
- 客户端支持防止CSRF
- **提供了一些并发请求的接口**（重要，方便了很多的操作）

### 10、Map和ForEach的区别

- `forEach()`: 数组中的每个元素执行一次回调函数
- `map()`: 返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组

**示例**

下方提供了一个数组，如果我们想将其中的每一个元素翻倍，我们可以使用`map`和`forEach`来达到目的。

```js
let arr = [1, 2, 3, 4, 5];
```

**ForEach**

注意，`forEach`是不会返回有意义的值的。
我们在回调函数中直接修改`arr`的值。

```js
arr.forEach((num, index) => {
    return arr[index] = num * 2;
});
```

**Map**

```js
let doubled = arr.map(num => {
    return num * 2;
});
```

### 11、indexOf与search的区别

- indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置，如果没有找到返回-1
  - 该方法将从头到尾地检索字符串stringObject，看它是否含有子串searchvalue。开始检索的位置在字符串的fromindex处。如果没有fromindex参数则从字符串的开头检索。如果找到一个searchvalue，则返回searchvalue的第一次出现的位置。stringObjec中的字符串位置是从0开始的。
  - indexOf()方法对大小写敏感。

- search方法用于检索字符串中指定的子字符串，检索与**正则表达式**相匹配的子字符串。如果没有找到，返回-1。
  - search() 方法不执行全局匹配，它将忽略标志 g。它同时忽略 regexp 的 lastIndex 属性，并且总是从字符串的开始进行检索，这意味着它总是返回 stringObject 的第一个匹配的位置。
  - search() 方法对大小写敏感。

**indexOf与search的区别**

search()的参数必须是正则表达式,而indexOf()的参数只是普通的字符串。indexOf()是比search()更加底层的方法。

如果只是对一个具体字符串来检索，那么使用indexOf()的系统资源消耗更小，效率更高；如果查找具有某些特征的字符串（例如查找以a开头，后面是数字的字符串），那么indexOf()就无能为力，必须要使用正则表达式和search()方法了。

大多是时候用indexOf()不是为了真的想知道子字符串的位置，而是想知道长字符串中有没有包含这个子字符串。r如果返回索引为-1，那么说明没有，反之则有。

### 12、String对象中slice()、substring()、substr()的用法与区别

- **slice() 方法**可提取字符串的某个部分，并以新的字符串返回被提取的部分。
  - 语法：`stringObject.slice(start,end)`
  - 返回一个新的字符串。包括字符串 stringObject 从 start 开始（包括 start）到 end 结束（不包括 end）为止的所有字符。
  - 如果是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推。

- **substring() 方法**用于提取字符串中介于两个指定下标之间的字符。
  - 语法：`stringObject.substring(start,stop)`
  - 一个新的字符串，该字符串值包含 stringObject 的一个子字符串，其内容是从 start 处到 stop-1 处的所有字符，其长度为 stop减 start。
  - 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数。
  - 与 slice() 和 substr() 方法不同的是，substring() 不接受负的参数。
- **substr() 方法**可在字符串中抽取从 *start* 下标开始的指定数目的字符。
  - 语法：`stringObject.substr(start,length)`
  - 一个新的字符串，包含从 stringObject 的 start（包括 start 所指的字符） 处开始的 length 个字符。如果没有指定 length，那么返回的字符串包含从 start 到 stringObject 的结尾的字符。
  - 如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。
  - ECMAscript 没有对该方法进行标准化，因此反对使用它。

String 对象的方法 slice()、substring() 和 substr() （不建议使用）都可返回字符串的指定部分。slice() 比 substring() 要灵活一些，因为它允许使用负数作为参数。slice() 与 substr() 有所不同，因为它用两个字符的位置来指定子串，而 substr() 则用字符位置和长度来指定子串。

还要注意的是，String.slice() 与 Array.slice() 相似。

### 13、Array对象中slice() 、splice（）的区别

**slice() 方法**可从已有的数组中返回选定的元素。

- 语法：`arrayObject.slice(start,end)`
- 返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。在只有一个参数的情况下，返回从该参数指定位置开始到当前数组末尾的所有项。
- 该方法不改变原字符串，而是返回新的字符串。如果想删除数组中的一段元素，应该使用方法 Array.splice()。
- 如果slice()方法的参数中有一个负数，则用数组长度加上该数来确定相应的位置。
- 如果结束为止小于起始位置，则返回空数组。

**splice() 方法**主要用途是向数组的中部插入项。

- 语法：`arrayObject.splice(index,howmany,item1,.....,itemX)`

  

- | index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
  | ----------------- | ------------------------------------------------------------ |
  | howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。       |
  | item1, ..., itemX | 可选。向数组添加的新项目。                                   |

- splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）

### 14、Object.assign()

语法：`Obejct.assign(target,...sources)`

用途：将来自一个或多个源对象中的值复制到一个目标对象，它将返回目标对象。

其中对象的继承属性和不可枚举属性是不能拷贝的，所以不能使用它来实现深拷贝。

assign这个方法会把原型上面的内容也拷贝了。

```javascript
let obj = { name:"goudan"}
let obj2 = { name:"xiaofei",age:12}
obj2.__proto__.sex = "man"
console.log(Object.assign(obj,obj2));//在obj的__proto__对象上面也会有sex属性
```

第一级属性深拷贝，从第二级属性开始就是浅拷贝。

如果多个源对象具有同名属性，则排位靠后的源对象会覆盖排位靠前的。但null或undefined被视为空对象一样对待，不会覆盖。

```js
var receiver = {};
Object.assign(receiver, 
    {
    	type: "js", 
    	name:"file.js"
	},
    {
    	type: "css"
	}
)
console.log(receiver); // {type: "css", name: "file.js"}
```



```js
//实现 deepAssign({a: {b: 1, c: 2}}, {a: {c: 3}});
//=> {a: {b: 1, c: 3}}

// 只有两个对象
function deepAssign(obj1, obj2){
    for(var item in obj2){
        obj1[item] = typeof obj2[item] === 'object' ? deepClone(obj1[item], obj2[item]) : obj2[item];
    }
    return obj1;
}
// 通用
function deepAssign() {
  var args = Array.from(arguments);
  return args.reduce(deepClone, args[0]);

  function deepClone(target, obj){
    if(!target) target = Array.isArray(obj) ? [] : {};
      for(key in obj){
        target[key] = typeof obj[key] ==="object" ? deepClone(target[key], obj[key]) : obj[key]
      }
    return target;
  }
}
```

### 15、ES6之Array.from()方法

1、类数组对象：所谓类数组对象，最基本的要求就是**具有length属性的对象**。

2、Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。

​	Array.from有三个参数，Array.from(arrayLike[, mapFn[, thisArg]])，

​	arrayLike：想要转换成数组的伪数组对象或可迭代对象；

​	mapFn：如果指定了该参数，新数组中的每个元素会执行该回调函数；

​	thisArg：可选参数，执行回调函数 mapFn 时 this 对象。

​	该方法的返回值是一个新的数组实例（真正的数组）。

**例1:Array.from ({length:n}, Fn) 将类数组转换为数组**

```js
Array.from({length:3}, () => 'jack') //["jack", "jack", "jack"]
 
Array.from({length:3}, item => (item = {'name':'shao','age':18})) //[{'name':'shao','age':18}, {'name':'shao','age':18}, {'name':'shao','age':18}]
 
Array.from({length:2}, (v, i) => item = {index:i});
//生成一个index从0到4的数组对象[{index: 0},{index: 1}]
```

```js
let array = {
    0: 'name', 
    1: 'age',
    2: 'sex',
    3: ['user1','user2','user3'],
    'length': 4
}
let arr = Array.from(array)
console.log(arr) // ['name','age','sex',['user1','user2','user3']]
```

如果将上面代码中length属性去掉arr将会是一个长度为0的空数组，如果将代码修改一下，就是具有length属性，但是对象的属性名不再是数字类型的，而是其他字符串型的，代码如下：

```js
let array = {
    'name': 'name', 
    'age': 'age',
    'sex': 'sex',
    'user': ['user1','user2','user3'],
    'length': 4
}
let arr = Array.from(array )
console.log(arr)  // [ undefined, undefined, undefined, undefined ]
```

会发现结果是长度为4，元素均为undefined的数组，由此可见，要将一个类数组对象转换为一个真正的数组，必须具备以下条件：
（1）该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。
（2）该类数组对象的属性名必须为数值型或字符串型的数字
该类数组对象的属性名可以加引号，也可以不加引号

**例2:Array.from (obj, mapFn)**

obj指的是数组对象、类似数组对象或者是set对象，map指的是对数组中的元素进行处理的方法。

```js
let arr = [1,1,2,5,5,6,7,8,9]
let set = new Set(arr)
console.log(Array.from(set))  // [1, 2, 5, 6, 7, 8, 9]
```

```js
//将数组中布尔值为false的成员指为0
Array.from([1, ,2,3,3], x => x || 0) //[1,0,2,3,3]
 
//将一个类似数组的对象转为一个数组，并在原来的基础上乘以2倍
let arrayLike = { '0': '2', '1': '4', '2': '5', length: 3 }
Array.from(arrayLike, x => x*2) //[4,8,10]
 
//将一个set对象转为数组，并在原来的基础上乘以2倍
Array.from(new Set([1,2,3,4]), x => x*2) //[2,4,6,8]
```

**例3:Array.from(string) 将字符串转换为数组**

```js
Array.from('abc') //['a','b','c']
```

例子4——将Map解构转为数组，最方便的做法就是使用扩展运算符(...)

```js
const myMap = new Map().set(true, 7)
console.log(myMap); //Map(1) {true => 7}
console.log([...myMap]); //[true ,7]
```

### 16、数组去重的方法

**1、利用ES6 Set去重（ES6中最常用）**

```js
function unique (arr) {
  return Array.from(new Set(arr))
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
 //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

不考虑兼容性，这种去重的方法代码最少。这种方法无法去掉“{}”空对象。

**2、利用for嵌套for，然后splice去重（ES5中最常用）**

```js
function unique(arr){            
    for(var i=0; i<arr.length; i++){
        for(var j=i+1; j<arr.length; j++){
            if(arr[i]==arr[j]){         
                arr.splice(j,1);
                j--;
            }
        }
    }
	return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
    console.log(unique(arr))
    //[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}]     
    //NaN和{}没有去重，两个null直接消失了
```

**3、for...of + includes()**

双重for循环的升级版，外层用 for...of 语句替换 for 循环，把内层循环改为 includes()

先创建一个空数组，当 includes() 返回 false 的时候，就将该元素 push 到空数组中 

类似的，还可以用 indexOf() 来替代 includes()

```js
function unique(arr) {
    var result = []
    for (var i of arr) {
        !result.includes(i) && result.push(i)
    }
    return result
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
   // [1, "true", true, 15, false, undefined, null, NaN, NaN, "NaN", 0, "a", {…}, {…}]      //NaN、{}没有去重
```

**4、利用indexOf去重**

```js
function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!');
        return;
    }
    var array = [];
    for (var i = 0; i < arr.length; i++) {
        if (array.indexOf(arr[i]) === -1) {
            array.push(arr[i]);
        }
    }
    return array;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
   // [1, "true", true, 15, false, undefined, null, NaN, NaN, "NaN", 0, "a", {…}, {…}]      //NaN、{}没有去重
```

**5、利用sort()**

```js
function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!')
        return;
    }
    arr = arr.sort()
    var arrry= [arr[0]];
    for (var i = 1; i < arr.length; i++) {
        if (arr[i] !== arr[i-1]) {
            arrry.push(arr[i]);
        }
    }
    return arrry;
}
     var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
        console.log(unique(arr))
// [0, 1, 15, "NaN", NaN, NaN, {…}, {…}, "a", false, null, true, "true", undefined]      // NaN、{}没有去重
```

**6 、利用hasOwnProperty**

```js
function unique(arr) {
    var obj = {};
    return arr.filter(function(item, index, arr){
        return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)
    })
}
    var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
    console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}]   //所有的都去重了
```

**7、利用filter**

```js
function unique(arr) {
  return arr.filter(function(item, index, arr) {
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });
}
    var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
        console.log(unique(arr))
//[1, "true", true, 15, false, undefined, null, "NaN", 0, "a", {…}, {…}]
```

**8、利用Map数据结构去重**

```js
function arrayNonRepeatfy(arr) {
  let map = new Map();
  let array = new Array();  // 数组用于返回结果
  for (let i = 0; i < arr.length; i++) {
    if(map.has(arr[i])) {  // 如果有该key值
      map.set(arr[i], true); 
    } else { 
      map.set(arr[i], false);   // 如果没有该key值
      array.push(arr[i]);
    }
  } 
  return array;
}
 var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
 console.log(arrayNonRepeatfy(arr))
//[1, "a", "true", true, 15, false, 1, {…}, null, NaN, NaN, "NaN", 0, "a", {…}, undefined]
// {}没去
```

创建一个空Map数据结构，遍历需要去重的数组，把数组的每一个元素作为key存到Map中。由于Map中不会出现相同的key值，所以最终得到的就是去重后的结果。

**9、利用reduce+includes**

```js
function unique(arr){
    return arr.reduce((prev,cur) => prev.includes(cur) ? prev : [...prev,cur],[]);
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
// [1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {…}, {…}]
```

**10、for...of + Object**

首先创建一个空对象，然后用 for 循环遍历

利用对象的属性不会重复这一特性，校验数组元素是否重复

```js
function unique(arr){
    let result = []
    let obj = {}
    for (let i of arr) {
        if (!obj[i]) {
            result.push(i)
            obj[i] = 1
        }
    }
    return result
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr));
// [1, "true", 15, false, undefined, null, NaN, 0, "a", {…}]
```

### 17、对象数组去重

```js
const objArr = [{
    name: '名称1'
},{
    name: '名称2'
},{
    name: '名称3'
},{
    name: '名称1'
},{
    name: '名称2'
}]

const obj = {}
const newObjArr = []
for(let i = 0; i < objArr.length; i++){
    if(!obj[objArr[i].name]){
        newObjArr.push(objArr[i]);
        obj[objArr[i].name] = true
    }
}

console.log(newObjArr)；
/*结果：
     [{
        name: '名称1'
      },{
        name: '名称2'
      },{
        name: '名称3'
      }]
*/
```

```js
const objArr = [{
    name: '名称1'
},{
    name: '名称2'
},{
    name: '名称3'
},{
    name: '名称1'
},{
    name: '名称2'
}]
const obj = {}
const newObjArr =  objArr.reduce((prev, curr)=>{
    obj[curr.name] ? true : obj[curr.name] = true && prev.push(curr);
    return prev
}, [])
console.log(newObjArr)
```

### 18、fetch发送post请求时，总是发送两次，第一次状态码204，第二次才成功

因为你用的fetch post修改了请求头,导致fetch第一次发送一个options请求，询问服务器是否支持修改的请求头，如过服务器支持，那么将会再次发送真正的请求。

### 19、跨域

**什么是跨域**

- 浏览器有同源策略，不允许ajax访问其他域接口。

- 跨域条件：协议、域名、端口有一个不同就算跨域。

**JSONP：**ajax请求受**同源策略**影响，不允许进行跨域请求，而**script标签src属性中的链接却可以访问跨域的js脚本**，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src中进行了调用，这样实现了跨域。

**JSONP的缺点：**

- JSON只支持get，因为script标签只能使用get请求；


- JSONP需要后端配合返回指定格式的数据。

- jsonp在调用失败的时候不会返回各种HTTP状态码

- 安全性。万一假如提供jsonp的服务存在页面注入漏洞，即它返回的javascript的内容被人控制的

**ajax与jsonp的区别**

- ajax和jsonp这两种技术再调用方式上“看起来很像”，目的也一样，都是请求一个url，然后把服务器返回的数据进行处理，因此jquery和ext等框架都把jsonp作为ajax的一种形式进行了封装。
- 但ajax和jsonp在本质上是不同的东西。ajax的核心是通过XmlHttpRequest获取非本页内容，而jsonp的核心则是动态添加。

**如何实现跨域**

- **JSONP：通过动态创建script，再请求一个带参网址实现跨域通信。**

  ```js
  <script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
  <script>
      function jsonp(data) {
      	console.log(data);
  	}    
  </script>
  ```

  在开发中可能会遇到多个JSONP请求的回调函数名是相同的，这时候就需要自己封装一个JSONP

  ```js
  function jsonp(url, jsonpCallback, success) {
      let script = document.createElement("script");
      script.src = url;
      script.async = true;
      script.type = "text/javascript";
      window[jsonCallback] = function(data) {
          success & success(data);
      };
      document.body.appendChild(script);
  }
  jsonp(
  	"http://xxx",
      "callback",
      function(value) {
          console.log(value);
      }
  );
  ```

- document.domain + iframe跨域：两个页面都通过js强制设置document.domain为基础主域，就实现了同域。

  该方式只能用于二级域名相同的情况下，比如a.test.com和b.test.com适用于该方法。

  只需要给页面添加document.domain = 'test.com'表示二级域名相同就可以实现跨域。

- location.hash + iframe跨域：a欲与b跨域相互通信，通过中间页c来实现。 三个页面，不同域之间利用iframe的location.hash传值，相同域之间直接js访问来通信。


- window.name + iframe跨域：通过iframe的src属性由外域转向本地域，跨域数据即由iframe的window.name从外域传递到本地域。


- postMessage跨域：可以跨域操作的window属性之一。

  postMessage和iframe相结合的方法。postMessage(data,origin)方法允许来自不同源的脚本采用异步方式进行通信，可以实现跨文本档、多窗口、跨域消息传递。

  这种方式通常用于获取嵌入页面中的第三方页面数据。一个页面发送消息，另一个页面判断来源并接收消息。

  ```js
  // 发送消息端
  window.parent.postMessage('message', 'http://test.com');
  // 接收消息端
  var mc = new MessageChannel();
  mc.addEventListener('message', (event) => {
      var origin = event.origin || event.originalEvent.orign;
      if (origin === 'http://test.com') {
          console.log('验证通过');
      }
  })
  ```

- **CORS：（服务器端设置http header）服务端设置Access-Control-Allow-Origin即可，前端无须设置，若要带cookie请求，前后端都需要设置。**

```js
// 第二个参数填写允许跨域的域名称，不建议直接写"*"
response.setHeader("Access-Control-Allow-Origin", "http://a.com, http://b.com");
response.setHeader("Access-Control-Allow-Headers", "X-Requested-With");
response.setHeader("Access-Control-Allow-Methods", "PUT, POST, GET, DELETE, OPTIONS");
// 接收跨域的cookie
response.setHeader("Access-Control-Allow-Credential", "true")
```

- **代理跨域：起一个代理服务器，实现数据的转发。**

### 20、优化SPA应用的首屏加载速度慢的问题

- 将公用的JS库通过script标签外部引入，减小 `app.bundle` 的大小，让浏览器并行下载资源文件，提高下载速度；
- 在配置路由时，页面和组件使用懒加载的方式引入，进一步缩小 `app.bundle` 的体积，在调用某个组件时再加载对应的js文件；
- 加一个首屏loading图，提升用户体验；

### 21、jQuery获取的dom对象和原生的dom对象的区别

js原生获取的dom是一个对象，jQuery对象就是一个数组对象，其实就是选择出来的元素的数组集合，所以说他们两者是不同的对象类型不等价。

原生DOM对象转jQuery对象：

```js
var box = document.getElementById('box');
var $box = $(box);
```

jQuery对象转原生DOM对象：

```js
var $box = $('#box');
var box1 = $box[0];       // 方法一
var box2 = $box.get(0);   // 方法二
```

### 22、深拷贝和浅拷贝

**区别**

1.浅拷贝： 将原对象或原数组的**引用**直接赋给新对象，新数组，新对象／数组只是原对象的一个引用

2.深拷贝： 创建一个新的对象和数组，将原对象的各项属性的“**值**”（数组的所有元素）拷贝过来，是“值”而不是“引用”

**为什么要使用深拷贝？**

我们希望在改变新的数组（对象）的时候，不改变原数组（对象）

**深拷贝数组**

1.直接遍历

```js
function copyArr(arr) {
    let res = []
    for (let i = 0; i < arr.length; i++) {
     res.push(arr[i])
    }
    return res
}
var arr = [1,2,3,4,5]
var arr2 = copyArr(arr)
```

2.slice()

```js
var arr = [1,2,3,4,5]
var arr2 = arr.slice()
```

3.concat()

```js
var arr = [1,2,3,4,5]
var arr2 = arr.concat()
```

**深拷贝对象**

迭代递归法

这是最常规的方法，思想很简单：就是对对象进行迭代操作，对它的每个值进行递归深拷贝。

```js
function deepClone(obj){
    var newObj= obj instanceof Array ? []:{};
    for(var item in obj){
        var temple= typeof obj[item] == 'object' ? deepClone(obj[item]):obj[item];
        newObj[item] = temple;
    }
    return newObj;
}
```

```js
function deepClone(obj, newObj) {
  for (var key in obj) {
    var val = obj[key];
    if (val instanceof Object) {   
      var tempObj = new val.constructor;
      deepClone(val, tempObj);
      newObj[key] = tempObj;
    } else {
      newObj[key] = val;
    }
  }
}
```

“一招鲜，吃遍天” ——序列化反序列化法** 

**JSON.parse(JSON.stringify(XXXX))**

```js
var array = [
    { number: 1 },
    { number: 2 },
    { number: 3 }
];
var copyArray = JSON.parse(JSON.stringify(array))
copyArray[0].number = 100;
console.log(array); //  [{number: 1}, { number: 2 }, { number: 3 }]
console.log(copyArray); // [{number: 100}, { number: 2 }, { number: 3 }]
```

它也只能深拷贝对象和数组，对于其他种类的对象，会失真。这种方法比较适合平常开发中使用，因为通常不需要考虑对象和数组之外的类型。

缺点：

- 会忽略undefined
- 不能序列化函数
- 不能解决循环引用的对象

在通常情况下，复杂数据都是可以序列化的，所以这个函数可以解决大部分问题，并且该函数是内置函数中处理深拷贝性能最快的。当然如果你的数据中含有以上三种情况下，可以使用lodash的深拷贝函数。

### 23、清空数组的方法

**方式1：splice函数**

arrayObject.splice(index,howmany,element1,.....,elementX)

index：必选，规定从何处添加/删除元素。

howmany：必选，规定应该删除多少元素。未规定此参数，则删除从 index 开始到原数组结尾的所有元素。

element1:可选，规定要添加到数组的新元素。

```js
<script type ="text/javascript">  
　　var arr = [1,2,3,4];  
   arr.splice(0,arr.length);  
</script>  
```

**方式2：给数组的length赋值为0**

```js
<script type ="text/javascript">  
　　var arr = [1,2,3,4];  
   arr.length = 0;
</script> 
```

赋予数组的长度小于本身的长度，数组中后面的元素将被截断。

赋予数组的长度大于本身的长度，将扩展数组长度，多的元素为undefined。

**方式3：直接赋予新数组 []**

```js
<script type ="text/javascript">  
　　var arr = [1,2,3,4];  
   arr = [];
</script> 
```

这种方式为将arr重新复制为空数组，之前的数组如果没有被引用，将等待垃圾回收。

### 24、Pomise.all的使用

待**全部完成**之后统一执行

```js
let p1 = new Promise((resolve, reject) => {
  resolve('成功了')
})

let p2 = new Promise((resolve, reject) => {
  resolve('success')
})

let p3 = Promise.reject('失败')

Promise.all([p1, p2]).then((result) => {
  console.log(result)               //['成功了', 'success']
}).catch((error) => {
  console.log(error)
})

Promise.all([p1,p2,p3]).then((result) => {
  console.log(result)
}).catch((error) => {
  console.log(error)      // 失败了，打出 '失败'
})
```

```js
let wake = (time) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time / 1000}秒后醒来`)
    }, time)
  })
}

let p1 = wake(3000)
let p2 = wake(2000)

Promise.all([p1, p2]).then((result) => {
  console.log(result)       // [ '3秒后醒来', '2秒后醒来' ]
}).catch((error) => {
  console.log(error)
})
```

**需要特别注意的是，Promise.all获得的成功结果的数组里面的数据顺序和Promise.all接收到的数组顺序是一致的，即p1的结果在前，即便p1的结果获取的比p2要晚。这带来了一个绝大的好处：在前端开发请求数据的过程中，偶尔会遇到发送多个请求并根据请求顺序获取和使用数据的场景，使用Promise.all毫无疑问可以解决这个问题。**

### 25、简单实现 Promise.all

```js
function promiseAll(promises) {
    return new Promise((resolve, reject) => {
      let resultCount = 0;
      let results = new Array(promises.length);

      for (let i = 0; i < promises.length; i++) {
        promises[i].then(value => {
          resultCount++;
          results[i] = value;
          if (resultCount === promises.length) {
            return resolve(results)
          }
        }, error => {
          reject(error)
        })
      }
    })
  }

  let p1 = new Promise(resolve => resolve('p1'))
  let p2 = new Promise(resolve => resolve('p2'))
  let p3 = Promise.reject('p3 error')

  promiseAll([p1, p2]).then(results => {
    console.log(results)    // ['p1', 'p2']
  }).catch(error => {
    console.log(error)
  })

  promiseAll([p1, p2, p3]).then(results => {
    console.log(results)
  }).catch(error => {
    console.log(error)      // 'p3 error'
  })
```

### 26、Promise.race的使用

只要**有一个完成**就执行，返回为最先完成的

```js
let p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
  },1000)
})

let p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('failed')
  }, 500)
})

Promise.race([p1, p2]).then((result) => {
  console.log(result)
}).catch((error) => {
  console.log(error)  // 打开的是 'failed'
})
```

### 27、作用域链

```js
var a = 100
function F1() {
    var b = 200
    function F2() {
        var c = 300
        console.log(a)	// a是自由变量，向父级作用域寻找a，未果，再向上一级父级作用域寻找a
        console.log(a)	// b是自由变量，向父级作用域寻找b
        console.log(a)
    }
    F2()
}
F1()               // 自由变量不断地往父级作用域去找，形成一个链式结构
```

改变作用域链的方法

with、try...catch、eval

### 28、  一个完整的JavaScript实现应该由下列三个不同的部分组成

1.核心(ECMAScript) ——提供核心语言功能
2.文档对象模型(Dom) ——提供访问和操作网页内容的方法和接口
3.浏览器对象模型(Bom) ——提供与浏览器交互的方法和接口

### 29、延迟脚本

defer=“defer” 
defer属性:表明脚本在执行时不会影响页面的构造，也就是说，脚本会被延迟到整个页面都解析完毕再运行

### 30、NaN

var result = “a” < 3; // false，因为“a”被转化成了NaN
根据规则，任何操作数与NaN进行关系比较，结果都是false

### 31、在函数体内可以通过arguments对象来访问这个参数数组，从而获取传递给函数的每一个参数  

```js
function doadd() {
    if (arguments.length == 1) {
        alert(arguments[0] + 10);
    } else if (arguments.length == 2) {
        alert(arguments[0] + arguments[1]);
    }
}
doAdd(10) // 20
doAdd(30, 20) // 50
```

### 32、js数组拍平

1、递归

```js
function flatArr(arr) {
	var newArr = [];
	arr.forEach((val) => {
		if (Array.isArray(val)) {
			newArr = newArr.concat(flatArr(val))
		} else {
			newArr.push(val)
		}
	})
	return newArr;
}
```

2、reduce

```js
function flatArr(arr) {
   return arr.reduce((pre, cur) => pre.concat(Array.isArray(cur) ? flatArr(cur) : cur), [])
}
```

3.利用数组join()或toString()方法

```js
// join()
function flatArr(arr) {
  	arr.join().split(',')
	return JSON.parse(`[${arr.join()}]`)
}
// toString()
function flatArr(arr) {
	arr.toString().split(',')
	return JSON.parse(`[${arr.toString()}]`)
}
```

4.es6数组的flat()方法 (浏览器版本过低不支持)

flat方法默认打平一层嵌套，也可以接受一个参数表示打平的层数，传 Infinity 可以打平任意层。

```js
function flatArr(arr) {
  	return arr.flat(Infinity);
}
```

### 33、async和await

- async/await是写异步代码的新方式，以前的方法有回调函数和Promise

- async/await是基于Promise实现的，它不能用于普通的回调函数及节点回调

- async/await和Promise一样，是非阻塞的

- async/await使得异步代码看起来像同步代码

一个函数如果加上async，那么该函数就会返回一个Promise

```js
async function test() {
    return "1";
}
console.log(test());  // Promise {<resolved>: "1"}
```

可以把async看成将函数返回值使用Promise.resolve()包裹了起来

await只能在async函数中使用

```js
function sleep() {
    return new Promise(resolve => {
        setTimeout(() => {
            console.log('finish');
            resolve("sleep");
        }, 2000);
    });
}
async function test() {
    let value = await sleep();
    console.log("object");
}
test();
// finish
// object
```

因为await会等待sleep函数resolve，所以即使后面是同步代码，也不会先去执行同步代码再来执行异步代码。

async和await相比直接使用Promise来说，优势在于处理then的调用链，能够更清晰准确的写出代码。缺点在于滥用await可能会导致性能问题，因为await会阻塞代码，也许之后的异步代码并不依赖于前者，但仍然需要等待前者完成，导致失去了并发性。

#### JavaScript 利用 async await 实现 sleep 效果

```js
const sleep = (timeountMS) => new Promise((resolve) => {
  setTimeout(resolve, timeountMS);
});

(async () => {
  console.log('11111111, ' + new Date());
  await sleep(2000);
  console.log('22222222, ' + new Date());
  await sleep(2000);
  console.log('33333333, ' + new Date());
})();
```

### 34、手写设置cookie

**1.设置cookie一天后过期**

```js
function setCookie(name,expireday){
    var dayobject = new Date();  // Date()函数获取当前的日期和时间
    // getTime()函数获取的事1970年1月1号至今的毫秒数
    // 注意要多加8小时，我们位于东八区比标准时间相差8小时
    var daynum = dayobject.getTime() + expireday*(24+8)*60*60*1000;
    // 计算过期时间毫秒数
    dayobject.setTime(daynum);
    // 设置超时的时间
    alert('name=' + name + ';' + 'expires=' + dayobject.toUTCString());
    document.cookie = 'name=' + name + ';' + 'expires=' + dayobject.toUTCString();
}
setCookie('coco',1)
```

**2.设置cookie马上过期**

```js
function delCookie(name){
    var expires = new Date();
    expires.setTime(expires.getTime() - 1);
    document.cookie = 'name='+name+';'+'expires=' + expires.toGMTString();
}
// 设置cookie的过期时间是比当前时间提前一秒，也就是立马过期了。
```

### 35、获得一段范围内的随机数

值 = Math.floor(Math.random()可能值的总数+第一个可能的值)
例：选择一个1-10之间的数组
 var num = Math.floor(Math.random()*10+1)

### 36、大数相加

**解释**

- 首先我们用字符串的形势来保存大数，就保证了其在数学表示上不会发生变化
- 初始化`res, temp`变量来保存中间计算的结果，在将两个字符串`split`为数组，以便我们进行每一位的运算
- 循环的第一次就是进行 "个位" 的运算，将二者最末尾的两个数相加，由于每一位数字是0 - 9，所以需要进行进位，在进过取余数操作后，将结果保留在个位。
- 判断 `temp` 是否大于 10，若是则将 `temp` 赋值为 `true`。
- 在两个大数中的一个还有数字没有参与运算，或者前一次运算发生进位后，进行下一次循环。
- 接着除了对新的两个数字相加还要加上 `temp`，**若上次发生了进位，则此时 `temp` 为 `true`，Js因为存在隐式转换，所以 `true` 转换为 1，我们借用 Js 的类型转换，完成了逻辑上的逢10进1操作。**
- 接下来就是重复上述的操作，直到计算结束。
- 除去非数字的字符

```js
function sumBigNumber(a, b) {
    if (a.charAt(0) == 0 || b.charAt(0) == 0) {
      return "0";
    }
    var res = '', temp = 0;
    a = a.toString().split('');
    b = b.toString().split('');
    while (a.length || b.length || temp) {
        temp += ~~a.pop() + ~~b.pop();
        res = (temp % 10) + res;
        temp = temp > 9;
    }
    return res.replace(/^0+/, '');
}
console.log(sumBigNumber('3782647863278468012934670', '23784678091370408971329048718239749083')); // 23784678091374191619192327186252683753
```

### 37、5个原型规则

- 所有的引用类型（数组，对象，函数），都具有对象特性，即可自由扩展属性（除了null以外）
- 所有的引用类型（数组，对象，函数），都有一个_ proto _(隐式原型)属性，属性值是一个普通对象
- 所有的函数，都有一个prototype(显式原型)属性，属性值也是一个普通对象
- 所有的引用类型（数组，对象，函数）,_ proto _属性值指向他的构造函数的prototype属性
- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的_ proto _（即它的构造函数的prototype）

### 38、一个原型链继承的例子

```js
// 写一个封装DOM查询的例子

function Elem(id){
    this.elem = document.getElementById(id);
}

Elem.prototype.html = function(val){
    var elem = this.elem;
    if(val){
        elem.innerHTML = val;
        return this;  // 链式操作
    } else{
        return elem.innerHTML;
    }
}
 
Elem.prototype.on = function(type,fn){
    var elem = this.elem;
    elem.addEventListener(type,fn);
    return this;
}
 
var div1 = new Elem('div');
div1.html('<p>hello imooc</p>').on('click', function(){
    alert('clicked');
}).html('<p>javascript</p>');
```

### 39、开放封闭原则

其核心思想是软件实体应该是可扩展的，而不可修改的，即对扩展开放，对修改封闭。

开放封闭主要体现在两个方面:
**对扩展开放**，意味着新的需求或变化时，可以对现有代码进行扩展，以适应新的情况。
**对修改封闭**，意味着类一旦设计完成时，就可以独立完成其工作，而不要对类进行任何修改。 

### 40、new一个对象的过程

```js
   function Person () {  
        this.name = name;  
        this.age = age;  
        this.job = job;  
        this.sayName = function () {  
            return this.name;  
        }
  }  
  var person = new Person("tom", 21, "WEB");  
  console.log(person.name)
```

1、创建一个新对象，如：var person = {};

2、新对象的_ proto _属性指向构造函数的原型对象。

3、将构造函数的作用域赋值给新对象。（this对象指向新对象）

4、执行构造函数内部的代码，将属性和方法添加给person中的this对象。

5、返回新对象person。

```js
  var person = {};  
  person._proto_ = Person.prototype;//引用构造函数的原型对象  
  Person.call(person);//将构造函数的作用域给person,即：this值指向person  

  Function.methods("new", function () {  
     //新创建一个对象，它继承了构造器的原型对象。  
     var that = Object.create(this.prototype); //此时，this是指向Function构造器的。  
     //调用构造器，绑定this对象到新对象that上  
     var other = this.apply(that, argument); //此时，this对象指向that对象。  
     //如果它的返回值不是一个对象，就返回新的对象。  
     return (typeof other === "object" && other) || that;  
 });  
```

通过new关键字创建某构造函数的新实例对象，**就是将原型链与实例的this联系起来，this指向这个新对象，同时也指向这个构造函数**，并且this对象还是这个构造函数的实例。



对于new来说，还需要注意下运算符优先级。

```js
function Foo() {
    return this;
}
Foo.getName = function () {
    console.log('1');
};
Foo.prototype.getName = function () {
    console.log('2');
};

new Foo.getName(); // 1
new Foo().getName(); // 2

// new Foo()的优先级大于new Foo，所以对于上述代码来说可以这样划分执行顺序
new (Foo.getName());
(new Foo()).getName();
```

### 41、闭包以及实际应用

**闭包就是能够读取其他函数内部变量的函数。**只有函数内部的子函数才能读取局部变量，所以闭包可以理解成“定义在一个函数内部的函数“。在本质上，闭包是将函数内部和函数外部连接起来的桥梁。

**闭包的用途**：

1、读取函数内部的变量，并且让这些变量在函数执行完后, 仍然存活在内存中(延长了局部变量的生命周期)。

2、让函数外部可以操作(读写)到函数内部的数据(变量/函数)

**缺点：**容易形成循环引用，比普通函数占用更多的内存。闭包会导致原始作用域链不释放,造成内存泄漏。参数和变量不会被垃圾回收机制回收。

**解决方法：**

- 把造成循环引用的变量设为null
- 不用的变量及时释放

```js
    function fn1() {
        var arr = new Array[99999999999999999];
        function fn2() {
            console.log(arr);
        }
        return fn2;
    }

    var f = fn1();
    f();

    f = null;
```

**高阶函数**

如果一个函数A的实参为函数，或者函数A内部又定义了函数B，则称A为高阶函数。其中B可称为**内层函数，**这时A相对于B来说又可称为**外层函数。**

**使用场景**

1、函数作为另一个函数的返回值

```js
function F1() {
    var a = 100;
    // 返回一个函数（函数作为返回值）
    return function() {
        console.log(a); // a是自由变量，父级作用域寻找
    }
}
// f1得到一个函数
var f1 = F1();
var a = 200;
f1(); // 100
```

2、参数作为返回值

```js
function F1() {
    var a = 100;
    // 返回一个函数（函数作为返回值）
    return function() {
        console.log(a); // a是自由变量，父级作用域寻找
    }
}

function F2(fn) {
    var a = 200;
    fn();
}

var f1 = F1();
F2(f1); // 100
```

3、将函数的形参作为实参传递给另一个函数调用

```js
function logMsgDelay(msg, time) {
    setTimeout(function () {
        console.log(msg);
    }, time);
}

logMsgDelay('aaa', 1000);
```

**闭包的实际应用**

**1.通过闭包可以让内层函数延迟执行，只有需要时再执行它**

```js
function highLevelFunct2() {
    var arr = ['a', 'b', 'c'];
    var size = function () {
        alert(arr.length);
    };
    return size;
}


function testClosure() {
    var f = highLevelFunct2();
    f();
}
```

**2.通过闭包，内层函数可以将外层函数的局部变量进行封装，封闭后就只有内层函数才能访问到外层函数的局部变量。**

```js
//  计数器
function myCounter() {
    var counter = 0;
    return function add () {
        return counter += 1;
    }
}

function testClosure() {
    var increase = myCounter();
    increase();	// 1
    increase(); // 2
    increase(); // 3
}
```



```js
//  主要用于封装变量，收敛权限
function isFirstLoad() {
    var _list = [];  // 变量封装，在isFirstLoad函数外面，根本不可能修改掉_list的值
    return function(id) {
        if (_list.indexOf(id) >= 0) {
            return false;
        } else {
            _list.push(id);
            return true;
        }
    }
}

var firstLoad = isFirstLoad(); // 自执行函数，就是不用调用，只要定义完成，立即执行的函数
firstLoad(10); // true
firstLoad(10); // true
firstLoad(20); // false
```

**3.定义JS模块**

- 将所有的数据和功能都封装在一个函数内部(私有的)
- 只向外暴露一个包含多个方法的对象或函数
- 模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能

```js
// MyTool.js
function myTool() {
    // 1. 私有的数据
    var money = 1000;
    // 2. 提供操作私有数据的函数
    function get() {
        money *= 10;
        console.log('赚了一笔钱, 总资产:' + money + '元');
    }

    function send() {
        money --;
        console.log('花了一笔钱, 总资产:' + money + '元');
    }

    return {
        'get': get,
        'send': send
    }
}

<script type="text/javascript" src="js/MyTool.js"></script>
<script type="text/javascript">
   var toolObj = myTool();
   toolObj.get();
   toolObj.send();
</script>
```

```js
// MyTool1.js
(function (w) {
    // 1. 私有的数据
    var money = 1000;
    // 2. 提供操作私有数据的函数
    function get() {
        money *= 10;
        console.log('赚了一笔钱, 总资产:' + money + '元');
    }

    function send() {
        money --;
        console.log('花了一笔钱, 总资产:' + money + '元');
    }

    // 向外部暴露对象
    w.myTool = {
        'get': get,
        'send': send
    }

})(window);

<script src="js/MyTool1.js"></script>
<script>
    (function () {
        console.log(window.myTool, myTool);
        myTool.get();
        myTool.send();

        var str = 'zhangsan';
        console.log(str);
        console.log(window.str);
    })();
</script>
```

**4.实现函数节流**

```js
   function throttle(fn, delay) {
        var timer = null;
        return function () {
            clearTimeout(timer);
            timer = setTimeout(fn, delay);
        }
    }
   throttle(function () {
       console.log('大家好!!!');
   }, 200)();
```

### 42、获取xxxx-xx-xx格式的日期

```js
function formatDate(dt) {
    if (!dt) {
        dt = new Date()
    }
    var year = dt.getFullYear();
    var month = dt.getMonth() + 1;
    var date = dt.getDate();
    if (month < 10) {
        month = '0' + month;  // 强制类型转换
    }
    if (date < 10) {
        date = '0' + date; // 强制类型转换
    }
    return year + '-' + month + '-' + date;
}

var dt = new Date();
console.log(formatDate(dt));
```

### 43、写一个能遍历对象和数组的通用forEach函数

```js
function forEach(obj, fn) {
    var key;
    if (obj instanceof Array) {
        obj.forEach(function (item, index) {
            fn(index, item);
        })
    } else {
        for (key in obj) {
            fn(key, obj[key]);
        }
    }
}

var arr = [1, 2, 3];
forEach(arr, function (index, item) {
    console.log(index, item);
})

var obj = {x: 100, y: 200};
forEach(obj, function (key, value) {
    console.log(key, value);
})
```

### 44、一个通用的事件监听函数

```js
function bindEvent(elem, type, selector, fn) {
    if (fn == null) {
        fn = selector;
        selector = null;
    }
    elem.addEventListener(type, function (e) {
        var target;
        if (selector) {
            target = e.target;
            if (target.matches(selector)) {
                fn.call(target, e);
            }
        } else {
            fn(e);
        }
    })
}

// 使用代理
var div1 = document.getElementById('div1')
bindEvent(div1, 'click', 'a', function (e) {
    console.log(this.innerHTML);
})

// 不使用代理
var a = document.getElementById('a1')
bindEvent(div1, 'click', function (e) {
    console.log(a.innerHTML);
})
```

### 45、箭头函数和普通函数的区别

- 箭头函数是匿名函数，不能作为构造函数，不能使用new
- 箭头函数不绑定arguments，取而代之用rest参数...解决
- 箭头函数不绑定this，会捕获其所在的上下文的this值，作为自己的this值
- 箭头函数通过 call()  或 apply() 方法调用一个函数时，只传入了一个参数，对 this 并没有影响
- 箭头函数没有原型属性
- 箭头函数不能当做Generator函数,不能使用yield关键字

### 46、apply，call与bind

共同点：

1、都是用来**改变函数的this对象的指向**的。
2、第一个参数都是this要指向的对象。
3、都可以利用后续参数传参。

区别：

apply：最多只能有两个参数——**新this对象和一个数组arrArray**。**立即调用**

`xw.say.apply(xh, [1,2,3,4]);`

call：它可以接受多个参数，**第一个参数与apply一样**，后面则是**一串参数列表**。**立即调用**

`xw.say.call(xh, 1, 2, 3, 4);`

bind：bind() 方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind() 方法的**第一个参数 作为 this**，传入 bind() 方法的**第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数**来调用原函数。bind改变this作用域会返回一个新的函数，这个函数**不会马上执行**。

`xw.say.bind(xh, 1, 2, 3, 4)();` 或 `xw.say.bind(xh)(1, 2, 3, 4);`

### 47、字符串全排列

```js
function perm(s) {
    var result = [];
    if (s.length <= 1) {
        return [s];
    } else {
        for (var i = 0; i < s.length; i++) {
            var char = s[i];
            var newStr = s.slice(0, i) + s.slice(i + 1, s.length);
            var str = perm(newStr);

            for (var j = 0; j < str.length; j++) {
                var tmp = char + str[j];
                result.push(tmp);
            }
        }
    }
    return result;
};
```

### 48、6种声明变量的方法：var，function，let，const，import，class 

### 49、事件捕获、事件冒泡、事件委托（代理）

**事件捕获**：事件从最不精确的对象(document对象)开始触发，然后到最精确

**事件冒泡**：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发

不是所有事件都能冒泡。以下事件不冒泡：blur、focus、load、unload（关闭页面）

**事件委托（代理）**：不在事件的发生地（直接dom）上设置监听函数，而是在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素DOM的类型，来做出不同的响应。

举个例子：

有三个同事预计会在周一收到快递。为签收快递，有两种办法：一是三个人在公司门口等快递；二是委托给前台MM代为签收。现实当中，我们大都采用委托的方案（公司也不会容忍那么多员工站在门口就为了等快递）。前台MM收到快递后，她会判断收件人是谁，然后按照收件人的要求签收，甚至代为付款。这种方案还有一个优势，那就是即使公司里来了新员工（不管多少），前台MM也会在收到寄给新员工的快递后核实并代为签收。

这里其实还有2层意思的：

第一，现在委托前台的同事是可以代为签收的，即程序中的现有的dom节点是有事件的；

第二，新员工也是可以被前台MM代为签收的，即程序中新添加的dom节点也是有事件的。

**为什么要用事件委托：**

在JavaScript中，添加到页面上的事件处理程序数量将直接关系到页面的整体运行性能，因为需要不断的与dom节点进行交互，访问dom的次数越多，引起浏览器重绘与重排的次数也就越多，就会延长整个页面的交互就绪时间，这就是为什么性能优化的主要思想之一就是减少DOM操作的原因；如果要用事件委托，就会将所有的操作放到js程序里面，与dom的操作就只需要交互一次，这样就能大大的减少与dom的交互次数，提高性能；

**事件委托的原理：**

事件委托是利用事件的冒泡原理来实现的，何为事件冒泡呢？就是事件从最深的节点开始，然后逐步向上传播事件，举个例子：页面上有这么一个节点树，div>ul>li>a;比如给最里面的a加一个click点击事件，那么这个事件就会一层一层的往外执行，执行顺序a>li>ul>div，有这样一个机制，那么我们给最外面的div加点击事件，那么里面的ul，li，a做点击事件的时候，都会冒泡到最外层的div上，所以都会触发，这就是事件委托，委托它们父级代为执行事件。

**事件委托怎么实现：**

举例：最经典的就是ul和li标签的事件监听，比如我们在添加事件时候，采用事件委托机制，不会在li标签上直接添加，而是在ul父元素上添加。

**好处：**比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触发机制。

```js
// 通用的事件绑定函数
function bindEvent(elem, type, selector, fn) {
    if (fn = null) {
        fn = selector;
        selector = null;
    }
    elem.addEventListener(type, function(e){
        var target;
        if (selector) {
            target = e.target;
            if (target.matches(selector)) {
                fn.call(target, e);
            }
        } else {
            fn(e);
        }
    })
}

// 使用代理
var div1 = document.getElementById('div1');
bindEvent(div1, 'click', 'a', function(e){
    console.log(this.innerHtml);
})
// 不使用代理
var a = document.getElementById('a1');
bindEvent(a, 'click', function(e){
    console.log(a.innerHtml);
})
```



### 50、单线程

**单线程**就是同时只能做一件事，两段js不能同时执行。

原因——避免dom渲染冲突

- 浏览器需要渲染dom
- js可以修改dom 
- js执行的时候，浏览器dom渲染会暂停
- 两段js也不能同时执行(都修改dom就冲突) 

### 51、js异步及处理异步的几种方法

[看这里~](zh-cn/JavaScript/js异步及处理异步的几种方法)

### 52、this

另外，可以看看这篇文章：https://www.cnblogs.com/pengshengguang/p/11105323.html

this对象是在运行时基于函数的执行环境绑定的: 

- 在全局函数中，this--->window

- 在函数中

  1、作为对象的方法来调用  this--->当前的对象

  2、作为普通的函数调用 this--->window

  （1.2可总结为 看函数名前面是否有“.” ，有的话， “.”前面是谁，this就是谁；没有的话this就是window ）

  3、作为构造函数和new使用 this--->构造函数内部新创建的对象

  4、被call或者是apply调用（函数上下文调用） this--->第一个参数

  5、立即执行函数中的this永远都是window 

  6、箭头函数不绑定this，会捕获其所在的上下文的this值，作为自己的this值。通过 call()  或 apply() 方法调用一个函数时，只传入了一个参数，对 this 并没有影响

  ```js
  (function() {
    return [
      (() => this.x).bind({ x: 'inner' })()
    ];
  })()
  // undefined
  (function() {
    return [
      (() => this.x).bind({ x: 'inner' })()
    ];
  }).call({ x: 'outer' });
  // ['outer']
  ```


**一道this面试题**

```js
var num = 20;
var obj = {
    num: 30,
    fn: (function(num) {
        this.num *= 3;
        num += 15;
        var num = 45;
        return function() {
            this.num *= 4;
            num += 20;
            console.log(num);
        }
    })(num)
};
var fn = obj.fn;
fn(); // ->65
obj.fn(); // ->85
console.log(window.num, obj.num) // ->240, 120

// 1、fn();
// 因为立即执行函数中的this永远是window，所以 this.num = 20*3 = 60, num到上一个作用域找到是45
// 输出num 45+20=65   window.num = 60*40 = 240   obj.num = 30

// 2、obj.fn(); 
// this指向obj，所以这里面 this.num = 30，num = 65
// 输出num 65+20=85   window.num = 240           obj.num = 30*4 = 120
```

### 53、vue react jquery的区别

#### jquery和框架的区别

 框架：数据和视图分离，以数据驱动视图，只关心数据变化，dom操作被封装。数据驱动

 jquery： 依靠dom操作去组合业务逻辑。事件驱动

#### React和Vue对比

这篇文章挺好的：https://www.jianshu.com/p/b7cd52868e95?from=groupmessage

**两者本质区别**

- Vue—本质是MVVM框架，由MVC发展而来
- React—本质是前端组件化框架，由后端组件化发展而来

**模板的区别**

- Vue—使用模板（最初由Angular提出）
- React—使用JSX
- 模板语法上，更倾向于JSX
- 模板分离上，更倾向于Vue（React模板与JS混在一起，未分离）

**组件化的区别**

- React本身就是组件化，没有组件化就不是React
- Vue也支持组件化，不过是在MVVM上的扩展
- 对于组件化，更倾向于React，做得彻底而清新

**两者共同点**

- 都支持组件化
- 都是数据驱动视图

#### 什么时候用react，什么时候用vue

react灵活性比较大，处理复杂业务时有更多技术方案的选择 。
vue提供了更丰富的api，实现功能简单，但也因api多会对灵活性有一定的限制。
做复杂度比较高的项目时使用react，面向用户端复杂度不高的使用vue 。

### 54、前端模块化

**概念：**将一个复杂的程序依据一定的规则（规范）封装成几个块（文件）并进行组合。

模块的内部数据的实现是私有的，只是向外部暴露一些接口（方法）与外部其他模块通信，这就是模块化。

**优点：**模块化可以降低代码耦合度，减少重复代码，提高代码重用性，并且在项目结构上更加清晰，便于维护。  

**AMD、CMD、CommonJs、ES6的对比**

他们都是用于在模块化定义中使用的，AMD、CMD、CommonJs是ES5中提供的模块化编程的方案，import/export是ES6中定义新增的

- **AMD**

  AMD是**RequireJS**在推广过程中对模块定义的规范化产出，它是一个概念，RequireJS是对这个概念的实现，就好比JavaScript语言是对ECMAScript规范的实现。AMD是一个组织，RequireJS是在这个组织下自定义的一套脚本语言

  RequireJS：是一个AMD框架，可以异步加载JS文件，按照模块加载方法，通过define()函数定义，第一个参数是一个数组，里面定义一些需要依赖的包，第二个参数是一个回调函数，通过变量来引用模块里面的方法，最后通过return来输出。

  是一个依赖前置、异步定义的AMD框架（在参数里面引入js文件），在定义的同时如果需要用到别的模块，在最前面定义好即在参数数组里面进行引入，在回调里面加载

  ```js
  define(['./a', './b'], function(a, b) {
      a.do();
      b.do();
  });
  define(function(require,exports,module){
  	var a = require('./a');
      a.doSomething();
      var b = require('./b');
      b.doSomething();
  });
  ```

- **CMD**

  是**SeaJS**在推广过程中对模块定义的规范化产出，是一个同步模块定义，是SeaJS的一个标准，SeaJS是CMD概念的一个实现，SeaJS是淘宝团队提供的一个模块开发的js框架.

  通过define()定义，没有依赖前置，通过require加载jQuery插件，CMD是依赖就近，在什么地方使用到插件就在什么地方require该插件，即用即返，这是一个同步的概念

  ```js
  define(function(require,exports,module){...});
  ```

- **CommonJs**

  是通过module.exports定义的，在前端浏览器里面并不支持module.exports,通过**node.js后端使用**的。Nodejs端是使用CommonJS规范的，前端浏览器一般使用AMD、CMD、ES6等定义模块化开发的。

  加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的exports对象。

  CommonJS定义的模块分为:{模块引用(require)} {模块定义(exports)} {模块标识(module)}

  require()用来引入外部模块；exports对象用于导出当前模块的方法或变量，唯一的导出口；module对象就代表模块本身。

  ```js
  // a.js
  module.exports = {
      a: 1;
  }
  // or
  exports.a = 1;
  
  // b.js
  var module = require('./a.js');
  module.a; // 1
  ```

- **ES6**

  export/import对模块进行导出导入的

  commonjs和ES6模块化的区别

  - 前者支持动态导入，也就是require(${path}/xx.js)，后者目前不支持，但是已有提案
  - 前者是同步导入，因为用于服务端，文件都在本地，同步导入即使卡住主线程影响也不大。而后者是异步导入，因为用于浏览器，需要下载文件，如果也采用导入会对渲染有很大影响
  - 前者在导出时都是值拷贝，就算导出的值变了，导入的值也不会改变，所以如果想更新值，必须重新导入一次。但是后者采用实时绑定的方式，导入导出的值都指向同一个内存地址，所以导入值会跟随导出值变化。
  - 后者会编译成require/export来执行

**CMD与AMD区别**

AMD和CMD最明显的区别就是在模块定义时对依赖模块的执行时机处理不同。

**1、AMD推崇依赖前置，在定义模块的时候就要声明其依赖的模块** 

js可以方便知道依赖模块是谁，立即加载；

**2、CMD推崇就近依赖，只有在用到某个模块的时候再去require** 

需要使用把模块变为字符串解析一遍才知道依赖了那些模块，牺牲性能来带来开发的便利性，实际上解析模块用的时间短到可以忽略。

### 55、js的各种高度，如clientHeight,scrollHeight,offsetHeight ,以及scrollTop, offsetTop,clientTop

clientHeight：表示的是可视区域的高度，不包含border和滚动条

offsetHeight：表示可视区域的高度，包含了border和滚动条

scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。

clientTop：表示边框border的厚度，在未指定的情况下一般为0

scrollTop：滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。

offsetTop：子元素的外边框到父元素的内边框的垂直距离 （没边框时自然就是content到content的距离）

### 56、JSON

- js的对象表示法（JS Object Notation）

- 存储和交换文本信息的语法，类似XML

- JSON比XML更小、更快、更易解析

- 数据格式简单, 易于读写, 占用带宽小

- ```js
  // 把对象变成字符串
  JSON.stringify({"a": 10, "b": 20});
  // 把字符串变成对象
  JSON.parse('{"a": 10, "b": 20}');
  ```

### 57、webpack和gulp区别（模块化与流的区别）

gulp强调的是前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。

webpack是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。

### 58、pwa

PWA全称Progressive Web App，即渐进式WEB应用。

一个 PWA 应用首先是一个网页, 可以通过 Web 技术编写出一个网页应用。

 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能。

### 59、toString方法、valueOf方法、Symbol.toPrimitive方法

每个对象都有一个toString()方法和valueOf方法

其中**toString()方法返回一个表示该对象的字符串，valueOf方法返回该对象的原始值**。

对于**一个对象，toSting()返回"[object type]",其中type是对象类型**。

如果x不是对象，toString()返回应有的文本值。

**toString()方法和String()方法的区别**

toString()方法和String()方法都可以转换为字符串类型。 
1、toString()可以将所有的数据都转换为字符串，除了**null和undefined**。

null和undefined调用toString()方法会报错。

如果当前数据为数字类型，则toString()括号中的可以写一个数字，代表进制，可以将数字转化为对应进制字符串。

2、String()可以将null和undefined转换为字符串，但是**没法转进制字符串**。



**Symbol.toPrimitive**

JavaScript 对象转换到基本类型值时，会使用 ToPrimitive 算法，这是一个内部算法，是编程语言在内部执行时遵循的一套规则。

```js
// 没有 Symbol.toPrimitive 属性的对象
var obj1 = {};
console.log(+obj1);       //NaN
console.log(`${obj1}`);   //"[object Object]"
console.log(obj1 + "");   //"[object Object]"
```

上面的结果我们可以通过上面说的toSting()方法和value方法去理解。 
第一个，+符号。可以看成是是把数据转化为数字类型，由于obj是个空对象，所以结果是NaN 
第二个，是es6中的字符串的新语法，这里需要的结果是一个字符串，所以使用的是toString()方法，而toString()方法返回的是对象的类型。 
第三个，这里是连接符连接obj。实际上也是需要字符串的结果，所以同理。

```js
// 拥有 Symbol.toPrimitive 属性的对象
var obj2 = {
  [Symbol.toPrimitive](hint) {
    if(hint == "number"){
        return 10;
    }
    if(hint == "string"){
        return "hello";
    }
    return true;
  }
}

console.log(+obj2);     //10    --hint in "number"
console.log(`${obj2}`); //hello --hint is "string"
console.log(obj2 + ""); //"true"
```



对象在转换基本类型时，首先会调用valueOf然后调用toString。并且这两个方法你是可以重写的。

```js
let a = {
    valueOf() {
        return 0;
    }
}
```

当然你也可以重写Symbol.toPrimitive，该方法在转基本类型时调用优先级最高。

```js
let a = {
    valueOf() {
        return 0;
    },
    toString() {
        return '1';
    },
    [Symbol.toPrimitive]() {
        return 2;
    }
}
1 + a // 3
'1' + a // '12'
```

### 60、只有当加法运算时，其中一方是字符串类型，就会把另一个也转为字符串类型。其他运算只要其中一方是数字，那么另一方就转为数字。

### 61、export和export default的区别

export  default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export  default命令只能使用一次。所以import命令后面才不用加{}，因为只可能唯一对应export default命令。

本质上，export  default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字。

1、export与export default均可用于导出常量、函数、文件、模块等。

2、在一个文件或模块中，export、import可以有多个，export default仅有一个。

3、通过export 方法导出，在导入时要加{}，export  default则不需要。

4、export，import时需要知道所加载的变量名或函数名；export default，import时可指定任意名字

5、（1）输出单个值，只用export  default

（2）输出多个值，使用export

（3）export  default与普通export不要同时使用

### 62、JS内置对象

Arguments（函数参数集合）

Array（数组）

Boolean（布尔对象）

Date（日期对象）

Error（异常对象）

Function（函数构造器）

Math（数学对象）

Number（数值对象）

Object（基础对象）

RegExp（正则表达式对象）

String（字符串对象）

### 63、JavaScript RegExp对象方法

1.test()方法用来检测一个字符串是否匹配某个正则表达式，如果匹配成功，返回true，否则返回false

2.exec()方法用来检索字符串中与正则表达式匹配的值。exec()方法返回一个数组，其中存放匹配的结果。如果未找到匹配的值，则返回null

3.compile()方法可以在脚本执行过程中编译正则表达式，也可以改变已有表达式

### 64、{} == false // false

"=="运算符比较"喜欢"Number类型

```js
{} == false  <=> Number({}) == Number(false) <=> NaN == 0  // false
```

### 65、伪数组转化为数组

#### 方法一、 声明一个空数组，通过遍历伪数组把它们重新添加到新的数组中

```js
var aLi = document.querySelectorAll('li');
var arr = [];
for (var i = 0; i < aLi.length; i++) {
	arr[arr.length] = aLi[i]
}
```

#### 方法二、使用数组的slice()方法 它返回的是数组，使用call或者apply指向伪数组

```js
var arr = Array.prototype.slice.call(arg);  // 方法一
var arr = [].slice.call(arg);   			// 方法二
```

#### 方法三、使用原型继承

```js
oldarr.__proto__ = Array.prototype;
```

#### 方法四、ES6的数组新方法Array.from()  

```js
var arr = Array.from(oldarr);
```

### 66、图片懒加载和预加载

来源：https://www.cnblogs.com/psxiao/p/11542930.html

预加载：提前加载图片，当用户需要查看时可直接从本地缓存中渲染。

懒加载：懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。

两种技术的本质：两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。

懒加载对服务器前端有一定的缓解压力作用，预加载则会增加服务器前端压力。

**懒加载：**

img的data-src属性及懒加载：当访问一个页面的时候，先把img元素或是其他元素的背景图片路径替换成一张大小为1*1px图片的路径（这样就只需要请求一次），当图片出现在浏览器的可视区域内时，才设置图片真正的路径，让图片显示出来。这就是图片懒加载。

通俗一点：

1、就是创建一个自定义属性data-src存放真正需要显示的图片路径，而img自带的src放一张为1*1px的图片路径。

2、当页面滚动直至此图片出现在可视区域时，用js取到该图片的data-src的值赋给src。

ps:自定义属性可以取任何名字

**场景：**对于图片过多的页面，为了加快页面加载速度，需要将页面内未出现的可视区域内的图片先不做加载，等到滚动可视区域后再去加载。

**原理：**img标签的src属性用来表示图片的URL，当这个属性值不为空时，浏览器就会根据这个值发送请求，如果没有src属性就不会发送请求。所以，在页面 加入时将img标签的src指向为空或者指向一个小图片（loading或者缺省图），将真实地址存在一个自定义属性data-src中，当页面滚动时，将可视区域的图片的src值赋为真实的值。

**预加载：**

简单理解：就是在使用该图片资源前，先加载到本地来，真正到使用时，直接从本地请求数据就行了。

```js
var arr = [
    '../picture/1.jpg',
    '../picture/2.jpg',
    '../picture/3.jpg',
];

var imgs =[]
preLoadImg(arr);

//图片预加载方法
function preLoadImg(pars){
    for(let i=0;i<arr.length;i++){
        imgs[i] = new Image();
        imgs[i].src = arr[i];
    }
}
```

预加载其实是声明式的fetch，强制浏览器请求资源，并且不会阻塞onload事件，可以试用以下代码开启预加载。

`<link rel="preload" href="http://example.com"></link>`

预加载可以一定程度上降低首屏的加载时间，因为可以将一些不影响首屏但重要的文件延后加载，唯一缺点就是兼容性不好。

### 67、MVC和MVVM的区别

#### MVC

优点:

- 易懂: 简单易懂
- 层次分明: 共三个部分，各自完成各自的内容，在有Controller将大家协调在一起。

弊端:

- 量级重 : `ViewController`处理过多的业务逻辑如协调模型和视图之间的所有交互，导致量级重，维护成本很高。
- 过轻的`Model`对象:在实践中往往大家都把Model的量级设计的非常轻，总容易当做数据模型来对待。

#### MVVM

优点:

- 低耦合: `View`可以独立于Model变化和修改，一个`ViewModel`可以绑定到不同的View 上。
- 可重用性: 可以把一些视图逻辑放在一个`ViewModel`里面，让很多`View`重用这段视图逻辑。

弊端:

- 数据绑定后使得`Bug`很难被调试。
- 数据绑定和数据转化需要`花费更多`的内存成本。

#### 二者之间的关系图

MVVM实质上是把 MVC 中的C的功能给拆分了。

![MVC和MVVM](C:\Users\csm\Desktop\博客\picture\MVC和MVVM.png)

### 68、[原生javascript和jQuery操作DOM的对比总结](https://www.cnblogs.com/jiangyuzhen/p/10978611.html)

### 69、事件轮询（event-loop）

事件轮询是JS实现异步的具体解决方案。

轮询过程：

1、同步代码直接执行

2、异步函数先放在异步队列中

3、待同步函数执行完毕，轮询执行异步队列的函数

不同的任务源会被分配到不同的task队列中，任务源可以分为微任务（microtask）和宏任务（macrotask）。在ES6规范中，microtask称为jobs，macrotask称为task。

```js
console.log('script start');

setTimeout(function() {
    console.log('setTimeout');
}, 0);

new Promise((resolve) => {
    console.log('Promise');
    resolve();
}).then(function() {
    console.log('promise1');
}).then(function() {
    console.log('promise2');
});

console.log('script end');

// script start => Promise => script end => promise1 => promise2 => setTimeout
```

虽然setTimeout写在Promise之前，但是Promise属于微任务而setTimeout属于宏任务。

微任务包括process.nextTick，promise，Object.observe，MutationObserver

宏任务包括script，setTimeout，setInterval，setImmediate，I/O，UI rendering

很多人有个误区，认为微任务快于宏任务，其实是错误的。因为宏任务中包括了script，浏览器会先执行一个宏任务，接下来异步代码的话就先执行微任务。

所以正确的一次Event loop顺序是这样的

1、执行同步代码，这属于宏任务

2、执行栈为空，查询是否有微任务需要执行

3、执行所有微任务

4、必要的话渲染UI

5、然后开始下一轮Event loop，执行宏任务中的异步代码

### 70、null和undefined的区别

- Undefined类型只有一个值，即undefined。当声明的变量还未被初始化时，变量的默认值为undefined。
  - 变量被声明了，但没有赋值时，就等于undefined。
  - 调用函数时，应该提供的参数没有提供，该参数等于undefined。 
  - 对象没有赋值的属性，该属性的值为undefined。
  - 函数没有返回值时，默认返回undefined。 
- Null类型也只有一个值，即null。null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。
  - 作为函数的参数，表示该函数的参数不是对象。
  - 作为对象原型链的终点。

### 71、defer和async

延迟脚本

`<script type="text/javascript" defer="defer" src="example.js"></script>`

defer属性：表明脚本在执行时不会影响页面的构造，也就是说，脚本会被延迟到整个页面都解析完毕再运行。

异步脚本

HTML5为`<script>`定义了async属性。与defer属性相似，都用于改变处理脚本的行为。但标记为async的脚本并不会保证按照指定它们的先后顺序执行。

`<script type="text/javascript" async src="example.js"></script>`

指定async属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。为此，建议异步脚本不要在加载期间修改DOM。

异步脚本一定会在页面的load时间前执行，但可能会在DOMContentLoaded事件触发之前或之后执行。

### 72、优雅降级和渐进增强？

优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了,为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效.

渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能,向页面增加无害于基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。

### 73、内存溢出和内存泄露

#### 内存溢出

  一种程序运行出现的错误

  当程序运行需要的内存超过了剩余的内存时, 就出抛出内存溢出的错误

```js
var arrObj = {};
for(var i=0; i<100000000; i++){
	arrObj[i] = new Array(999999);
	console.log(arrObj);
}
```

#### 内存泄露

内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。

-   占用的内存没有及时释放


-   内存泄露积累多了就容易导致内存溢出


  常见的内存泄露:

1. 占用内存很大的全局变量

2. 没有及时清理的计时器/定时器

3. 闭包

```js
    // 占用内存很大的全局变量
    var num = new Array(99999999);
    var num1 = new Array(99999999);
    var num2 = new Array(99999999);
    var num3 = new Array(99999999);
    var num4 = new Array(99999999);
    var num5 = new Array(99999999);
    var num6 = new Array(99999999);
    var num7 = new Array(99999999);

    num = null;


   // 没有及时清理的计时器/定时器
    var intervalId = setInterval(function () {
        console.log("-----");
    }, 1000);

    clearInterval(intervalId);

   // 闭包
    function fn1() {
        var num  = 1111;
        function fn2() {
            num--;
            console.log(num);
        }

        return fn2;
    }

    var f = fn1();
    f();

    f = null;
```

### 74、Symbol：表示独一无二的值

- Symbol函数前不能使用new命令，否则会报错。这是因为生成的Symbol是一个原始类型的值，不是对象。
- Symbol函数可以接受一个字符串作为参数，表示对Symbol事例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。
- Symbol值不能与其他类型的值进行运算。Symbol值作为对象属性名时，不能用点运算。

### 75、随机打乱数组

```js
function randomsort(a, b) {
    return Math.random()>.5 ? -1 : 1;
    //用Math.random()函数生成0~1之间的随机数与0.5比较，返回-1或1
}
var arr = [1, 2, 3, 4, 5];
arr.sort(randomsort);

// es6 写法
arr.sort(()=>Math.random() - 0.5);
```

### 76、根据数组中对象的某一个属性值进行排序

```js
var arr = [
    {name:'zopp',age:0},
    {name:'gpp',age:18},
    {name:'yjj',age:8}
];

// 方法一
function compare(property){
    return function(a,b){
        var value1 = a[property];
        var value2 = b[property];
        return value1 - value2;
    }
}
console.log(arr.sort(compare('age')));

// 方法二
console.log(arr.sort((a,b) => a.age - b.age));
```

###  77、立即执行函数

声明一个函数，并马上调用这个匿名函数就叫做立即执行函数；也可以说立即执行函数是一种语法，让你的函数在定义以后立即执行。

立即执行函数的作用：

1. 不必为函数命名，避免了污染全局变量

2. 立即执行函数内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量

   

   例子：

```js
var foo = 1;
(function foo() {
     foo = 10; 
     console.log(foo);
}())
// ƒ foo() { foo = 10; console.log(foo) }
```

​	因为当js解释器在遇到非匿名的立即执行函数时，会创建一个辅助的特定对象，然后将函数名称作为这个对象的属性，因此函数内部才可以访问到foo，所以打印的还是这个函数，并且外部的值也没有发生更改。

### 78、防抖和节流

##### 防抖

在日常开发中，像在滚动事件中需要做个复杂计算或者实现一个按钮的防二次点击操作这些需求都可以通过函数防抖动来实现。

整体实现：

- 对于按钮防点击来说的实现：一旦我开始一个定时器，只要定时器还在，不管你怎么点击都不会执行回调函数。一旦定时器结束并设置为null，就可以再次点击了。
- 对于延时执行函数来说的实现：每次调用防抖动函数都会判断本次调用和之前的时间间隔，如果小于需要的时间间隔，就会重新创建一个定时器，并且定时器的延迟为设定时间减去之前的时间间隔。一旦时间到了，就会执行相应的回调函数。

##### 节流

防抖动和节流本质是不一样的。防抖动是将多次执行变为最后一次执行，节流是将多次执行变成每隔一段时间执行。

### 79、Proxy

Proxy是ES6中新增的功能，可以用来自定义对象中的操作。

```js
let p = new Proxy(target, handler);
// 'target'代表需要添加代理的对象
// 'handler'用来自定义对象中的操作
```

可以很方便的使用Proxy来实现一个数据绑定和监听

```js
let onWatch = (obj, setBind, getLogger) => {
    let handler = {
        get(target, property, receiver) {
            getLogger(target, property);
            return Reflect.get(target, property, receiver);
        },
        set(target, property, value, receiver) {
            setBind(value);
            return Reflect.set(target, property, value);
        }
    };
    return new Proxy(obj, handler);
};

let obj = {a: 1};
let value;
let p = onWatch(obj, (v) => {
    value = v;
}, (target, property) => {
    console.log(`Get '${property}' = ${target[property]}`);
});
p.a = 2; // bind `value` to `2`
p.a; // Get 'a' = 2
```

### 80、V8下的垃圾回收机制

转载自https://yuchengkai.cn/docs/frontend

V8将内存（堆）分为新生代和老生代两部分

#### 新生代算法

新生代中的对象一般存活时间较短，使用Scavenge GC算法。

在新生代空间中，内存空间分为两部分，分别为From空间和To空间。在这两个空间中，必定有一个空间是使用的，另一个空间是空闲的。新分配的对象就会被放入From空间中，当From空间被占满时，新生代GC就会启动了。算法会检查From空间中存活的对象并复制到To空间中，如果有失活的对象就会销毁。当复制完成后将From空间和To空间互换，这样GC就结束了。

#### 老生代算法

老生代中的对象一般存活时间较长且数量也多，使用了两个算法，分别是标记清除算法和标记压缩算法。

什么情况下对象会出现在老生代空间中：

- 新生代的对象是否已经经历过一次Scavenge算法，如果经历过得话，会将对象从新生代空间移到老生代空间中
- To空间的对象占比大小超过25%。在这种情况下，为了不影响到内存分配，会将对象从新生代空间移到老生代空间中

老生代中的空间很复杂。

在老生代中，以下情况会先启动标记清除算法：

- 某一个空间没有分块的时候
- 空间中被对象超过一定限制
- 空间不能保证新生代中的对象移动到老生代中

清除对象后会造成堆内存出现碎片的情况，当碎片超过一定限制后会启动压缩算法。在压缩过程中，将活的对象向一端移动，直到所有对象都移动完成然后清理掉不需要的内存。

### 81、   &&和||

短路原理

1、只要“&&”前面是false，无论“&&”后面是true还是false，结果都将返“&&”前面的值;

2、只要“&&”前面是true，无论“&&”后面是true还是false，结果都将返“&&”后面的值;


1、只要“||”前面为false,不管“||”后面是true还是false，都返回“||”后面的值。

2、只要“||”前面为true,不管“||”后面是true还是false，都返回“||”前面的值。

### 82、in、hasOwnProperty、isPrototypeOf和Object.getPrototypeOf()

#### 1、in

**判断一个对象是否拥有这个属性。如果对象上没有，就去它的原型对象里面找**

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.address = '杭州';
var p = new Person('csm', 21);
console.log('name', p);			// true  注意：这里name要加引号表示字符串，不然就是全局变量了
console.log('address', p);		// true
```

#### 2、hasOwnProperty

**判断当前对象是否拥有这个属性，只到对象自身查找**

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.address = '杭州';
var p = new Person('csm', 21);
console.log('name', p);			// true
console.log('address', p);		// false
```

#### 3、isPrototypeOf

**判断一个对象是否是某个实例的原型对象**

```js
function Dog(name, age) {
    this.name = name;
    this.age = age;
}
function Person(name, age) {
    this.name = name;
    this.age = age;
}
var p = new Person('csm', 21);
// 判断p的原型指针是否指向传入构造函数的原型对象，这个过程会往上层层判断。
console.log(Person.prototype.isPrototypeOf(p));		// true
console.log(Object.prototype.isPrototypeOf(p));     // true
console.log(Dog.prototype.isPrototypeOf(p));		// false
```

#### 4、Object.getPrototypeOf()

方法返回对象`__proto__`指向的prototype 

```js
console.log(Object.getPrototypeOf(Object.prototype)); //null  此处表明 Object.prototype 的原型对象是 null
```

### 83、删除对象

delete 删除对象中的属性；删除没有使用var关键字声明的全局变量

注意：

1、返回值：布尔类型的值（通过该值判断是否删除成功）

2、使用var关键字声明的变量无法被删除

3、删除对象中不存在的属性没有任何变化，但是返回值为true

4、不能删除window下面的全局变量（使用var声明）但可以删除定义在window上面的属性

### 84、创建对象的方式

1、字面量的方式创建对象

```js
var p1 = {
    name: '张三',
    run: function() {
        console.log(this.name + '跑')
    }
}
```

2、内置构造函数的方法

```js
var p1 = new Object()
p1.name = '张三'
p1.run = function() {
    console.log(this.name + '跑')
}
```

问题：使用内置构造函数的方式和字面量的方式来创建对象差不多但都存在以下问题

​	1、创建的对象无法复用，复用性差

​	2、如果需要创建多个同类型的对象，需要书写大量重复的代码，代码冗余度高

3、简单工厂函数方式

问题：无法判定类型

```js
class Product {
    constructor(name) {
        this.name = name
    }
    init() {
        alert('init')
    }
}
class Creator {
    ctreate(name) {
        return new Product(name)
    }
}
let creator = new Creator()
let p = creator.create('p1')
p.init()
```

4、自定义构造函数的方式来创建对象

- 自定义构造函数和工厂函数的对比

  1、函数的首字母大写（用于区别构造函数和普通函数）

  2、创建对象的过程是由new关键字实现的

  3、在构造函数内部会自动的创建新对象，并赋给this指针

  4、自动返回创建出来的对象

  - 构造函数的执行过程

    ```js
    function Person(name, age, sex) {
        // 1、自动创建一个空对象，把这个对象的地址 this => 新对象
        // var this = new Object()
        // 2、this给空对象绑定属性和行为
        this.name = name
        this.age = age
        this.sex = sex
        // 3、返回this
        // return this
    }
    var p = new Person()
    ```

  - 构造函数的返回值说明

    1、如果在构造函数中没有显示的return，则默认返回的是新创建出来的对象

    2、如果在构造函数中显示的return对象，则依照具体的情况处理

    ​	1>return的是对象，则直接返回这个对象，取而代之本该默认返回的新对象

    ​	2>return的是null或基本数据类型值，则返回新创建的对象

### 85、形参和arguments

该参数是一个类似于数组的结构（可以像数组一样遍历，还可以使用下标来访问数据），但是并不是数组。

1、函数调用的时候，会把实参的值赋给形参，而且会使用arguments来接收实参

2、如果实参的个数超过形参的个数，那么可以通过arguments来获取超出的数据

3、如果实参的个数小于形参的个数，那么不足的全部设置为undefined

两者之间是关联的关系

函数名.length => 形参的长度（个数）

### 86、变量的解构赋值

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

#### (1)数组的解构赋值

**基本用法**

在没有ES6之前给变量赋值经常是指定赋值

```js
var x = 33;
var y = 44;
var z = 55
```

在ES6中允许使用以下方式赋值

```js
var [x,y,z] = [33,44,55]
```

如果解构不成功，变量的值就是undefined，如下：

```js
var [a] = [];//a就是undefined;
var [a ,b] =[1]//同样a的值是1，b 的值就是undefiend;
```

以上的两个例子都是属于不完全解构，但可以成功。

<strong> 如果等号右边的不是数组，严格的来说就是不可以遍历的结构，解构赋值的过程中都会报错。</strong>

```js
//以下都是会报错的Example
var [a] = 1;
let [a] = false;
let [a] = NaN;
let [a] = undefined;
let [a] = null;
let [a] = {};
```

上面的赋值会报错的主要原因是，前五个表达式在转化为对象后不具备(Iterator)接口，（最后一个表达式）要么本身就不具备(Iterator)接口。

遍历器（Iterator）是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

#### (2) 对象的解构赋值

```js
let {name,age} = {name:"aaa",age:12}
name//"aaa"
age//12;
```

对象与数组的解构赋值有个本质的不同，数组的元素是按照次序排列的，对象中的属性排列是没有次序的，要想赋上值就必须保证，属性名必须保持一致才能获取的到值。

```js
let {age,name} = {name:"aaa",age:12}
name//"aaa"
age//12;
let{foo} ={name:"aaa",age:12}
foo//undefined 
```

上面的这个例子表示等号左边的两个变量的次序，与等号右边两个同名属性的次序不一致，但是对取值完全没有影响。第二个例子的变量没有对应的同名属性，导致取不到值，最后等于undefined。

#### (3)字符串的解构赋值

字符串也是可以解构赋值的这是因为，字符串在被解构赋值的时候就形成了一个类似数组的对象。

```js
let [a,b,c,d,e,f]="goudan"
a//g
b//o
...
f//n
```

类似数组的对象都有 一个length属性，也可以给length赋值

```js
let {length:len}="goudan"
len//6
```

### 87、扩展运算符的应用

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

1、将一个数组变为参数序列

```js
function add(a,b){
    return a+b;
}
let num = [22,33];
add(...num)//55
```

2、可以替代函数中的apply

由于扩展运算符可以展开数组，所以不需要apply方法，将数组转化为函数的参数了。

```js
//ES5中
Math.max.apply(null,[3,2,5])
//在es6中的写法
Math.max(...[3,2,5])
等同于Math.max(3,2,5);
```

由于 JavaScript 不提供求数组最大元素的函数，所以只能套用Math.max函数，将数组转为一个参数序列，然后求最大值。有了扩展运算符以后，就可以直接用Math.max了。

3、扩展运算符也可以复制对象

作用是用于取出对象中所有可以遍历的属性，拷贝到当前对象中，是浅拷贝

```js
var obj = {name:"feng",color:["yellow","blue"]};
var obj1 ={...obj}
obj1.color.push("red")
console.log(obj)//{ name: 'feng', color: [ 'yellow', 'blue', 'red' ] }
```

4、将某些数据类型转化为数组

```js
//arguments对象
!function(){
    const arr = [...arguments];
    console.log(arr)
}(2,3)//[2,3]
//Dom返回的对象
console.log(Array.isArray([...document.getElementsByTagName("li")]))//true
```

扩展运算符所使用的是遍历器接口（Iterator），如果一个对象没有这个接口，就无法转化。

### 88、Array.of

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

Array.of主要是用于将一组值转化为数组

Array.of的出现主要是对Array创建数组的不足进行的补充，因为用Array创建数组，因为参数个数的不同，会造成差异。
如下：

```js
Array()//[]
Array(3)//[,,,]
Array(1,2,3)//[1,2,3]
//当Array()中的参数只有一个的时候，此时的参数就代表了数组的长度，只有参数大于等于2的时候才会返回，参数组成的新数组。
//Array.of
console.log(Array.of())//[]
console.log(Array.of(3))//[3]
console.log(Array.of(3).length)//1
//而Array无论参数有几个最后都会返参数组成的数组。
```

Array.of功能的模拟实现如下

```js
function arrayof{
    return Array.slice.call(arguments);
}
```

### 89、对象中属性的遍历

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

在ES6中共有5种方法实现对对象属性的遍历
这五种遍历方法都遵循同样的遍历次序规则：
首先遍历所有数值键，按照数值升序排列。
其次遍历所有字符串键，按照加入时间升序排列。
最后遍历所有 Symbol 键，按照加入时间升序排列。

#### (1). for...in

> for...in 是用来遍历自身属性，和继承的可以枚举的属性。

```js
var obj = {name:"feng",age:12}
obj.__proto__.sex="nan"
obj[Symbol()]="bol";
for(var item in obj){
    console.log(item);//name,age,sex
}
```

#### (2).Reflect.ownKeys(obj)

> Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

```js
console.log(Reflect.ownKeys(obj));//[ 'name', 'age', Symbol() ]
```

#### (3).Object.keys(obj)

> Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。
>
> ```js
> console.log(Object.keys(obj));//[ 'name', 'age' ]
> ```

#### (4).Object.getOwnPropertyNames(obj)

> Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。
>
> ```js
> console.log(Object.getOwnPropertyNames(obj));//[ 'name', 'age' ]
> ```

#### (5).Object.getOwnPropertySymbols(obj)

> Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

```js
console.log(Object.getOwnPropertySymbols(obj));//[ Symbol() ]
```

### 90、ES6中set 和 map两种数据结构（集合）

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

#### 1.set的基本用法

set和数据相似，也是一种 集合，主要的区别是，set里面的值是唯一的，没有重复的。set中可以放数组，不可以放对象，使用add向里面填充数据,可以使用delete删除其中的一个元素 ，创建set如下：

```js
let coll = new Set([3,5,"feng","true"]);//放数组
console.log(coll) // Set(4) {3, 5, "feng", "true"}
coll.add(22)
console.log(coll) // Set(5) {3, 5, "feng", "true", 22}
coll.delete(3)
console.log(coll) // Set(4) {5, "feng", "true", 22}
```

set不是数组，是一个像对象的数组，就是一个伪数组。Set中的数据可以用for of 以及 foreach来进行遍历。

```js
coll.forEach(item =>console.log(item));//3 5 feng true
for(let item of coll){console.log(item);}//3 5 feng true
```

可以使用set来实现数组去重

```js
let coll = [1,1,12,3,3,true,true,NaN,NaN]
let coll1 = [...(new Set(coll))]
console.log(coll1)//[ 1, 12, 3, true, NaN ]
```

#### 2.map的基本用法

它类似于对象，里面存放也是键值对，区别在于：对象中的键名只能是字符串，如果使用map，它里面的键可以是任意值。
Map的创建和用法如下

```js
var m = new Map();
o = {p: "Hello World"};
console.log(m.get(o))
// "content"
```

Map中的实例属性主要有

**size**：返回成员总数。

**set(key, value)**：设置key所对应的键值，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键。

**get(key)**：读取key对应的键值，如果找不到key，返回undefined。

**has(key)**：返回一个布尔值，表示某个键是否在Map数据结构中。

**delete(key)**：删除某个键，返回true。如果删除失败，返回false。

**clear()**：清除所有成员，没有返回值。

**set()**：方法返回的是Map本身，因此可以采用链式写法。

<strong>主要看下Map的遍历方法</strong>

keys()：返回键名的遍历器。

values()：返回键值的遍历器。

entries()：返回所有成员的遍历器。

```js
let map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  document.write(key);
}
// "F"
// "T"
for (let value of map.values()) {
  document.write(value);
}
// "no"
// "yes"
for (let item of map.entries()) {
  document.write(item[0], item[1]);
}
// "F" "no"
// "T" "yes"
// 或者
for (let [key, value] of map.entries()) {
  document.write(key, value);
}
// 等同于使用map.entries()
for (let [key, value] of map) {
  document.write(key, value);
}
```

### 91、ES6中字符串的扩展

转自[ES6核心，教你 玩转 ES6新特性](http://www.imooc.com/article/67156)

#### 1.includes(),startsWith(),endsWith()

在ES6之前，js中只有indexof方法，来确定一个字符串中是否包含在另一个字符串中。

ES6中又提供了三种新的方法。

- includes()：返回布尔值，表示是否找到了参数字符串。

- startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。

- endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
let str = 'hello My word!'
console.log(str.startsWith("hello"));//true
console.log(str.endsWith('!'));//true
console.log(str.includes('My'));//true
```

#### 2.padStart(),padEnd()

ES6引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。padStart()用于头部补全，padEnd()用于尾部补全。

```js
console.log('foo'.padStart(4,'a'));//afoo
console.log('foo'.padEnd(4,'a'));//fooa

console.log('foo'.padStart(3,'a'));//foo
console.log('foo'.padEnd(3,'a'));//foo
```

padstart最常见的用途

1.是用来补全在指定的位数。2.是用来提示字符串格式：

```js
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

### 92、JavaScript语言特性
1、运行在客户端浏览器上；

2、脚本语言、解释性语言，不用预编译，直接解析执行代码；

3、是弱类型语言，较为灵活；

4、与操作系统无关，跨平台的语言；

5、基于对象，是一种基于对象的脚本语言,它不仅可以创建对象,也能使用现有的对象。



