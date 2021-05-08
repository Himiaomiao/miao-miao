# JavaScript数组方法

## 1、数组对象继承的方法

>`[toString()]`
>
>toString()方法返回以逗号分割的每个数组中的值。
>
>【注意】：此方法的返回值和不使用任何参数调用join()方法返回的字符一样。
>
>```javascript
>[123].toString();//'1,2,3'
>['a','b','c'].toString();//'a,b,c'
>[1,[2,'c']].toString();//'1,2,c'
>```
>
>	alert([1,2,3]);//'1,2,3'
>`[toLocaleString()]`
>toLocaleString()是toString()方法的本地化版本，经常返回与toString()方法相同的值
>``` javascript
>var colors = [1,undefined,2,null,3];
>console.log(colors.toString());//'1,,2,,3'
>console.log(colors.toLocaleString());//'1,,2,,3'
>```
>`[valueOf]`
>valueOf()方法返回数组对象本身
>```javascript
>var a = [1,2,3];
>console.log(a.valueOf());//[1,2,3]
>console.log(a.valueOf() instanceof Array);//true
>```

## 2、数组转换方法
>`[join()]`
>Array.join()方法是String.split()方法的逆向操作，后者是将字符串分割成若干块来创建一个数组。
>数组继承的toLocaleString()和toString()方法，在默认情况下都会以逗号分隔的字符形式返回数组项，而join()可以选择不同的分隔符，join()方法只接收一个参数，用作分隔符的字符串，然后返回。
>```javascript
>var a = [1,2,3]
>console.log(a.join());//'1,2,3'
>console.log(a.join(' '));//'1,2,3'
>console.log(a.join(''));//'123'
>```
>* 若join()方法的参数是undefined,标准浏览器以逗号为分隔符返回字符串，而IE浏览器以undefined为分隔符`
>
>```javascript
>var a = [1,2,3]
>console.log(a.join(undefined))
>```
>* 如果数组中的某一项的值是null或者undefined，则该值在join()方法返回结果中以空字符串表示`
>
>```javascript
>var colors = [1,undefined,2,null,3]
>console.log(colors.join())//'1,,2,,3'
>```
>* 该方法可以用于类数组对象上`
>
>```javascript
>console.log(Array.prototype.join.call('hello', '-'));// "h-e-l-l-o"
>var obj = { 0: 'a', 1: 'b', length: 2 };
>console.log(Array.prototype.join.call(obj, '-'));// 'a-b'
>```
>* 【注意】若对象没有length属性，就不是类数组，也就不能调用数组的方法`
>
>```javascript
>var obj = { 0: 'a', 1: 'b' };
>console.log(Array.prototype.join.call(obj, '-'));//''
>```
>* 使用join()方法可以创建重复某些字符N次的函数`
>
>```javascript
>function repeatString(str,n){
>return new Array(n+1).join(str);
>}
>console.log(repeatString('a',3));//'aaa'
>console.log(repeatString('Hi',5));//'HiHiHiHiHi'
## 3、栈和队列方法

>　　push()和pop()方法允许将数组当作栈来使用。unshift()和shift()方法的行为非常类似于push()和pop()，不一样的是前者是在数组的头部而非尾部进行元素的插入和删除操作
>
>　　栈是一种LIFO(Last-In-First-Out，后进先出)的数据结构，也就是最新添加的项最早被移除。而栈中项的插入(叫做推入)和移除(叫做弹出)，只发生在一个位置——栈的顶部。javascript为数组专门提供了push()和pop()方法，以便实现类似栈的行为
>
>　　队列数据结构的访问规则是FIFO(First-In-First-Out，先进先出)。队列在列表的末端添加项，从列表的前端移除项。结合使用shift()和push()方法，可以像使用队列一样使用数组
>
>`[push]`
>
>* push()方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度，所以该方法会修改原数组
>
>```javascript
>var a = [];
>console.log(a,a.push(1));//[1] 1
>console.log(a,a.push('a'));//[1,'a'] 2
>console.log(a,a.push(true, {}));//[1,'a',true,{}] 4
>console.log(a,a.push([5,6]));//[1,'a',true,{},[5,6]] 5
>```
>
>* 如果需要合并两个数组，可以使用apply方法 
>
>```javascript
>var a = [1, 2, 3];
>var b = [4, 5, 6];
>console.log(a,Array.prototype.push.apply(a, b));//[1,2,3,4,5,6] 6
>```
>
>* [注意]如果使用call方法，则会把数组b整体看成一个参数
>
>```javascript
>var a = [1, 2, 3];
>var b = [4, 5, 6];
>console.log(a,Array.prototype.push.call(a, b));//[1,2,3,[4,5,6]] 4
>```
>
>* push()方法也可以向对象中添加元素，添加后的对象变成类数组对象，即新加入元素的键对应数组的索引，并且对象有一个length属性
>
>```javascript
>var obj = {a: 1};
>console.log(obj,[].push.call(obj, 2));// {a:1, 0:2, length: 1}
>console.log(obj,[].push.call(obj, [3]));// {a:1, 0:2, 1:[3], length: 2}
>```
>
>`[pop()]`
>
>* pop()方法从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。所以，该数组会改变原数组
>
>```javascript
>var a = ['a', 'b', 'c'];
>console.log(a,a.pop()); // ['a', 'b'] 'c'
>```
>
>* 对空数组使用pop()方法，不会报错，而是返回undefined
>
>```javascript
>var a = [];
>console.log(a,a.pop()); // [] undefined
>```
>
>`[shift()]`
>
>* shift()方法移除数组中的第一个项并返回该项，同时数组的长度减1。所以，该数组会改变原数组
>
>```javascript
>var a = ['a', 'b', 'c'];
>console.log(a,a.shift());//['b', 'c'] 'a'
>```
>
>* 对空数组使用shift()方法，不会报错，而是返回undefined
>
>```javascript
>var a = [];
>console.log(a,a.shift());// [] undefined
>```
>
>`[unshift()]`
>
>* unshift()方法在数组前端添加任意个项并返回新数组长度。所以，该数组会改变原数组
>
>```javascript
>var a = ['a', 'b', 'c'];
>console.log(a,a.unshift('x')); //['x', 'a', 'b', 'c'] 4
>```
>
>* 当使用多个参数调用unshift()时，参数是一次性插入的而非一次一个地插入。这意味着最终的数组中插入的元素的顺序和它们在参数列表中的顺序一致
>
>```javascript
>var a = ['a', 'b', 'c'];
>console.log(a,a.unshift('x','y','z')); //['x','y','z','a', 'b', 'c'] 6
>```
>
>* 【注意】在IE7-浏览器中，unshift()方法返回的总是undefined`
>
>```javascript
>//标准浏览器下，返回[1] 1；而IE7-浏览器下，返回[1] undefined
>var a = [];
>console.log(a,a.unshift(1));
>
>```

## 4、数组排序方法

>数组中存在两个可以直接用来重排序的方法: reverse()和sort() 
>
>`【reverse()】`
>
>* reverse()方法用于反转数组的顺序，返回经过排序之后的数组；而原数组顺序也发生改变
>
>```javascript
>var array = [1,2,4,3,5];
>console.log(array,array.reverse());//[5,3,4,2,1] [5,3,4,2,1]
>var array = ['str',true,3];
>console.log(array,array.reverse());//[3,true,'str'] [3,true,'str']
>```
>
>`【sort()】`
>
>* 默认情况下，sort()方法按字符串升序排列数组项，sort方法会调用每个数组项的toString()方法，然后比较得到的字符串排序，返回经过排序之后的数组，而原数组顺序也发生改变
>
>```javascript
>var array = [1,2,4,3,5];
>console.log(array,array.sort());//[1,2,3,4,5] [1,2,3,4,5]
>var array = ['3str',3,2,'2'];
>console.log(array,array.sort());//[2, "2", 3, "3str"] [2, "2", 3, "3str"]
>var array = [1,5,10,50];
>console.log(array,array.sort());//[1, 10, 5, 50] [1, 10, 5, 50]
>```
>
>* 如果数组包含undefined元素，它们会被排到数组的尾部
>
>```javascript
>var array = ['3',3,undefined,2,'2'];
>console.log(array,array.sort());//["2", 2, "3", 3, undefined] ["2", 2, "3", 3, undefined]
>```
>
>* sort()方法可以接受一个比较函数作为参数，以便指定哪个值在哪个值的前面。比较函数接收两个参数，如果第一个参数应该位于第二个参数之前则返回一个负数，如果两个参数相等则返回0，如果第一个参数应该位于第二个参数之后则返回一个正数
>
>```javascript
>function compare(value1,value2){
>    if(value1 < value2){
>        return -1;
>    }else if(value1 > value2){
>        return 1;
>    }else{
>        return 0;
>    }
>}
>var array = ['5px',50,1,10];
>//当数字与字符串比较大小时，字符串'5px'会被转换成NaN，这样结果就是false
>console.log(array.sort(compare));//["5px",1, 10, 50]
>
>```
>
>* 对于数值类型或valueOf()方法会返回数值类型的对象类型，比较函数可以简化
>
>```javascript
>function compare(value1,value2){
>    return value1 - value2;
>}
>var array = ['5px',50,1,10];
>console.log(array.sort(compare));//["5px",1,10,50]
>var array = [5,50,1,10];
>console.log(array.sort(compare));//[1,5,10,50]
>```
>
>* 如果对一个字符串数组执行不区分大小写的字母表排序，比较函数首先将参数转化为小写字符串再开始比较
>
>```javascript
>a = ['ant','Bug','cat','Dog'];
>a.sort();//['Bug','Dog','ant','cat'];
>a.sort(function(s,t){
>    var a = s.toLowerCase();
>    var b = t.toLowerCase();
>    if(a < b)return -1;
>    if(a > b)return 1;
>    return 0;
>});//['ant','bug','cat','dog']
>```
>
>* 使用sort()方法创建一个随机数组
>
>```javascript
>function compare(){
>    return Math.random() - 0.5;
>}
>var array = [1,2,3,4,5];
>console.log(array.sort(compare));//[2,1,5,4,3]
>```

## 5、数组拼接方法

>`[concat()]`
>
>* concat()方法基于当前数组中的所有项创建一个新数组，先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。所以concat()不影响原数组
>
>  　　如果不给concat()方法传递参数时，它只是复制当前的数组；如果参数是一个或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中；如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾
>
>```javascript
>var numbers = [1,2];
>console.log(numbers,numbers.concat(3,4));//[1,2] [1,2,3,4]
>console.log(numbers,numbers.concat([5,4,3],[3,4,5],1,2));//[1,2] [1,2,5,4,3,3,4,5,1,2]
>console.log(numbers,numbers.concat(4,[5,[6,7]]));//[1,2] [1,2,4,5,[6,7]]
>```
>
>* 　如果不提供参数，concat()方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是如果数组成员包括复合类型的值（比如对象），则新数组拷贝的是该值的引用
>
>```javascript
>//该方法实际只复制了数组的第一维，数组第一维存放的是第二维的引用，而第二维才是实际存放他们的内容
>var numbers = [1,2];
>var newNumbers = numbers.concat();
>console.log(numbers,newNumbers);//[1,2] [1,2]
>numbers[0] = 0;
>console.log(numbers,newNumbers);//[0,2] [1,2]
>
>var numbers = [[1,2]];
>var newNumbers = numbers.concat();
>console.log(numbers,newNumbers);//[[1,2]] [[1,2]]
>numbers[0][0] = 0;
>console.log(numbers,newNumbers);//[[0,2]] [[0,2]]
>
>```
>
>* concat()方法也可以用于将对象合并为数组，但是必须借助call()方法
>
>```javascript
>var newArray = Array.prototype.concat.call({ a: 1 }, { b: 2 })
>console.log(newArray);// [{ a: 1 }, { b: 2 }]
>console.log(newArray[0].a);//1
>```

## 6、创建子数组方法

>* lice()方法基于当前数组中的一个或多个项创建一个新数组，接受一个或两个参数，即要返回项的起始和结束位置，最后返回新数组，所以slice()不影响原数组
>
>  　　slice(start,end)方法需要两个参数start和end，返回这个数组中从start位置到(但不包含)end位置的一个子数组；如果end为undefined或不存在，则返回从start位置到数组结尾的所有项
>
>  　　如果start是负数，则start = max(length + start,0)
>
>  　　如果end是负数，则end = max(length + end,0)
>
>  　　start和end无法交换位置
>
>  　　如果没有参数，则返回原数组
>
>```javascript
>var numbers = [1,2,3,4,5];
>console.log(numbers.slice(2));//[3,4,5]
>console.log(numbers.slice(2,undefined));//[3,4,5]
>console.log(numbers.slice(2,3));//[3]
>console.log(numbers.slice(2,1));//[]
>
>console.log(numbers.slice(-3));//-3+5=2 -> [3,4,5]
>console.log(numbers.slice(-8));//max(5 + -8,0)=0 -> [1,2,3,4,5]
>
>console.log(numbers.slice(0,-3));//-3+5=2 -> [1,2]
>console.log(numbers.slice(-2,-1));//-2+5=3;-1+5=4; -> [4]
>```
>
>
>
>