# 编写可维护的Javascript

## 编程风格

### 1.基本格式

> 缩进

    4个空格/一个制表符

> 语句结尾

    *自动分号插入机制ASI（Automatic Semicolon Insert）会自动寻找代码中应当使用分号但是实际上没有使用分号的位置，  并插入分号*

    function getData(){
        return
        {}
    }
    => return;{}

> 行的长度

    80

> 换行

    1. 在运算符后换行，第二行追加两个层级缩进
    2. 在赋值语句，第二行的位置应当和赋值运算符的位置保持对齐

> 空行
使用空行的场景：

    1. 在方法之间
    2. 在方法中的局部变量和第一条语句之间
    3. 在多行或者单行注释之前
    4. 在方法内的逻辑片段之间插入空行，提高可读性

> 命名
命名原则

    1. 小驼峰
    2. 变量名前缀用名词，方法名前缀用动词
    3. 常量命名用大写字母和下划线
    4. 构造函数首字母要大写

> 直接量
使用原则

    1. 单引号或者双引号要保持一致
    2. 数字避免省略小数或者整数部分，避免八进制写法
    3. null:空指针对象；undefined：变量未声明
    4. 对象直接量：每个属性独占一行，并且保持一个缩进；最后的花括号也独占一行

    var book = {
        title:'Javascript'
    }

    5. 数组直接量：[] 代替 new Array()

### 2.注释

什么情况下要注释：

    1.  难于理解的代码
    2.  可能被认为错误的代码
    3.  浏览器特性hack
    4.  文档注释：入参、出参

> 单行注释

    1.注意：不应该连续使用多行单行注释，除非注释掉大段代码
    2.独占一行的注释：与双斜线之间有个空格，缩进和下一行保持一致
    3.行末尾的注释
    4.大段代码注释

    // 正确的注释
    if(isTrue){
       // 一系列处理
       handleData();
    }

> 多行注释

注意：空格和保持缩进

    /**
    * 一段多行注释
    * 多行注释
    */

### 3.语句和表达式

1. 不论语句块包含多行代码还是单行代码，都要使用花括号。
2. 花括号的对齐方式推荐：

    if (isTrue) {
            // 一些代码
    }

3. 语句块间隔推荐使用：
   if空格(xxx)空格{
4. switch缩进推荐使用：
    switch(){
        case 'first':
            // 代码
            break;
        case 'second':
            // 代码
            break;
        default:
            break;
    }
    注意：1）case的连续执行
         2）default不要省略 或者 写了注释的情况下省略default （ // 没有default）
5. width不应当继续使用
6. for循环中避免使用continue
7. for-in循环：以键值做遍历，不仅遍历实例上的属性，还遍历从原型上继承来的属性。最好使用hasOwnPrototype()方法过滤

### 4.变量 、函数和运算符

> 变量
- 不论var语句是否真的被执行，所有的var语句都会提前到包含这段逻辑的函数的顶部执行。因此推荐在函数顶部使用单var语句,每个变量的初始化应该独占一行，赋值运算符应当对齐。

    var value = 20,
        result = value + 10,
    i,
    len;

- 函数

推荐总是先声明js函数然后使用函数
函数声明不应当出现在语句块之内
函数调用间隔: doSometing(xxx)

- 立即调用的函数

    (function(){})();

- 相等

    ====

- 避免使用eval()

## 二：编程实践

### 1.UI层的松耦合

> 从CSS中抽离JS
> 从JS中抽离CSS：使用class作为通信的桥梁
> 从HTML中抽离JS：使用addEventListener
> 从JS中抽离HTML：从服务器加载或者客户端模版

### 2.避免使用全局变量：使用命名空间

> 单全局变量模式

    var maintainableJs = {};// 全局变量
    maintainableJs.book = {};// book -> namespace
    maintainableJs.color = {};//  another namespace

> 零全局变量模式

    立即执行的函数：适用于你的脚本非常短并且不需要和其他代码进行交互

### 3.事件处理

（1）隔绝应用逻辑
element.addEventListener('click',handleClick);
function handleClick(e){
        // do something
}
(2)不要分发事件对象
element.addEventListener('click',handleClick);
function handleClick(e.clientX,e.clientY){
        this,shopPop(e.clientX,e.clientY);
}
 
4.避免空比较
不好的做法：
if(object[propertyName]){};
if(object[propertyName] === null){};
if(object[propertyName] === undefined){};
当属性值为假值（0 '' null false undefined）时，都会导致判断错误.
判断属性最好的方法是使用in运算符
 
5.将配置数据从代码中分离出来
配置数据：都是写死在代码里面的，并且将来可能被修改
 
6.抛出自定义错误
抛出错误的经验法则：
1）一旦修复了一个很难调试的问题，尝试增加一两个自定义错误。当再次发生错误时，有助于更好的解决问题
2）如果在编写代码，思考一下：我希望【某些事情】不会发生，如果发生我的代码会一团糟。这时候如果【某些事情】发生，就要抛出错误
3）如果正在编写的代码别人也会用，思考一下他们的使用方式，在特定的情况下抛出错误
 
7.不是你的对象你不要动
应该把一个已经存在的对象像工具函数库一样对待：
不覆盖方法
不新增方法
不删除方法
 
更好的方式：
使用继承，方法可以腹写不会影响继承原型
 
7.浏览器嗅探
对特定功能进行探测
三：自动化（略）
