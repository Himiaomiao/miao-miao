# javascript知识记录

## 1、常用代码调式函数

>1. `console.log()`
>
>  这个方法主要用于将传给它的值输出到控制台。可以给log()传递任何类型：可以是字符串、数组、对象、布尔值。
>
> 2. `console.error()`
>
>  这个方法在测试代码时非常有用。它用于将错误输出到浏览器控制台。错误消息默认用红色突出显示。
>
> 3. `console.warn()`
>
>   这个方法用于向控制台抛出警告，警告消息默认黄色突出显示。
>
> 4. `console.clear()`
>
>   这个函数用来清除控制台，如果控制台中充满了消息和错误信息，可以用它清除控制台，并在控制台中显示一条消息。
>
> 5. `console.time()`与`console.timeEnd()`
>
>  这种方法要相互结合使用，每当我们想知道一个代码块或函数所花费的时间时，都可以用`time()`和`timeEnd()`方法。这两个函数都以字符串作为参数。使用时要对这两个函数用相同的字符串来测量时间。
>
> 6. `console.table()`
>
>  这个方法可以在控制台生成一个表格，能够提高可读性。它可以自动为数组或对象生成一个表。
>
> 7. `console.count()`
>
>  可以在循环中用它来检查特定的值使用了多少次。
>
> 8. `console.group()`和`console.groupEnd()`
>
>  `group()`和`groupEnd()`可以让我们把内容分组到一个单独的块中。就像`time()`和`timeEnd()`一样，它们需要以相同值的标签作为参数。你还可以对组执行展开或折叠操作。
>
> 9. 为你的日志添加样式
>
>  还可以在控制台日志添加样式，使日志看起来更漂亮。只需要把css样式作为`log()`函数的第二个参数，同时第一个参数以`%c`开始即可。

## 2、几种常见事件的方法

>**preventDefault()   取消事件默认行为，****如阻止点击提交按钮时对表单的提交****（本题中click并没有什么默认行为）**
>
>  **stopImmediatePropagation()  取消事件冒泡同时阻止当前节点上的事件处理程序被调用，影响当前的事件\**\***
>
>**stopPropagation()  取消事件冒泡，不影响事件\**\***
>
>**cancelBubbe()   取消事件冒泡**
>
>**returnValue()    取消事件默认行为**

## 3、javascript数据类型

 >1. 原始数据类型（primitive type）
 >
 > 字符串(String)、数字(Number)、布尔(Boolean)、对空(Null)、未定义(Undefined)、symbol(符号）
 >
 >2. 引用数据类型（object type）
 >
 >  数组(array)、对象(object)、函数(function)、date、RegExp
 >
 >原始值采用栈内存中，数据是永久保存，不可更改
 >
 >引用数据类型数据的值存在堆内存中，栈内存中存的是堆内存中的地址

## 4、toString()函数--将数字转化为字符串

>语法：number.toString(radix)
>
>参数值：radix为可选参数，规定表示数字的基数，是2~36之间的整数，若该参数省略，则默认使用基数10。
>
>          * 2 - 数字以二进制形式表现
>          * 8 - 数字以八进制形式表现
>          * 16 - 数字以十六进制形式表现
>
>返回值：String(字符串)

## 5、parseInt()函数--解析一个字符串，返回一个整数

>语法：parseInt(string,radix)
>
>参数值：string:必需参数，需要解析的字符串
>
>  			radix:可选参数，表示要解析的数字的基数，为于2~36之间
>
>返回值：返回解析后的数字

## 6、indexOf()函数--检索字符串首次出现的位置

>语法：stringObject.indexOf(searchvalue,fromindex)
>
>参数值：seaechvalue:必需，规定需要检索的字符串的值
>
>​			fromindex:可选整数，规定在字符串中开始检索的位置。它的合法取值是0~stringObject.length-1。如果省略则从首字符开始。
>
>返回值：字符串首次出现的位置或者-1，当需要检索的字符不存在时返回-1.
>
>注释：indexOf()对大小写敏感

## 7、call()函数--可以编写使用在不同对象上的方法

>+ javascript call()方法
>
>第一个参数表示函数体内this的指向
>
>`call()` 方法是预定义的javascript方法，它可以用来调用所有者对象作为参数的方法。通过`call()`能够使用属于另一个对象的方法。本例调用 person 的 fullName 方法，并用于 person1：
>
>例子：
>
>```javascript
>var person = {
>    fullName: function() {
>        return this.firstName + " " + this.lastName;
>    }
>}
>var person1 = {
>    firstName:"Bill",
>    lastName: "Gates",
>}
>var person2 = {
>    firstName:"Steve",
>    lastName: "Jobs",
>}
>person.fullName.call(person1);  // 将返回 "Bill Gates"
>```
>
>+ 带参数的call()方法
>
>call() 方法可接受参数：
>
>实例：
>
>```javascript
>var person = {
>  fullName: function(city, country) {
>    return this.firstName + " " + this.lastName + "," + city + "," + country;
>  }
>}
>var person1 = {
>  firstName:"Bill",
>  lastName: "Gates"
>}
>person.fullName.call(person1, "Seattle", "USA");
>```
>
>

## 8、apply()函数--可以编写使用在不同对象上的方法

>+ javascript apply()方法
>
>第一个参数表示函数体内this的指向
>
>在本例中，person 的 fullName 方法被*应用*到 person1：
>
>例子：
>
>```javascript
>var person = {
>    fullName: function() {
>        return this.firstName + " " + this.lastName;
>    }
>}
>var person1 = {
>    firstName: "Bill",
>    lastName: "Gates",
>}
>person.fullName.apply(person1);  // 将返回 "Bill Gates"
>```
>
>+ 带参数的apply()方法
>
>`apply()`函数中接受参数
>
>例子：参数以数组的形式传入
>
>```javascript
>var person = {
>  fullName: function(city, country) {
>    return this.firstName + " " + this.lastName + "," + city + "," + country;
>  }
>}
>var person1 = {
>  firstName:"John",
>  lastName: "Doe"
>}
>person.fullName.apply(person1, ["Oslo", "Norway"]);
>```

## 9、apply()和call的区别

>+ `call()` 方法分别接受参数。
>+ `apply() `方法接受数组形式的参数。
>+ 如果要使用数组而不是参数列表，则 apply() 方法非常方便。

## 10、prototype 属性--用于向对象中添加属性和方法

>语法：object.prototype.name=value
>
>实例：在本例中，我们将展示如何使用 prototype 属性来向对象添加属性
>
>```javascript
><script type="text/javascript">
>
>function employee(name,job,born)
>{
>this.name=name;
>this.job=job;
>this.born=born;
>}
>
>var bill=new employee("Bill Gates","Engineer",1985);
>
>employee.prototype.salary=null;
>bill.salary=20000;
>
>document.write(bill.salary);
>
></script>
>```
>
>

## 11、创建Array的语法

>+ var arr = [1,2,3]
>+ var arr = new Array(1,2,3)
>+ var arr = new Array(12) //代表只有一个元素12
>+ var arr = new Array(0) //清空数组

## 12、undefined和null是否相等问题

>+ (undefined==null),值为true,`==`是判断值是否相等，undefined和null值相等，因此结果为true
>+ (undefined===null),值为false,`===`是判断值是否相同的同时还判断类型是否相同，undefined的类型为undefined,null的值为object,因此值不同为false

## 13、正则表达式

>+ `?`出现0次或1次.[0,1]
>+ \* 出现0次或多次.  [0,+∞]
>+ `+`出现1次或多次  [1,+∞]

## 14、Array对象方法

>| 方法             | 描述                                                         |
>| ---------------- | ------------------------------------------------------------ |
>| concat()         | 连接两个数组或更多的数组，并返回结果                         |
>| join()           | 把数组的所有元素放入一个字符串，元素通过指定的分割符进行分割 |
>| pop()            | 删除并返回数组的最后一个元素                                 |
>| push()           | 向数组的末尾添加一个或更多元素，并返回新的长度               |
>| reverse()        | 颠倒数组中元素的顺序                                         |
>| shift()          | 删除并返回数组的第一个元素                                   |
>| slice()          | 从某个已有的数组返回选定的元素                               |
>| sort()           | 对数组元素进行排序                                           |
>| splice()         | 删除元素，并向数组添加新元素                                 |
>| toSource()       | 返回该对象的源代码                                           |
>| toString()       | 把数组转化为字符串，并返回结果                               |
>| toLocaleString() | 把数组转化为本地数组，并返回结果                             |
>| unshift()        | 向数组的开头添加一个或更多的元素，并返回新的长度             |
>| valueOf()        | 返回数组对象的原始值                                         |
>| indexOf()        | 返回数组中指定项的下标，从0开始算，不存在的返回-1            |

## 15、ES6 Generator 函数

>+ Generator函数的组成:
>
>  Generator函数有两个区分于普通函数的部分
>
>      - 一是在function后面函数名之前有个`*`
>      - 函数内部有yield表达式
>      - 执行该函数会返回一个Generator对像
>
> 其中 * 用来表示函数为 Generator 函数，yield 用来定义函数内部的状态。
>
> ```javascript
> function* func(){
>  console.log("one");
>  yield '1';
>  console.log("two");
>  yield '2'; 
>  console.log("three");
>  return '3';
> }
> ```
>
>+ 执行机制
>
>  调用 Generator 函数和调用普通函数一样，在函数名后面加上()即可，但是 Generator 函数不会像普通函数一样立即执行，而是返回一个指向内部状态对象的指针，所以要调用遍历器对象Iterator 的 next 方法，指针就会从函数头部或者上一次停下来的地方开始执行。
>
> ```javascript
> f.next();
> // one
> // {value: "1", done: false}
>
> f.next();
> // two
> // {value: "2", done: false}
>
> f.next();
> // three
> // {value: "3", done: true}
>
> f.next();
> // {value: undefined, done: true}
> ```
>
>第一次调用 next 方法时，从 Generator 函数的头部开始执行，先是打印了 one ,执行到 yield 就停下来，并将yield 后边表达式的值 '1'，作为返回对象的 value 属性值，此时函数还没有执行完， 返回对象的 done 属性值是 false。
>
>第二次调用 next 方法时，同上步 。
>
>第三次调用 next 方法时，先是打印了 three ，然后执行了函数的返回操作，并将 return 后面的表达式的值，作为返回对象的 value 属性值，此时函数已经结束，多以 done 属性值为true 。
>
>第四次调用 next 方法时， 此时函数已经执行完了，所以返回 value 属性值是 undefined ，done 属性值是 true 。如果执行第三步时，没有 return 语句的话，就直接返回 {value: undefined, done: true}。
>
>+ yield表达式
>
>  由于 Generator 函数返回的遍历器对象，只有调用`next`方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。`yield`表达式就是暂停标志。

## 16、hasOwnProperty属性--判断是否存在属性或者对象

>**hasOwnProperty：** 是用来判断一个对象是否有你给出名称的属性或对象。不过需要注意的是，此方法无法检查该对象的原型链中是否具有该属性，该属性必须是对象本身的一个成员。

## 17、**isPrototypeOf** 属性--判断原型链上是否存在属性或对象

>**isPrototypeOf :** 是用来判断要检查其原型链的对象是否存在于指定对象实例中，是则返回true，否则返回false。

## 18、iframe

>+ 什么是iframe
>
>  iframe 用于在页面内显示页面，使用 <iframe> 会创建包含另外一个文档的内联框架（即行内框架）
>
>  ```
>  <iframe src="URL"></iframe>
>  ```
>
>+ 相关知识点：
>
>  [深入理解iframe](https://www.cnblogs.com/Leophen/p/11403800.html)

## 19、javascript同名函数问题及函数声明提升

>+ 函数声明提升：
>
>   函数声明提升，浏览器在解析的时候会首先对声明函数优先解析，记住是声明函数不是匿名函数，因此调用函数可以在函数声明之前。
>
>+ 同名函数：
>
>   js中函数没有重载，简单的说没有重载就是每个函数的函数名只是指向函数的指针，因此再次命名相同的函数名时，就相当于改变了指针内的内容，看起来就像是后一个把前一个函数覆盖。
>
>+ *优先级为：**变量声明(foo#1) < 函数声明(foo#2) < 变量赋值(foo#3)***

## 20、NOSCRIPT标签

>NOSCRIPT标签用来定义在脚本未被执行时的替代内容。也可以用在检测浏览器是否支持脚本，若不支持脚本则可以显示NOSCRIPT标签里的innerText
>
>noscript:用以在不支持js的浏览器中显示替代的内容，这个元素可以包含能够出现在文档<body>中任何html元素，script元素除外。包含在noscript元素的内容只有在下列情况下才会显示出来
>    1.浏览器不支持脚本
>    2.浏览器支持脚本，但脚本被禁用

## 21、node节点常用的几个属性

>+ firstChild
>+ lastChild
>+ nextSibling：下一个兄弟节点
>+ previousSibling：前一个兄弟节点
>
>这些都是属性，都不需要添加括号的。

## 22、touch事件

>touchstart:   //手指放到屏幕上时触发
>
>touchmove:    //手指在屏幕上滑动式触发
>
>touchend:   //手指离开屏幕时触发
>
>touchcancel:   //系统取消touch事件的时候触发，这个好像比较少用

## 23、js中的循环

>1. `for`循环
>
>   ```javascript
>   let arr = [1,2,3];
>   for (let i=0; i<arr.length; i++){
>    console.log(i,arr[i])
>   }
>   // 0 1
>   // 1 2
>   // 2 3
>   ```
>
>   for循环是常用循环，通常用于遍历数组
>
>2. `for in`循环
>
>   ```javascript
>   let obj = {name:'zhou',age:'**'}
>   for(let i in obj){
>    console.log(i,obj[i])
>   }
>   // name zhou
>   // age **
>   ```
>
>   for in 循环主要用于遍历普通对象，i 代表对象的 key 值，obj[i] 代表对应的 value,当用它来遍历数组时候，多数情况下也能达到同样的效果，但是你不要这么做，这是有风险的，因为 i 输出为字符串形式，而不是数组需要的数字下标，这意味着在某些情况下，会发生字符串运算，导致数据错误，比如：'52'+1 = '521' 而不是我们需要的 53。
>
>   另外 for in 循环的时候，不仅遍历自身的属性，还会找到 prototype 上去，所以最好在循环体内加一个判断，就用 obj[i].hasOwnProperty(i)，这样就避免遍历出太多不需要的属性。
>
>3. `while`循环
>
>   ```javascript
>   cars=["BMW","Volvo","Saab","Ford"];
>   var i=0;
>   while (cars[i])
>   {
>   console.log(cars[i] + "<br>")
>   i++;
>   };
>   // BMW
>   // Volvo
>   // Saab
>   // Ford
>   ```
>
>   while与for循环事实上它们底层的处理是一样的，不过 for 循环可以把定义、条件判断、自增自减操作放到一个条件里执行，代码看起来方便一些，仅此而已。
>
>4. `do while`循环
>
>   ```javascript
>   let i = 3;
>   do{
>    console.log(i)
>    i--;
>   }
>   while(i>0)
>   // 3
>   // 2
>   // 1
>   ```
>
>   do while 循环是 while 循环的一个变体，它首先执行一次操作，然后才进行条件判断，是 true 的话再继续执行操作，是 false 的话循环结束。
>
>5. `Array forEach`循环
>
>   ```javascript
>   let arr = [1,2,3];
>   arr.forEach(function(i,index){
>    console.log(i,index)
>   })
>   // 1 0
>   // 2 1
>   // 3 2
>   ```
>
>   forEach循环，循环数组中每一个元素并采取操作， **没有返回值**， 可以不用知道数组长度,他有三个参数，只有第一个是必需的，代表当前下标下的 value。
>
>   另外请注意，forEach 循环**在所有元素调用完毕之前是不能停止的**，它没有 break 语句，如果你必须要停止，可以尝试 try catch 语句，就是在要强制退出的时候，抛出一个 error 给 catch 捕捉到，然后在 catch 里面 return，这样就能中止循环了，如果你经常用这个方法，最好自定义一个这样的 forEach 函数在你的库里。
>
>6. `Array map()`方法
>
>   ```javascript
>   let arr = [1,2,3];
>   let tt = arr.map(function(i){
>    console.log(i)
>    return i*2;
>   })
>   // [2,4,6]
>   ```
>
>   map() 方法**返回一个新数组**，数组中的元素为原始数组元素调用函数处理后的值。
>   注意：**map 和 forEach 方法都是只能用来遍历数组，不能用来遍历普通对象**。
>
>7. `Array filter()`方法
>
>   ```javascript
>   let arr = [1,2,3];
>   let tt = arr.filter(function(i){
>       //过滤条件，返回数组中大于1的新数组
>    return i>1;
>   })
>   // [2,3]
>   ```
>
>   filter 方法是 Array 对象内置方法，**它会返回通过过滤的元素**，不改变原来的数组。
>
>8. `Array some()`方法
>
>   ```javascript
>   let arr = [1,2,3];
>   let tt = arr.some(function(i){
>       //检测数组中是否存在大于1的元素
>    return i>1;
>   })
>   // true
>   ```
>
>   some() 方法用于检测数组中的元素是否存在满足指定条件（函数提供）,返回 boolean 值，存在满足条件的数值返回true,不存在返回false,不改变原数组。
>
>9. `Array every()`方法
>
>   ```javascript
>   let arr = [1,2,3];
>   let tt = arr.some(function(i){
>    return i>1;
>   })
>   // 检测数组中元素是否都大于1
>   // false
>   ```
>
>   every() 方法用于检测数组**所有元素**是否都符合指定条件（通过函数提供），返回 boolean 值，所有元素都符合条件返回true,存在不符合条件的返回false,不改变原数组。
>
>10. `Array reduce()`方法
>
>    ```javascript
>    let arr = [1,2,3];
>    let ad = arr.reduce(function(i,j){
>     return i+j;
>    })
>    // 6
>    ```
>
>    reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
>
>11. `Array reduceRight()`方法
>
>    ```javascript
>    let arr = [1,2,3];
>    let ad = arr.reduceRight(function(i,j){
>     return i+j;
>    })
>    // 6
>    ```
>
>    reduceRight()方法,和 reduce() 功能是一样的，它是从数组的末尾处向前开始计算。
>
>12. `for of`循环
>
>    ```javascript
>    let arr = ['name','age'];
>    for(let i of arr){
>     console.log(i)
>    }
>    // name
>    // age
>    ```
>
>    for of 循环是 Es6 中新增的语句，用来替代 for in 和 forEach，它允许你遍历 Arrays（数组）, Strings（字符串）, Maps（映射）, Sets（集合）等可迭代(Iterable data)的数据结构,注意它的兼容性。

## 24、5大主流浏览器

>| 浏览器名称 | 内核         |
>| ---------- | ------------ |
>| IE         | trident      |
>| chrome     | webkit blink |
>| safari     | webkit       |
>| firefox    | gecko        |
>| opera      | presto       |

## 25、javascript变量

>命名规范
>
>+ 不能以数字开头
>+ 能用字母_$开头
>+ 字母_$数字
>+ 关键字、保留字
>+ 语义化、结构化
>+ 小驼峰命名法

## 26、运算符

>1、括号运算>普通运算>赋值
>
>2、`+`运算符
>
>	+ 数学运算
>	+ 字符串拼接，任何数据类型的值加上字符串结果都是字符串
>
>3、除法
>
>+ `0/0`结果为NaN(NaN->Not a Number)及不是数据
>+ `1/0`结果为infinity，为数字类型
>
>4、取余
>
>5、交换值问题
>
>```javascript
>var a = 1,b = 2;
>//交换a和b的值
>a = a + b;//a = 3
>b = a - b;//3 - 2 =1
>a = a - b;// 3 - 1 =2
>```
>
>6、`++`和`--`
>
>7、比较运算符
>
>+ number与number比较直接进行数字大小比较
>
>+ number 遇上string ,string转化为number，再进行比较
>+ string 与string 比较则按照ASCII比较，多个字符从左到右，直到比较出结果
>+ `==`是不看数据类型的，只看数据
>+ `===`需要看数据类型是否相等
>+ `NaN`与包括自己在内的任何东西都不相等

## 27、逻辑运算符

>+ && 与运算符，&&两边都相等即可，遇到真往后走，遇到假或者走到最后就返回当前的值
>
>+ ||或者运算符，||两边有一边满足条件即可 ，遇到假就往后走，遇到真或者走到最后就返回当前的值
>
>   举例：
>
>  ```javascript
>  var name = '艾小耶';
>  console.log(name || '未找到数据')
>  a.onclik = function(e){
>  var event = e || window.event
>  }
>  ```
>
>+ `undefinde、null、NaN、0、“ ”、false`都是假值s

## 28、typeof --返回数据类型

>1、typeof可能的返回类型包括number,string,boolean,object,undefined,function
>
>```javascript
>console.log(a)//a为定义，返回undefined
>console.log(typeof({}))//返回object
>console.log(typeof([]))//返回object
>console.log(typeof(typeof(a)))//返回a数据类型的数据，结果为string
>```
>
>`把数据类型再typeof结果肯定为string`

## 29、数据类型转化

>1、显示数据类型转化
>
>+ Number()--转换为数字
>+ parseInt()--转换为整型，含有两个参数，第一个参数为需要转换的数字，第二个为基数，转换为相应的进制，第一个为非数字直接返回NaN
>+ parseFloat()--转换为小数
>+ number.toFixed()--一个参数，参数为四舍五入保留小数点后相应的位数
>+ toString()--转换为字符串，含有基数参数，可以转化指定的进制
>
>2、隐式类型转化
>
>+ ```javascript
>  var a = '123'//含有隐式类型转换Number(a)
>  a++;
>  console.log(a)//打印结果为124
>  ```
>```
>
>```
>
>```
>
>```
>
>```
>
>```
>
>```
>
>​```javascript
>
>+ ```javascript
>var a = "a" + 1;//含有隐式类型转换String(1)
>console.log(a)//打印结果为a1
>```
>```
>
>```
>
>```
>
>+ ```javascript
>var a = 1=== '1'//这个返回false,不进行数据类型转换
>```
>```
>
>```
>
>```
>
>+ ```javascript
>var a3 = undefined == null //返回true
>var a4 = undefined === null //返回false,数据类型不相同
>```
>```
>
>+ isNaN()--判断参数是不是非数字
>
>​```javascript
>console.log(isNaN('123'))//返回false,存在隐式数据类型转换，把字符串转换为数字再判断
>console.log(isNaN('a'))//返回true
>console.log(isNaN(NaN))//返回true
>console.log(isNaN(null))//返回false
>console.log(isNaN(undefined))//返回true,undefined转换为number结果为NaN
>```

## 30、函数

>1、最基本的函数写法 - 函数声明
>
>function test(参数){
>
>函数执行语句
>
>}
>
>2、表达式法,此时test1在函数外部是不可以调用的，在函数内可以调用
>
>var trest = function test1(){
>
>}
>
>3、匿名函数表达式
>
>var trest = function (){//->匿名函数
>
>}
>
>4、实参和形参
>
>```javascript
>function test(a,b){
>console.log(arguments[1])//通过arguments可以获取实参，返回数组
>console.log(test.length)//可以获取形参的长度
>}
>//函数实参和形参的个数可以不相同
>test(1,2,3)
>
>//实参求和,一个函数被调用时累加他的实参
>function sum(){
>var a = 0;
>for(var i = 0;i<arguments.length;i++){
>   a += arguments[i]
>}
>console.log(a)
>}
>sum(1,2,3,4,5,6)
>
>//在函数内部可以更改实参的值
>function test(a,b){
>a = 3;//改变实参的值
>console.log(arguments[0])//输出结果为3
>}
>test(1,2)
>
>//如果在函数内部改变未传入的实参的值，则打印结果为undefined
>function test(a,b){
>b = 3;//由于没有传入实参b的值，因此b为undefined,无法给undefined赋值
>console.log(arguments[1])//打印结果为undefined
>}
>test(1)
>```
>
>5、初始化参数——默认值(默认值为undefined,当给形参赋默认值时，形参和实参哪个不为undefined参数的值就选择那个)
>
>```javascript
>function test(a,b){
>console.log(a)
>console.log(b)
>}
>test(1)//没有给b赋值，b的值默认为undefined
>```

## 31、预编译

>1、函数声明整体提升，变量只有声明提升，赋值是不提升的
>
>2、暗示全局变量，imply global variable
>
>+ 全局变量不论声明不声明，都存在window对象中.
>
>  ```javascript
>  //声明全局变量
>  var a = 1;
>  b = 2;
>  console.log(a);
>  //以上函数在javascript中相当于
>  window = {
>  a:1,
>  b:2
>  }
>  console.log(window.a)
>  ```
>
>+ 在函数中没有声明的变量默认挂载到window对象中
>
>3、函数预编译——函数执行之前需要进行AO,即活跃对象，函数上下文，预编译做过的在函数执行时不需要再做，AO在函数执行完成后，AO是要销毁的，AO是一个即时的存储容器
>
>+ 第一步创建AO对象，寻找函数里的形参和变量声明放到对象AO中
>+ 把实参的参数值赋值给形参
>+ 寻找函数声明，赋值函数体，放到AO中，
>+ 执行函数
>
>4、全局上下文——global object
>
>+ 寻找变量
>+ 寻找函数声明
>+ 执行

## 32、闭包

>+ 当内部函数被返回到外部并保存时，一定会产生闭包，闭包会产生原来的作用域链不释放，过渡的闭包可能会导致内存泄露或者加载过慢
>
>

## 33、立即执行函数——IIFE（immediately-invoked function expression）

>1、立即执行函数特点：
>
>+ 页面加载时自动执行
>+ 执行完成之后立即销毁
>+ 打印立即执行函数会打印出undefined
>+ 有没有函数名是一样的，函数名会自动被忽略，因此写不写函数名都是一样的
>+ 用`()`括起来的为表达式，表达式中的函数名会自动被忽略
>
>2、两种写法
>
>+ ```javascript
> (function(){
> ```
> ```
>
> ```
>
>```
>
>```
>
>})();
>```
>
>+ ```javascript
> (function(){
>```
>```
>
>}());//w3c建议
>​```javascript
>
>3、案例
>
>​```javascript
>function test(){
>var arr = [];
>for(var i = 0; i < 10; i++){
>arr[i] = function(){
>document.write(i + '')
>}
>}
>return arr
>}
>var myArr = test();
>console.log(myArr)//打印出10次匿名函数
>for(var j = 0; j < 10;j++){
>myArr[j]();//形成闭包，导致打印出10个10
>}
>```
>
>```javascript
>var fn = (
>function test1(){
>   return 1;
>},
>function test2(){
>   return '2';
>}   
>)();
>console.log(typeof(fn))//返回字符串‘2’，打印结果为string
>
>var a = 10;
>if(function b(){}){//if语句中是一个函数，所以结果不是false,因此会执行if选择语句中的内容
>a += typeof(b);//if语句中(function b(){})为一个表达式，表达式中的函数名会被忽略，因此不存在b，所以打印结果为undefined
>}
>console.log(a)
>```
>
>

## 34、逗号运算符

>+ 逗号运算符只返回最后一个逗号后面的数值

## 35、对象构造函数

>1、对象的常见写法
>
>```javascript
>var teacher = {
>    //对象属性
>    name:'张三',
>    age:32,
>    sex:'male',
>    height:176,
>    weight:130,
>    //对象方法
>    teach:function(){
>        console.log('I am teaching JavaScript');
>    },
>    eat:function(){
>        this.weight++;//this代表对象本身
>        console.log('I am having a dinner');
>    }
>}
>//通过一下方法可以增加对象属性和方法
>teacher.address = '北京';
>teacher.drink = function(){
>    console.log('I am frinking beer')
>}
>//修改对象的方法
>teacher.height = 180;
>teacher.teach = function(){
>    console.log('I am teaching HTML')
>}
>//删除对象属性
>delete teacher.address;
>//删除对象方法
>delete teacher.teach;//注意不能写成`delete teacher.teach()`
>```
>
>2、构造函数，通过系统自带的构造函数创建对象
>
>```javascript
>var obj = new Object();
>obj.name = '张三'
>obj.sex = '男士'
>```
>
>3、自定义构造函数
>
>```javascript
>function Teacher(){
>    this.name = '张三';
>    this.sex = '男士';
>    this.smoke = function(){
>        console.log('I am smoking');
>    }
>}
>var teacher = new Teacher()//自定义构造函数当创建实例化对象时，函数中的this才存在
>```
>
>

## 36、包装类

>笔试题：
>
>```javascript
>var name = 'languiji';
>name +=10;//'languiji10'
>var type = typeof(name);//'string'
>if(type.length === 6){//true
>    type.text = 'string';//new String(type).text = 'string';delect  
>    //因为type为字符串，字符串加属性没办法保存，会自动delect
>}
>console.log(type.text)//打印undefined
>```
>
>```javascript
>function Car(brand,color){
>    this.brand = 'Benz';
>    this.color = 'red';
>}
>var car = new Car('Mazda',blank)
>console.log(car)//因为给属性赋默认值，所以打印的结果为'Benz'和'red'
>```
>
>```javascript
>function Test(a,b,c){
>    var d = 1;
>    this.a = a;
>    this.b = b;
>    this.c = c;
>    function f(){
>        d++;
>        console.log(d)
>    }
>    this.g = f
>}
>var test1 = new Test();
>test1.g();//2
>test1.g();//3
>var test2 = new Test()
>test2.g();//2
>```
>
>```javascript
>var x = 1,y = z = 0;
>function add(n){
>    return n = n + 1;
>}
>y = add(x)
>function add(n){
>    return n = n + 3
>}
>z = add(x)
>console.log(x,y,z)//1,4,4
>/*
>GO = {
>x : 1,
>y : 0,
>z ：0，
>add : function add(n){return n = n + 3}//第二次赋值把第一次赋值的覆盖
>}
>*/
>```
>

## 37、原型----prototype

>1、`prototype`是定义构造函数构造出的每个对象的公共祖先，所有被改构造函数构造出的对象都可以继承原型上的属性和方法
>
>2、构造函数中有的属性，访问时会优先访问构造函数中的属性，而不会访问原型上的祖先属性，一般公共的固定的属性值放在原型上，只有需要传参数的放在构造函数中
>
>3、通过实例化对象`delect`只能删除构造函数中的属性，不能删除原型上的属性
>
>4、`constructor`默认指向构造函数本身，可以通过原型更改构造指向
>
>5、原型链即沿着`_poto_`找原型上的属性，形成继承关系,原型链的顶端为`object.prototype`,其中`object.prototype`包含一个toString。
>
>6、谁在使用this,this就指向谁