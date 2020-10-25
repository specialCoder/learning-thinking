# 编写可维护的Javascript
[toc]

## 一：编程风格

### 为什么要讨论编程风格
提炼编程风格是一道工序，花再多的时间也不为过。毕竟每个人都有自己的想法，如果一天当中你有8小时是在写代码，那么你自然希望用一种舒服的方式来写代码。刚开始，团队成员对新的编程风格有点不适应，全靠强势的项目组长强制推行才得以持续。一旦风格确立后，这套编程风格就会促成团队成员高水准的协作，因为所有代码（的风格）看起来极为类似。

在团队开发中，所有的代码看起来风格一致是极其重要的，原因有以下几点:
1. 任何开发者都不会在乎某个文件的作者是谁，也没有必要花费额外
精力去理解代码逻辑并重新排版，因为所有代码排版格式看起来非常一
致。我们打开一个文件时所干的第一件事，常常不是立即开始工作而是
首先修复代码的缩进，当项目很庞大时，你会体会到统一的编程风格的
确大幅度节省了时间成本。

2. 我能很容易地识别出问题代码并发现错误。如果所有代码看起来很
像，当你看到一段与众不同的代码时，很可能错误就产生在这段代码
中。

毫无疑问，全球性的大公司都对外或对内发布过编程风格文档。编程风格是个人的事情，只有放到团队开发中才能发挥作用。本书的这部分给出了JavaScript编码规范中值得关注（推荐）的方面。在某些场景中，很难说哪种编程风格好，哪种编程风格不好，因为有些编程风格只是某些人的偏好。

### 基本格式
>“程序是写给人读的，只是偶尔让计算机执行一下。”——Donald Knuth。

#### 缩进: 4个空格
推荐使用4个空格字符为一个缩进层级:
- 很多文本编辑器都默认将缩进设置为4个空格，你可以在编辑器中配置敲入Tab键时插入4个空格。
- 使用2个空格的缩进时，代码的视觉展现并不是最优的，至少看起来是这样。
> 尽管是选择制表符还是选择空格做缩进只是一种个人偏好，但绝对不要将两者混用，这非常重要。这么做会导致文件的格式很糟糕，而且需要做不少清理工作，

#### 语句结尾：使用分号
> 有一件很有意思且很容易让人困惑的事情，那就是JavaScript的语句要么独占一行，要么以分号结尾。

自动分号插入机制ASI（Automatic Semicolon Insert）会自动寻找代码中应当使用分号但是实际上没有使用分号的位置,并插入分号。

```javascript
    function getData(){
        return
        {}
    }
    => return;{}
```
推荐总是使用分号：
- 当某个场景我们认为不需要插入分号而ASI认为需要插入时，常常会产生错误。
- Crockford的编程规范推荐总是使用分号，同样，jQuery核心风格指南、Google的JavaScript风格指南以及Dojo编程风格指南都推荐不要省略分号。

#### 行的最大长度: 80
> 如果一行代码太长，编辑窗口出现了横向滚动条，会让开发人员感觉很别扭。即便是在当今的宽屏显示器中，保持合适的代码行长度也会极大地提高工程师的生产力。
推荐一行不超过80：
- 很多语言的编程规范都提到一行代码最长不应当超过80个字符。这个数值来源于很久之前文本编辑器的单行最多字符限制，即编辑器中单行最多只能显示80个字符，超过80个字符的行要么折行，要么被隐藏起来，这些都是我们所不希望的。
+ 其他参考
- 1. Java语言编程规范中规定源码里单行长度不超过80个字符，文档中代码单行长度不超过70个字符。
- 2. Android开发者编码风格指南规定单行代码长度不超过100个字符。
- 3. 非官方的Ruby编程规范中规定单行代码长度不超过80个字符。
- 4. Python编程规范中规定单行代码长度不超过79个字符。

可选：80/100/120

#### 换行：两个层级的缩进
>当一行长度达到了单行最大字符数限制时，就需要手动将一行拆成两行。通常我们会在运算符后换行，下一行会增加两个层级的缩进。

```javascript 
// good：在运算符后换行，第二行追加两个缩进 ✅
callAFunction(document, element, window, "some string value", true, 123,
        navigator);

// bad：第二行只有一个缩进 ⚠️
callAFunction(document, element, window, "some string value", true, 123,
    navigator);

// bad：在运算符之前换行了 ⚠️
callAFunction(document, element, window, "some string value", true, 123
, navigator);
```

```javascript
let a = 'aaa';
    b = 'bbb';

// 用到一个变量
const { nameA } = objA; 

// 用到3个变量
const {
    nameB,nameBB,nameeBBB
} = objB; 

// 用到>3个变量
const {
    nameC,
    nameCC,
    nameCCC,
    nameCCC
} = objC; // 用到多于3个变量
```

- 在运算符后换行，第二行追加两个层级缩进
- 在赋值语句，第二行的位置应当和赋值运算符的位置保持对齐

#### 使用空行
>通常来讲，代码看起来应当像一系列可读的段落，而不是一大段揉在一起的连续文本。有时一段代码的语义和另一段代码不相关，这时就应该使用空行将它们分隔，确保语义有关联的代码展现在一起。

在下面这些场景中添加空行也是不错的主意:
1. 在方法之间
2. 在方法中的局部变量和第一条语句之间
3. 在多行或者单行注释之前
4. 在方法内的逻辑片段之间插入空行，提高可读性

另附书籍作者推荐风格:
1. 二元运算符前后必须使用一个空格来保持表达式的整洁
2. 使用括号时，紧接左括号之后和紧接右括号之前不应该有空格
```javascript
for(i=0; i<count; i++){
    process(i);
}
```

#### 命名规范
>“计算机科学只存在两个难题：缓存失效和命名。”——PhilKarlton。

命名原则:
1. 小驼峰
2. 变量名前缀用名词，方法名前缀用动词
3. 常量命名用大写字母和下划线
4. 构造函数首字母要大写

| 动词 | 含义 |
|-----------|----------|
|can | 函数返回一个布尔值 |
|has | 函数返回一个布尔值 |
|is  | 函数返回一个布尔值 |
|get | 函数返回一个非布尔值|
|set | 函数用来保存一个值 |

#### 直接量
使用原则：
1. 单引号或者双引号要保持一致
>我倾向于使用双引号，因为我经常在Java和JavaScript之间来回切换。由于Java只使用双引号括住符串，我发现如果在JavaScript中也使用这个约定，我会很容易在上下文之间相互切换。
2. 数字避免省略小数或者整数部分，避免八进制写法
3. null:空指针对象；undefined：变量未声明
4. 对象直接量：每个属性独占一行，并且保持一个缩进；最后的花括号也独占一行
```javascript
    var book = {
        title:'Javascript'
    }
```
5. 数组直接量：[] 代替 new Array()

#### 注释

什么情况下要注释：
- 难于理解的代码
- 可能被认为错误的代码
- 浏览器特性hack
- 文档注释：入参、出参

##### 单行注释"// xxx"：
- 注意：不应该连续使用多行单行注释，除非注释掉大段代码
- 独占一行的注释：与双斜线之间有个空格，缩进和下一行保持一致
- 行末尾的注释：代码结束到注释之间至少有一个缩进
- 大段代码注释
```javascript
    // 正确的注释
    if(isTrue){
       // 一系列处理
       handleData();
    }
```

##### 多行注释"/** xxx */":
推荐和java的一致风格：
```javascript
/** 我的注释 */
/**
 * 一段多行注释
 * 多行注释
 */
```

#### 语句块
##### 不论语句块包含多行代码还是单行代码，都要使用花括号
- 没有用花括号，这在Crockford的编程规范、jQuery核心风格指南、Google的JavaScript风格指南以及Dojo编程风格指南中都是明确禁止的。
- 省略花括号会造成一些困惑
```javascript
if (condition)
    doSomething();
    doSomethingElse();
```
##### 花括号的对齐方式
> 继承自Java,在Crockford的编程规范、jQuery核心风格指南、SproutCore编程风格指南、Google的JavaScript风格指南以及Dojo编程风格指南中都出现过。
```javascript
if (isTrue) {
     // 一些代码
}
```

##### 语句块间隔推荐：在括左圆括号之前和右圆括号之后各添加一个空格
>Crockford的编程规范和Google JavaScript风格指南所推荐。
```javascript
if (condition) {
    doSomething();
}
```
##### switch缩进推荐使用：
> Crockford的编程规范和Dojo编程风格指南则提倡的一种格式。
```javascript
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
```
注意：
- case的连续执行
- default不要省略,尽管什么都没做
>Douglas Crockford的JavaScript语言编程规范和Dojo编程风格指南将default作为它们标准的switch语句格式的组成部分。

#### 表达式规范
- with不应当继续使用
- for循环中避免使用continue，可以使用条件语句处理
- for-in循环：以键值做遍历，不仅遍历实例上的属性，还遍历从原型上继承来的属性。最好使用hasOwnPrototype()方法过滤。推荐使用Object.keys()
- for-in循环不能保证对象属性遍历的顺序
- 三元运算符：禁止嵌套(嵌套不易理解)
```javascript
const c = isA ? B : isC ? C : D;
```

#### 变量 、函数和运算符
##### 变量
不论var语句是否真的被执行，所有的var语句都会提前到包含这段逻辑的函数的顶部执行。因此推荐在函数顶部使用单var语句,每个变量的初始化应该独占一行，赋值运算符应当对齐。
```javascript
var value = 20,
    result = value + 10,
    i,
    len;
```

##### 函数
- 推荐总是先声明js函数然后使用函数
- 函数声明不应当出现在语句块之内
- 函数调用间隔:
>二元运算符前后必须使用一个空格来保持表达式的整洁;  使用括号时，紧接左括号之后和紧接右括号之前不应该有空格

```javascript
// 好的写法：单个好的写法
doSomething(item);
// 好的写法：多个参数
doSomething(item1, item2, item3);
// 不好的写法：看起来像一个块语句
doSomething (item);
```

##### 立即调用的函数
>为了让立即执行的函数能够被一眼看出来，可以将函数用一对圆括号包裹起来。
```javascript
// 推荐
(function(){}());
// 另一种写法
(function(){})()
```
##### 相等 ===
>由于JavaScript具有强制类型转换机制（type coercion），JavaScript中的判断相等操作是很微妙的。
```javascript
// 推荐使用 ====
```

#### 避免使用eval()
eval()会将传入的字符串当作代码来执行。开发者可以通过这个函数来载入外部的 JavaScript代码，或者随即生成JavaScript代码并执行它。使用Function构造函数亦可以做到这一点，setTimeout()和setInterval()也可以。

 尽管在JavaScript类库中eval()，可能会经常用到（通常和JSON操作有关），另外三种用法即使有也十分罕见。一个通用的原则是:
 - 严禁使用Function，并且只在别无他法时使用eval()。
 - setTimeout()和setInterval()也是可以使用的，但不要用字符串形式而要用函数。

 社区规范：
- Crockford的编程规范禁止使用eval()和Function，也禁止给setTimeout()和setInterval()传入字符串参数。jQuery核心风格指南禁止使用eval()，但有一个唯一的例外，即涉及到回调中解析JSON的情形。Google的JavaScript风格指南只允许在将Ajax的返回值转换为JavaScript值的场景下使用eval()。默认情况下，对于使用eval()、Function、setTimeout()和setInterval()的情形，JSLint和JSHint都会给出警告。

严格模式：
- ECMAScript 5严格模式对于eval()有着严格的限制，禁止在一个封闭的作用域中使用它创建新变量或者函数。这条限制帮助我们避免了eval()先天的安全漏洞。然而，如果实在没有别的方法来完成当前任务，这时依然推荐使用eval()。



## 二：编程实践

### UI层的松耦合

- 从CSS中抽离JS
- 从JS中抽离CSS：使用class作为通信的桥梁
- 从HTML中抽离JS：使用addEventListener
- 从JS中抽离HTML：从服务器加载或者客户端模版

### 避免使用全局变量：使用命名空间

> 单全局变量模式

    var maintainableJs = {};// 全局变量
    maintainableJs.book = {};// book -> namespace
    maintainableJs.color = {};//  another namespace

> 零全局变量模式

    立即执行的函数：适用于你的脚本非常短并且不需要和其他代码进行交互

### 事件处理

> 隔绝应用逻辑

    element.addEventListener('click',handleClick);
    function handleClick(e){
        // do something
    }

> 不要分发事件对象

    element.addEventListener('click',handleClick);
    function handleClick(e.clientX,e.clientY){
        this,shopPop(e.clientX,e.clientY);
    }

### 避免空比较

> 不好的做法：

- if(object[propertyName]){};
- if(object[propertyName] === null){};
- if(object[propertyName] === undefined){};

当属性值为假值（0 '' null false undefined）时，都会导致判断错误.
判断属性最好的方法是使用in运算符

### 将配置数据从代码中分离出来

配置数据：都是写死在代码里面的，并且将来可能被修改

### 抛出自定义错误

> 抛出错误的经验法则：

- 一旦修复了一个很难调试的问题，尝试增加一两个自定义错误。当再次发生错误时，有助于更好的解决问题
- 如果在编写代码，思考一下：我希望【某些事情】不会发生，如果发生我的代码会一团糟。这时候如果【某些事情】发生，就要抛出错误
- 如果正在编写的代码别人也会用，思考一下他们的使用方式，在特定的情况下抛出错误

### 不是你的对象你不要动

> 不推荐：
- 应该把一个已经存在的对象像工具函数库一样对待：
- 不覆盖方法
- 不新增方法
- 不删除方法

> 更好的方式：

- 使用继承，方法可以腹写不会影响继承原型

### 浏览器嗅探

- 对特定功能进行探测
- userAgent 判断移动端/PC

## 三：自动化（略）

## 更全面的推荐方案

[Airbnb](https://github.com/airbnb/javascript/blob/b4d8543f120ba761ae7f39caf850c1e4efdc2727/es5/README.md)


## 扩展阅读
1. 严格模式
2. ESLint风格对比