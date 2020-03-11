## es6基本语法
### let 和const
* let识别块级作用域 for循环使用
>* var 会发生变量提升，let 声明的变量一定要在声明后使用，否则报错
>* let 不允许变量重复声明
```javascript
{
    var a=1;
    let b=1;
}
console.log(a);// 1
console.log(b);//ReferenceError: a is not defined
```
* const 声明一个只读的常量 声明定义之后不可修改
### es6声明变量的6种方式
* var
* function
* let 
* const
* import
* class
### 解构赋值
* demo
```javascript
let [a,b,c]=[1,2,3];
let [a,[b,c,f],d,w,r]=[1,[2,3,4],5,6,7];
let [,,a]=[1,23,4];
//如果解构不成功，则会提示undifined
```
* 结构赋值允许设置默认值
```javascript
let [a,b=2]=[1,];
//es6使用严格相等运算符，当值为undifined时，默认值会生效，如果是null，
//设置默认值会失效
```
#### 对象的结构赋值
* 对象的结构赋值不同于数组的解构赋值，数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。 对象则要求同名
* demo
```javascript
let {a,b}={a:2,b:3};
console.log(a,b);
//属性名不同时
let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
console.log(f,l);//hello world
```
* 
* 对象的解构赋值也可以设置默认值，解构失败变量的值等于undifined //要注重：undifined和null不严格相等
```javascript
let x;
{x}={x=1};
//将会报错，引擎将{x}识别为代码块，发生语法错误 可以添加括号解决该问题 ({x}={x=1})//输出1
```
#### 字符串的结构赋值
```javascript
const [a,b,c,d,e]='hello';
//类数组
let {length:len}='hello';  //输出字符串长度5
```
#### 数值和布尔值的解构赋值
* 解构赋值时，如果等号右边是数值和布尔值，先会转为对象
```javascript
let {toString: s} = 123;
console.log(s);
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```
#### 函数参数的解构赋值
```javascript
function add([x,y]){
    return x+y;
}
aa([1,2]);
[[1, 2], [3, 4]].map(([a, b]) => a + b);//[3,7]
```
### 模板字符串
```javascript
var str=`<div>${变量}</div>`;
```
### Symbol 原始类型 表示独一无二的值
* 原始数据类型:__string__,__boolean__,__number__,__undefined__,__null__,__Object__,__Symbol__
### proxy 可以理解成拦截
```javascript
var obj = new Proxy({}, {
            get: function (target, propKey, receiver) {
                console.log(`getting ${propKey}!`);
                return Reflect.get(target, propKey, receiver);
            },
            set: function (target, propKey, value, receiver) {
                console.log(`setting ${propKey}!`);
                return Reflect.set(target, propKey, value, receiver);
            }
        });
        obj.count=1;
        //  setting count!
        console.log('------------------')
        ++obj.count
        //  getting count!
        //  setting count!
```
* var proxy = new Proxy(target, handler);
>* new proxy 表示生成一个proxy实例
>* target 表示要拦截的对象
>* hander 表示定制拦截行为
```javascript
var proxy = new Proxy({}, {
  get: function(target, propKey,receiver) {
   ······
  },
  set:function(){
    ······
  }
});
```
* proxy的handler是一个配置对象
>* get方法接收三个参数,目标对象、属性名、proxy实例本身(严格地说，是操作行为所针对的对象),最后一个参数可选
>* set方法接收四个参数，目标对象、属性名、属性值、proxy本身实例，最后一个参数可选
* proxy 支持的拦截操作
>* **get(target, propKey, receiver)**: 拦截对象的读取，
>* **set(target, propKey, value, receiver)**: 拦截对象属性的设置 eg: _obj.a=1;_
>* **has(target, propKey)**: 拦截_propKey in proxy_的操作，返回一个布尔值
>* **deleteProperty(target, propKey)**: 拦截_delete proxy[propKey]_的操作，返回一个布尔值
>* **ownKeys(target)**: 拦截_Object.getOwnPropertyNames(proxy)_、_Object.getOwnPropertySymbols(proxy)_、_Object.keys(proxy)_、_for...in_循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
>* **getOwnPropertyDescriptor(target, propKey)**: 拦截_Object.getOwnPropertyDescriptor(proxy, propKey)_，返回属性的描述对象。
>* **defineProperty(target, propKey, propDesc)**: 拦截_Object.defineProperty(proxy, propKey, propDesc）_、_Object.defineProperties(proxy, propDescs)_，返回一个布尔值。
>* **preventExtensions(target)**: 拦截_Object.preventExtensions(proxy)_，返回一个布尔值。
>* **getPrototypeOf(target)**: 拦截_Object.getPrototypeOf(proxy)_，返回一个对象。
>* **isExtensible(target)**: 拦截_Object.isExtensible(proxy)_，返回一个布尔值。
>* **setPrototypeOf(target, proto)**: 拦截_Object.setPrototypeOf(proxy, proto)_，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
>* **apply(target, object, args)**: 拦截 Proxy 实例作为函数调用的操作，比如_proxy(...args)_、_proxy.call(object, ...args)_、_proxy.apply(...)_。
>* **construct(target, args)**: 拦截 Proxy 实例作为构造函数调用的操作，比如_new proxy(...args)_。
### promise对象
```javascript
let p=new Promise((res,rej)=>{
  setTimeout(()=>{
            console.log(1);
            res();
        },2000)
});
p.then(()=>{
  console.log(2)
})
```
* *resolve*函数将 __Promise__对象的状态从'未完成'变为'成功'
* *reject*函数将 __Promise__对象的状态从'未完成'编程'失败'
* __Promise__ 对象实例生成后，可用then方法分别指定*resolve* 和 *reject*状态的回调函数
* __Promise__ 在新建之后会立即执行
```javascript
let p=new Promise((res,rej)=>{
  console.log(3);
  setTimeout(()=>{
            console.log(2);
            res();
  },2000)
})
p.then(()=>{
  console.log(1)
})
//立即输出 3，两秒之后输出 2 1
```
* __catch()__ 
>* 用于指定发生错误时的回调函数。
```javascript
let p=new Promise((res,rej)=>{
  setTimeout(()=>{
    // res();
    rej('发生错误');
  },1000)
})
p.then(()=>{

}).catch((error)=>{
  console.log(error);
})
```
* __finally()__ 
>* 不管promise最后的状态如何 都会执行
>* finally函数不接受任何参数 不会知道promise最后处于的状态
```javascript
let p=new Promise((res,rej)=>{
  // .....
}).then(()=>{
  //...
}).catch(error=>{
  //...
}).finally(()=>{
  //...
})
```
* __all()__
>* 用于将多个promise实例包装成一个新的实例
>* p的状态取决于p1,p2,p3的状态 三个都是成功状态，p才会变成成功，其中一个是rejected，p就会变成rejected
```javascript
let p1=new Promise((res,rej)=>{
  //...
});
let p2=new Promise((res,rej)=>{
  //...
})
let p3=new Promise((res,rej)=>{
  //...
})
let p=Promise.all([p1,p2,p3]).then(result=>{
  //...
})
```
* __race()__
>* 将多个promise实例，包装成一个新的实例
>* 只要实例中有一个promise实例状态发生了变化，无论成功还是失败，该实例就会变化
```javascript
let p1=new Promise((res,rej)=>{
  //...
});
let p2=new Promise((res,rej)=>{
  //...
})
let p3=new Promise((res,rej)=>{
  //...
})
let p=Promise.race([p1,p2,p3]).then(result=>{
  //...
})
```
* __allSettled()__
>* 将多个实例包装成一个新的Promise实例
>* 只有当所有的实例状态变化后才会结束
>* 所有实例结束后，无论成功还是失败，该实例都显示成功，不会有失败状态
>* 该实例成功后，会得到数组实例的结果
* __any()__
>* 接受一组 Promise 实例作为参数，包装成一个新的 Promise 实例。
>* 只要数组实例有一个变为成功状态，该实例会变成成功状态
>* 如果所有参数实例都是失败状态，该实例会变成失败状态
* __resolve()__
>* 将现有对象转化为Promise实例
* __reject()__
>* 返回一个新的Promise实例，该实例结果为rejected(失败)
## Module 的语法
* es6模块不是对象,通过 __export__ 显式指定输出的代码，用import命令输入
* es6的模块自定采用严格模式
* __export__ 命令
>* 模块功能主要有两个命令：__export__ 和 __import__
>>* __export__ 规定模块的对外接口
>>* __improt__ 输出模块提供的功能
```javascript
var firstname='jason';
var lastname='jack';
var year=1988;
export {firstname,lastname,year};
```
* 以上为 export 输出变量 {}表示一组变量
```javascript
export function add(x,y){
  return x+y;
}
```
* 以上为export 输出函数add，也可输出类
```javascript
function a(){
  //.....
}
function b(){
  //.....
}
export {a as v1,b as v2}
```
* 可用 __as__ 重新命名对外接口
* 要想输出值，最好写在{}中
* __import__ 命令
```javascript
import {a,b,c} from './add.js'
```
>* import 命令接受一对大括号，里面指定要从其他模块导入的变量，要与模块的命名统一
>* import 可使用 __as__ 对导入变量重新命名
>* 可使用 __*__ 表示将模块整体引入
```javascript
import * as func from './module'
```
* __export default__ 命令
```javascript
//module.js
export default function(){
  console.log('fn')
}
//main.js 引入模块
import myfn from './module'
myfn();//fn
```
>* 导出一个匿名函数模块，在其他模块引用时可以直接定义，用任意名称指向该输出的方法，此时import后面不适用{}
>* 也可用在非匿名函数的模块的导出
## js操作字符串
* 对字符串的索引进行操作，不会报错，也不会有任何结果
* toUpperCase() 将字符串全部转化为大写
* toLowerCase() 将字符串全部转化为小写
* indexOf() 搜索指定字符串出现的位置，没有找到则返回-1
* substring() 返回指定区间内的字符串；(0,5) 从0开始到5之间的字符串，但不包括5； (7)从7开始到结束
## js操作数组
* 数组可以通过索引将对应的元素改为新的值，对数组的索引操作会改变数组
* indexOf() 搜索一个指定的元素
* slice()  截取一个区间的元素并组成一个新数组，相当于字符串substring()方法
* push() 向数组末尾添加若干元素
* pop() 删除数组的最后一个元素
* unshift() 向数组头部添加若干元素
* shift() 删除数组的第一个元素
* sort() 对当前数组进行排序 修改数组中元素的位置 直接调用将按照默认顺序排序，也可以自定义排序
* reverse() 将数组倒序 从后到前的顺序重新排列
* splice() 数组‘万能方法’，(2,3,'a','b');从索引2的位置开始删除3个元素，并添加两个元素，会返回被删除的元素；(2,2)从索引2的位置删除两个元素没有添加元素；(2,0,'a','b')返回空数组并没有删除，原数组不发生变化；
* concat() 连接两个数组并返回一个新的数组，没有修改当前数组，只是重新生成一个新数组；
* join() 将数组用指定字符串连接，并返回一个新的字符串；如果元素不是字符串，会先进行转化在连接；
* every 方法，如果每个元素都符合条件返回true，否则就返回false
```javascript
var arr = [1, 3, 4, 5, 6, 7, 8];
var arr1 = arr.every(function (item, index, array) {
            return item > 3
        });
        console.log(arr1)
```
* filter 返回符合条件的元素
```javascript
var arr2 = arr.filter(function (item, index, array) {
            return item > 3
        })
        console.log(arr2);
```
* foreach 无返回值 可以对每一项进行操作 常用作列表渲染
```javascript
var html = '';
        arr.forEach(function (item, index) {
            html += '<p>' + item.id + '</p>';
        });
```
* map 对每一项进行操作并返回每次元素调用函数的结果组成的数组
```javascript
ar arr3 = arr.map(function (item, index, array) {
            return item * 2
        });
        console.log(arr3);
```
* some 对每一项进行函数调用 只要有一个满足条件 则返回true，否则返回false 与every相反,
```javascript
var arr4 = arr.some(function (item) {
            return item > 1
        });
        console.log(arr4);
```
* reduce 和 reduceRight 迭代数组所有项 返回最终的值 ,reduceRight与reduce操作一样 但迭代方向相``反,arr.reduce(callback,[initialValue]) initialValue 作为第一次调用 callback 的第一个参数。
```javascript
var sum = arr.reduce(function (total, cur, index, array) { //total 指计算后的返回值，cur值当前元素，index指当前元素的索引 array为原数组
            console.log(total, cur, index);
            return total + cur
        })
        console.log(sum);
```
## 立即执行函数
* 立即执行函数 将var变量的作用域限制于函数内，这样可以避免命名冲突。
```javascript
        //类型1：
        (function () {
            console.log(2)
        })();
        //类型2：
        ;(function () {
            console.log(document.scripts);
        }());
```
* 除了() 立即执行函数也是使用 + - = !符号 ，将匿名函数或函数声明转为函数表达式
```javascript
        !function () {
            console.log(window)
        }(window);
```
## js6种继承方式
```javascript
// 父类
    function Person(name){
        this.name=name;
        this.sum=function(){
            console.log(this.name)
        }
    }
    Person.prototype.age=10;
    function Per(){
        this.name='skr'
    }
//原型链继承
    Per.prototype=new Person();
    var per1=new Per();
    console.log(per1.age);
//借用构造函数继承
    function Con(){
        Person.call(this,'jer');
        this.age=12;
    }
    var con1=new Con();
    console.log(con1.name)
    console.log(con1.age);
//组合继承 （组合原型链继承和借用构造函数继承）
    function SubType(name){
        Person.call(this,name)
    }
    SubType.prototype=new Person();
    var sub=new SubType('skr');
    console.log(sub.name);
    console.log(sub.age)
//原型式继承
    function content(obj){
        function F(){};
        F.prototype=obj;
        return new F();
    }
    var sup=new Person();
    var sup1=content(sup);
    console.log(sup.age);
//寄生式继承
    function content(obj){
        function F(){};
        F.prototype=obj;
        return new F();
    }
    var sup2=new Person();
    function subobject(obj){
        var sub=content(obj);
        sub.name='sjk';
        return sub;
    }
    var sub2=subobject(sup2);
    console.log(sub2.name);
//寄生组合式继承（常用）
function content(obj){
        function F(){};
        F.prototype=obj;
        return new F();
    }
    var con2=content(Person.prototype);
    function Sub(){
        Person.call(this);
    }
    Sub.prototype=con2;
    con2.constructor=Sub;
    var sub3=new Sub();
    console.log(sub3.age);
```
## 正则表达式匹配规则
### 字面量字符和元字符
* 点字符(.) 匹配除回车(\r)、换行(\n)、行分隔符(\u2028)、和段分割符(\u2029)以外的所有字符
* 位置字符 用来提示字符所处的位置; (^)表示字符串开始的位置 ($)表示字符串结束的位置
* 选择符(|) 表示 或 的关系 即cat|dog 表示匹配cat或者dog。选择符会包括它前后的多个字符，比如/ab|cd/指的是匹配ab或者cd，而不是指匹配b或者c。如果想修改这个行为，可以使用圆括号。
* 转义符(\\); 匹配有特殊含义的元字符 加上反斜杠。需要反斜杠转义的字符：(^),(.),([),($),(\(),(\)),(|),(*),(+),(?),({),(\\)。
### 特殊字符串
* (\cX) 表示 Ctrl-[X],其中 X 表示A-Z之中任何一个字母 用来匹配控制字符
* ([\b]) 匹配退格键(U+0008),不要和\b混淆
* (\n) 匹配换行键
* (\r) 匹配回车键
* (\t) 匹配制表符tab(U+0009)
* (\v) 匹配垂直制表符(U+000B)
* (\f) 匹配换页符(U+000C)
* (\O) 匹配null字符(U+0000)
* (\xhh) 匹配一个以两位十六位进制数(\x00 - \xFF)表示的字符
* (\uhhhh) 匹配一个以四位十六进制数(\u0000 - \uFFFF) 表示的unicode字符
### 字符类 表示一系列字符可供选择 只要匹配其中一个,供选择的字符放在[]中
* 脱字符([^]) 表示除了字符之中的字符其他都可以匹配 。[^abc]表示除了abc以为的字符 [^]表示匹配一切字符包括换行符
* 连字符(-) [a-c],表示从a到c  [0-9] 表示0123456789 只在[]中起作用 [1-31]只匹配1-3
###预定义模式 表示几种常见模式的写法
* (\d) 表示0-9 相当于[0-9]
* (\D) 表示0-9以外的数字 相当于[^0-9]
* (\w) 表示任意的字母、数字和下划线 相当于[0-9A-Za-z_]
* (\W) 表示匹配除字母、数字和下划线以为的字符 相当于[^0-9a-zA-z_]
* (\s) 匹配空格（包括换行符、制表符、空格符等），相等于[ \t\r\n\v\f]。
* (\S) 匹配非空格的字符，相当于[^ \t\r\n\v\f]。
* (\b) 匹配词的边界。
* (\B) 匹配非词边界，即在词的内部
### 重复类 使用{}表示
* ({n}) 表示重复n次
* ({n,}) 表示至少重复n次
* ({n,m}) 表示重复不少于n次 不多于m次
### 量词 贪婪模式 最大限度的匹配 直到匹配到下一个不满足的字符为止
* (?) 表示某个模式出现0次或一次 相当于{0,1}
* (*) 表示某个模式出现0次或多次 相当于{0,}
* (+) 表示某个模式出现一次或者多次 相当于{1,}
### 修饰符
* (g) 默认情况 正则对象第一次匹配成功就会停止匹配 ，g表示全局匹配 主要用于搜索和替换
* (i) 默认情况下 正则区分字母的大小写，i表示忽略字母的大小写
* (m) m修饰符表示多行模式（multiline），会修改^和$的行为。默认情况下（即不加m修饰符时），^和$匹配字符串的开始处和结尾处，加上m修饰符以后，^和$还会匹配行首和行尾，即^和$会识别换行符（\n）。
* 组匹配() 正则表达式的括号表示分组匹配，括号中的模式可以用来匹配分组的内容。
* 非捕获组 (?:x) 表示不返回该组匹配的内容
* 先行断言 x(?=y) x只有在y前面才匹配，y不会被计入返回结果。比如，要匹配后面跟着百分号的数字，可以写成/\d+(?=%)/。
* 先行否定断言 x(?!y)称为先行否定断言（Negative look-ahead），x只有不在y前面才匹配，y不会被计入返回结果。比如，要匹配后面跟的不是百分号的数字，就要写成/\d+(?!%)/。
## 正则基本语法
* \d ---- 匹配数字
* \w ---- 匹配一个字母或数字
* \s ---- 匹配空格或空白
* . ---- 可以匹配任意字符
* \* ---- 表示任意个字符(包括0个)
* \+ ---- 表示至少一个字符
* ? ---- 表示0个活1个字符
* {n} ---- 表示n个字符
* {n,m} ---- 表示n-m个字符
* \ ---- 反斜杠 转义
* [] ---- 表示范围
>* [0-9a-zA-Z\_]可以匹配一个数字、字母或者下划线
>* [0-9a-zA-Z\_]+可以匹配至少由一个数字、字母或者下划线组成的字符串，比如'a100'，'0_Z'，'js2015'等等
>* [a-zA-Z\_\$][0-9a-zA-Z\_\$]{0, 19}更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符
* () ---- 表示提取的分组
* A|B ---- 匹配A或者B
* ^ ---- 表示行开头 eg:^\d 表示数字开头
* $ ---- 表示结束 \d$ 数字结束
* /g ---- 全局搜索
* i ---- 忽略大小写
* m ---- 执行多行匹配 
### 练习
```javascript
//书写方式
//第一种
var re1=/ABC\-001/;
var re2=new RegExp('ABC\\-001');//字符转义  所以两个\
//用 test() 方法 测试给定的字符串是否符合条件
re1.test('1234563');//false
```
### 切分字符串
```javascript
'a b   c'.split(' '); // ['a', 'b', '', '', 'c'] 无法识别连续的空格
//使用正则
'a,b, c  d'.split(/[\s\,]+/); // ['a', 'b', 'c', 'd']
```
