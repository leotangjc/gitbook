# ES6
***
### ECMAScript 和 JavaScript 的关系
ES6可以说是JS的规格、标准。
js是ES6的实现
***
### 部署进度
使用`node --v8-options | grep harmony`可以查看node已经实现的ES6特性
***
### Babel 转码器
使用Babel 转码器可以将ES6代码转为ES5代码，使用它，可以用ES6进行编写程序，转化之后，就不用担心兼容性的问题<br>
例:
```
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});```
Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。<br>
#### 配置文件.babelrc<br>
Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。

该文件用来设置转码规则和插件，基本格式如下。<br>
```
{
  "presets": [],
  "plugins": []
}
```
presets字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。<br>
```
# 最新转码规则
$ npm install --save-dev babel-preset-latest

# react 转码规则
$ npm install --save-dev babel-preset-react

# 不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```
然后，将这些规则加入.babelrc。<br>
```
  {
    "presets": [
      "latest",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```
注意，以下所有 Babel工具和模块的使用，都必须先写好.babelrc。<br>
#### 命令行转码babel-cli<br>
Babel提供babel-cli工具，用于命令行转码。<br>

它的安装命令如下。<br>
```
$ npm install --global babel-cli
```
基本用法如下。<br>
```
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```
上面代码是在全局环境下，进行 Babel 转码。这意味着，如果项目要运行，全局环境必须有 Babel，也就是说项目产生了对环境的依赖。另一方面，这样做也无法支持不同项目使用不同版本的 Babel。<br>
<br>
一个解决办法是将babel-cli安装在项目之中。<br>
```
# 安装
$ npm install --save-dev babel-cli
```
然后，改写package.json。<br>
```
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
```
转码的时候，就执行下面的命令。<br>
```$ npm run build```

***
***
# let 和 const 命令
***
### let命令
ES6中的let命令用来声明变量<br>
let类似于var，但是其声明的变量，只在let命令所在的代码块内有效<br>
* 比如在一个函数中用于循环计数时，使用let定义，可以有效避免变量名冲突
<br>

特性:
>##### 不存在变量提升<br>
var命令会发生”变量提升“现象，即变量可以在声明之前使用，值为undefined。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。<br>为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。<br>
>##### 暂时性死区<br>
只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。<br>
>##### 不允许重复声明<br>
let不允许在相同作用域内，重复声明同一个变量。<br>

***
### 块级作用域
***
* 有两种场景需要用到块级作用域：<br>
第一种场景，内层变量可能会覆盖外层变量。<br>
第二种场景，用来计数的循环变量泄露为全局变量。<br>
***
let定义的变量只在定义块以下生效<br>
* do 表达式<br>
本质上，块级作用域是一个语句，将多个操作封装在一起，没有返回值。<br>
只要在款及作用域钱加上do，使它变为do表达式<br>
***
### const命令<br>
* const声明一个只读的常量。一旦声明，常量的值就不能改变。<br>
* 作用域与let命令相同，只在声明所在的块级作用域内有效<br>
***
***
# 变量的解构赋值<br>
***
#### 数组的解构赋值<br>
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。<br>

以前，为变量赋值，只能直接指定值。<br>
```
let a = 1;
let b = 2;
let c = 3;```
ES6 允许写成下面这样。<br>
```
let [a, b, c] = [1, 2, 3];```
上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。<br>
***
#### 对象的解构赋值<br>
* 解构不仅可以用于数组，还可以用于对象。<br>
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
***
#### 字符串的解构赋值<br>
* 字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。<br>
* 非常不适应这个写法：<br>
```let {length : len} = 'hello';
len // 5```
***
#### 函数参数的解构赋值

`[[1, 2], [3, 4]].map(([a, b]) => a + b);`
***
#### 圆括号问题
* 对编译器来说，一个十字到底是模式，还是表达式，没有办法从一开始就知道，必须解析到等号才能知道<br>
由此带来的问题是，如果模式中出现圆括号怎么处理，ES6的规则是，只要有可能导致解构的企业，就不得使用圆括号<br>

##### 不能使用圆括号的情况
1. 变量声明语句

    ```

    let [(a)] = [1];

    let {x: (c)} = {};
    let ({x: c}) = {};
    let {(x: c)} = {};
    let {(x): c} = {};

    let { o: ({ p: p }) } = { o: { p: 2 } };
    ```
    上面6个语句都会报错，因为它们都是变量声明语句，模式不能使用圆括号。
  2. 函数参数
    函数参数也属于变量声明
  3. 赋值语句的模式
    圆括号将括号内的东西与外部隔开，使用不当的话，会报错

##### 可以使用圆括号的情况
可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。
***
### 用途
1. 交换变量的值

  例：

  ```
  let x = 1;
  let y = 2;
  [x, y] = [y, x];```
  这样交换x和y的值，简洁且易读
2. 函数参数的定义
  ES6简洁的书写方式，可以方便的将一组参数和变量名对应、结合起来
3. 从函数返回多个值
  函数只能返回一个值，如果要返回多个值，只能将他们放在数组或对象里返回。
4. 提取JSON数据
5. 函数参数的默认值
  设定默认值之后，就不用在函数体内再写
6. 遍历Map结构
  使用for...of循环获取值很便捷，如：
  `
  for (let 要取的东西 of 取值目标) {}`
