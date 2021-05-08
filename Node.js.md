# Node.js

## 1、模块化

>+ 内置模块
>+ 第三方模块
>+ 自定义模块
>  - 创建一个模块（一个js文件一个模块）
>  - 导出一个模块（`module.exports=name`）
>  - 引用一个模块并调用

## 2、ES6语法简介

>+ 浏览器：javascript三大部分：ECMAScript+BOM+DOM
>+ 服务器：javascript = ECMAScript + 系统内置的核心模块(fs http)

## 3、var的弊端

>      - var声明变量的时候，会有预解析（变量提升），造成逻辑混乱，即可以先使用后声明
>
>+ var可以重复去定义同一个名字的变量，逻辑错误，正常来说，第二次应该是修改变量，而不是定义
>
>+ 在for循环中，会有临时变量污染问题
>
>+ var在声明时没有块级作用域（ES5，只有全局和局部）
>
>  `现在常用let改变var的弊端`

## 4、const关键字

>+ const定义的量为常量，其数据不能被修改，修改会出现报错
>
>+ 一般的，大多数情况下，会把const定义的量用大写来书写
>
>+ 引入某个模块的某个对象，也可以用const，可以进行小写命名
>
>+ 对象型常量，它的属性可以修改
>
>  ```javascript
>  const OBJ={
>  name:'node.js',
>  age:11
>  }
>  OBJ.name="Node.js"//对象中的属性修改不会报错
>  ```
>
>+ 数组型常量中的每一项数据会修改
>
>  ```javascript
>  const ARR = [10,20,30]
>  console.log(ARR)//[10,20,30]
>  ARR[1]=40
>  console.log(ARR)//[10,40,30]
>  ARR=[10,40,30]//此时修改会报错
>  ```

## 5、对象解构语法

>```javascript
>let obj = {
>name: 'node.js',
>age:11,
>    email: 'Nodejs.@163.com'
>}
>//获取对象中属性的方式
>//方法一：
>let name = obj.name;
>let age = obj.age;
>let email = ibj.email
>//方法二：
>let name = obj['name']
>let age = obj['age']
>let email = obj['email']
>//方法三
>let {name,age,email} = obj//完全解构，大括号中的变量名顺序可以任意，变量名只能是obj中的属性
>let {name} = obj//部分解构，只想获取部分属性可以只写这部分属性
>let {name:myName} = obj//部分解构，等效于 let name = obj.name
>//注意点
>//1、大括号里面的变量名，都只能是obj里面的属性名
>//2、大括号里面的变量名顺序可以任意
>//3、如果只想获得部分属性，可以只写这部分属性名
>//4、let {name} = obj ;等效于 let name = obj.name
>//5、let {name:myName} = obj;给name起一个别名myName,取obj的name属性赋值myName
>```

## 6、对象数组的解构

>```javascript
>let arr1 = [10,20,30]
>let [a,b,c] = arr1 //数组的解构，a、b、c就是自定义变量名
>let [,,b] = arr1//只获取第三个
>//字符串解构
>let str1 = 'hello'
>let [a,b,c] = str1//h e l
>```
>
>

## 7、模板字符串语法

>```javascript
>let obj = {
>    name: 'nodejs',
>    age:11,
>    eamil:'nodejs@163.com'
>}
>console.log(obj.name+'的年龄是'+obj.age+',它的邮箱是'+obj.email)
>//等价于以下模板语法
>console.log('${obj.name}的年龄是${obj.age},它的邮箱是${obj.email}')
>```

## 8、对象简化语法

>```javascript
>let name = 'nodejs'
>let age = 11
>let email = 'nodejs@163.com'
>let obj = {name,age,email}
>//以上代码得到的obj对象,相当于
>//obj = {
>  //  name : 'nodejs',
>   // age : 11,
>    //email : 'nodejs@163.com'
>//}
>```
>
>

## 9、函数参数解构

>```javascript
>function func({name,age}={}){//等效于{name,age}=obj 解构的格式
>    //name和age的值就是obj中的属性的值
>    //如果没有传参数，则使用默认值，等号后面就是默认值，此时name和age就是undefined
>    console.log(name,age)
>}
>
>```

## 10、三点运算符

>+ 在形参中，三点运算符也叫剩余参数
>
>  ```javascript
>  function func(a,b,...rest){//`...加上变量名`用来收集剩下的形参的,称之为剩余参数
>      console.log(a,b)
>      console.log(rest)//是一个数组,打印结果为[30，40，50，60]
>  }
>  func(10,20,30,40,50,60)
>  function func2(...rest){
>      console.log(rest)//是一个数组,打印结果为[10,20,30，40，50，60]
>  }
>  func2(10,20,30,40,50,60)
>  //注意点：
>  //`...`这种写法我们称为三点运算符，在形参中，称为剩余参数，其他地方不称为三点运算符
>  ```
>
>+ 在其他地方，三点运算符也叫拓展运算符
>
>  ```javascript
>  let arr 1 = [10,20,30]
>  function func(a,b,c){
>      console.log(a,b,c)
>  }
>  func(...arr1)//等效于func(arr1[0],arr1[1],arr1[2])
>  //合并数组
>  let arr2 = [30,40,50]
>  let newarr = [...arr1,...arr2]//相当于合并数组
>  //合并对象
>  //方法一：
>  let obj1 ={
>      name:'nodejs',
>      age:11
>  }
>  let obj2 = {
>      name:'javascript',
>      email:'nodejs@163.com'
>  }
>  let newobj = {...obj1,...obj2}//把对象中的键值对拆解出来
>  console.log(newobj)//如果有同属性名，后面的会覆盖前面的属性值
>  //方法二：
>  let newObj2 = Object.assign({},obj1,obj2)//把第二个和第二个以上的参数合并到第一个对象中
>  ```

## 11、箭头函数

>+ 箭头函数是es6中新的定义函数的一种方式,例如以下实例
>
>```javascript
>//没有参数
>let func = ()=>{
>    console.log('hello');
>}
>func()
>//含有形参
>let func1 = (x)=>{
>    console.log(x)
>}
>func1(30)
>//注意点：
>//1、书写箭头函数，形参依旧放在小括号中，多个形参以及默认值的书写格式和之前的普通函数相同
>//2、如果只有一个形参并且没有带默认参数，可以省略小括号
>let func1 = x=>{
>    console.log(x)
>}
>//3、如果函数体中只有一个语句，可以省略大括号不写
>let func1 = (x)=>console.log(x)
>//4、第3点的基础上，会返回一个值，给函数的调用结果
>let func2 = () =>999+1
>//上面的代码相当于
>let func2 = () =>{
>    return 999+1
>}
>let ret2 = func2()
>console.log(ret2)//打印结果为1000
>
>```
>
>+ 箭头函数的四种情况
>
>  ```javascript
>  //无参数无返回值
>  let func1 = () =>console.log("hello")
>  //无参数有返回值
>  let func2 = () =>999+1
>  //有参数无返回值
>  let func3 = x =>console.log(x)
>  //有参数有返回值
>  let func4 = x =>x+1
>  ```
>
>+ 箭头函数中的this
>
>  ```javascript
>  function People(name,age){
>      
>  }
>  ```
>
>  

## 12、面向对象编程

>+ Es6之前的写法
>
>  ```javascript
>  //用函数定义类
>  function Animal(name){
>      this.name = name
>  }
>  //给类实例定义方法
>  Animal.ptototype.showName = function(){
>      console.log(this.name)
>  }
>  //给类定义静态方法
>  Animal.eat = function(){
>      console.log("进食")
>  }
>  //根据函数实例化对象
>  var a = new Animal("Tom")
>  //调用对象的方法
>  a.showName()
>  ```
>
>+ ES6写法
>
>  ```javascript
>  
>  class Animal{//定义一个类
>      //构造器
>      construcor(name){
>          //在构造函数中定义初始属性
>          this.name = name//实例属性
>      }
>      //定义一个实例方法
>      showName(){
>          console.log('my name is ${this.name}')
>      }
>      //定义静态方法
>      static eat(){
>          console.log('吃-------')
>      }
>  }
>  //调用静态方法
>  Animal.eat()
>  //实例化一个对象，创建对象，创建对象时构造函数就会被执行
>  let dog = new Animal("小白")
>  
>  //注意要点：
>  //1、实例属性和实例方法都是给实例对象去调用的，即创建出来的对象去调用
>  //2、每一个实例对象在内存中是独立的，各自拥有自己的属性和方法，互不干扰
>  //3、`let dog = new Animal("小白")`做了什么事情：1、创建了新的对象，2、调用constructor方法，并传入对应的参数，3、把这个对象的指向给到dog标识符
>  //4、因为第3点中传入的参数，并执行了constructor方法，所以新对象才有了这些属性
>  //5、静态方法是通过类名调用
>  //6、静态属性的定义，目前在es6中，只能在类外面定义 类名.属性名 = 值 来定义
>  //7、如果一个方法不确定要定义成是实例方法还是静态方法，写完这个方法之后，它函数体里面有没有用到this，如果没有，就是静态方法,加上static，如果用到就是实例方法
>  
>  ```
>
>+ 继承——es6之前的写法
>
>  ```javascript
>  function Animail(name){
>      this.name = name
>  }
>  Animail.prototype.showName = function(){
>      console.log(this.name)
>  }
>  Animail.eat = function(){
>      console.log('进食')
>  }
>  //定义子类
>  function Mouse(name,color){
>      //子类继承父类的属性，需要将this指向父类中的name
>      Animail.call(this.name)
>      this.color = color
>  }
>  //子类继承父类的方法
>  Mouse.prototype = new Animail()
>  //给子类实例添加新方法
>  Mouse.prototype.showInfo = function (){
>      console.log(this.name,this.color)
>  }
>  var m = new Mouse('Herry','gray')
>  m.showName()
>  m.showInfo()
>  Animail.eat()
>  ```
>
>+ 继承——es6
>
>  ```javascript
>  class Animal{
>      construcor(name){
>          this.name = name
>      }
>      showName(){
>          console.log('my name is ${this.name}')
>      }
>      static eat(){
>          console.log('吃-------')
>      }
>  }
>  //继承的格式
>  //class 子类名 extends 父类名
>  class Cat() extend Animail{//子类 派生类
>      constructor(name){
>          super(name)//调用父类的constructor方法,name参数传入父类的构造方法
>          this.age = 10
>      }
>      //子类独立的方法
>      catchMouse(){//实例方法
>          console.log('抓老鼠')
>      }
>      showName(){//如果子类和父类的方法名相同，就称重写父类方法，调用时会执行子类的方法
>             console.log('喵喵！my name is ${this.name}')
>      }
>  }
>  let cat = new Cat("小白")
>  Cat.eat()//静态方法也可以继承
>  cat.showName()
>  
>  //继承的写法
>  //1、在继承的子类，如果出现过和父类中一样的名字，就是重写，这样一来，对象调用的就是子类中的这个方法
>  //2、一旦子类中定义了constructor方法，就必须在子类constructor方法中调用super()。方法，如果父类的constructor方法需要传递参数，那么super()方法中也要传入相应的参数
>  //3、子类中的this，在调用super()之后才器作用，否则在super()之前使用this会报错
>  ```

## 11、全局对象

>+ JavaScript中有一个特殊的对象，称为全局对象(Global Object)，它及其所有属性都可以在程序的任何地方访问，即全局变量
>
>  - 在浏览器JavaScript中，通常window是全局对象，而Node.js中的全局对象是global，所有全局变量(除了global本身以外)都是global对象的属性
>  - 后面看到所有的全局变量，例如console,setTimeout和process是global变量的成员，我们甚至可以向全局变量添加成员，使其在任何地方都可以用.
>
>  ```javascript
>  //1、node.js里面没有window全局对象，但是存在一个global全局对象，之前使用console,setTimeout这些全局函数都是global上面的属性
>  //console.log(window)//报错ReferenceError:window is no defined
>  //console.log(global)
> //2、Node.js里面声明的变量，不会挂载到global
>//3、可以向global添加成员，可以再任何地方去使用
>  //4、在node.js中执行js文件，里面如果出现this和global不是相等的，this在文件中指向的是当前的模块
>  ```
>

## 12、模块化

>```javascript
>//CommonJS 的 Modules 规范：NodeJS
>//在这个文件中使用m1模块的数据
>//require(路径)
>let m1 = require("./modules/m1.js")//导入 引入m1模块
>console.log(m1);
>console.log(m1.num)
>//注意点：
>//1、CommonJS的规范中，需要使用其他模块的数据的时候，引入的关键方法是require
>//2、require("./modules/m1.js")；参数可以是相对路径(./不能省略)，也可以是绝对路径
>//3、模块的扩展名可写可不写
>//导出之后一般有一个常量来接收(const)，常量名一般和模块名一致(不一致也不会报错)
>
>//导出模块
>let num = 10;
>fuction sum1(a,b){
>    return a+b
>}
>class Animal{
>    constructor(){
>        this.age = 10;
>    }
>}
>//第一种方式：
>exports.num = num;
>exports.sum1 = sum1;
>exports.Animal = Animal;
>//第二种方式
>module.exports = {
>    num,
>    sum1,
>    Animal
>}
>
>
>```
>
>

## 13、模块中的this指向问题

>```javascript
>console.log(exports = module.exports);//true
>console.log(module.exports)//{}
>console.log(exports)
>console.log(exports === this)//true
>//exports是module.exports的引用，文件中才有exports,交互模式下没有exports
>//在js文件中，this指向这个模块导出的这个对象 module.exports
>//在交互模式中，this === global,即在交互模式下，this指向全局变量global
>
>```

## 14、内置path模块

>
>
>```JavaScript
>const path = require('path')//引入内置模块path
>console.log(_dirname);//得到当前执行的文件的绝对路径，不包括文件名
>console.log(_filename);//得到当前执行的文件的绝对路径，包括文件名
>let extname = path.extname(_filename)//获取文件的扩展名
>
>```
>
>

## 15、读取文件信息

>+ 同步读取文件内容:读取文件的时候，要等到文件读取完毕，才会执行后面的代码(sync 同步)
>
>  ```javascript
>  const fs = require('fs')
>  const path = require('path')
>  let filepath = path.join(_dirname,'hello.txt')//拼接需要读取的文件路径
>  const content = fs.readFileSync(filepath,"utf-8" )//同步读取文件内容,把整个文件读取完毕之后才继续执行
>  ```
>
>+ 异步读取文件内容：不用等到文件读取完毕，就会执行后面代码
>
>```javascript
>//异步读取文件的时候需要有三个参数，回调函数
>const fs = require('fs')
>const path = require('path')
>let filepath = path.join(_dirname,'hello.txt')//拼接需要读取的文件路径
>fs.readFile(filepath,'utf-8',(error,data)=>{//异步读取，有一个回调函数，读取文件完毕的时候执行回调函数代码
>    if(error){
>         console.log(error)//错误信息，如果没有发生错误，就为null
>        return
>    }
>    console.log(data)//data读取到的文件信息，出现错误的时候data为undefined  
>})
>```
>
>

## 16、异步写入文件

>
>
>```javascript
>const fs = require('fs')
>const path = require('path')
>let filepath = path.join(_dirname,'hello.txt')//拼接需要读取的文件路径
>//fs.writeFile(文件路径，写入内容，'utf-8',回调函数)
>fs.writeFile(filepath,'hello write','utf-8',(error)=>{
>    if(error){
>        console.log(error)
>        return
>    }
>    console.log("写完毕")
>})
>```
>
>

## 17、http核心模块

>+ 搭建后端程序
>
>  ```javascript
>  //1、引入http模块
>  const http = require('http')
>  //2、配置服务器程序的端口号
>  const port = 8080
>  //3、创建服务器对象
>  const server = http.createServer((request,response)=>{
>      //requset请求对象，response响应对象
>      //没接收到一次请求就来执行这里代码一次
>      response.write("hello nodejs http")//可以往浏览器书写响应体
>      response.end("hello nodejs http")//表示响应工作已经结束，这个方法后不要再去写一些响应后的操作了。
>  })
>  //write 和end 相同点，都可以传入参数表示往浏览器书写一定内容
>  //write 和 end不同点，write可以连续操作，end表示响应结束一般放最后
>  //4、调用服务器对象的监听方法，让服务器监听浏览器请求
>  server.listen(port,(error)=>{
>      console.log(error);
>      console.log("Webserver is listerning at port 8080")
>  })
>  ```
>
>+ 获取请求对象相关的信息
>
>  ```javascript
>  const http = require('http')
>  const port = 8080
>  const server = http.createServer((request,response)=>{
>      //获取请求路径
>      let requrl = request.url
>      //获取请求方式
>      let reqMethod = request.method
>      //获取get请求的参数
>      let obj = url.parse(reqUrl,true)
>      console.log(obj.query)
>      response.write("hello nodejs http")
>      response.end("hello nodejs http")
>  })
>  server.listen(port,(error)=>{
>      console.log(error);
>      console.log("Webserver is listerning at port 8080")
>  })
>  ```
>
>  