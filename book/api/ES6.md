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
let是最明显的局部变量<br>
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
    上面6个语句都会报错，因为它们都是变量声明语句，模式不能使用圆括号。<br>
  2. 函数参数<br>
    函数参数也属于变量声明<br>
  3. 赋值语句的模式<br>
    圆括号将括号内的东西与外部隔开，使用不当的话，会报错<br>

##### 可以使用圆括号的情况
可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。
***
### 用途
1. 交换变量的值<br>
  例：

  ```
  let x = 1;
  let y = 2;
  [x, y] = [y, x];```
  这样交换x和y的值，简洁且易读<br>
2. 函数参数的定义<br>
  ES6简洁的书写方式，可以方便的将一组参数和变量名对应、结合起来<br>
3. 从函数返回多个值<br>
  函数只能返回一个值，如果要返回多个值，只能将他们放在数组或对象里返回。<br>
4. 提取JSON数据<br>
5. 函数参数的默认值<br>
  设定默认值之后，就不用在函数体内再写<br>
6. 遍历Map结构<br>
  使用for...of循环获取值很便捷，如：<br>
  `
  for (let 要取的东西 of 取值目标) {}`
7. 输入模块的指定方法

***
# 函数的拓展
  * ##### 属性的简洁表示法
  **ES6 允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。**<br>
  变量声明、属性、方法都可以简写<br>
  例：<br>
  ```
  var birth = '2000/01/01';        
  var Person = {
    name: '张三',
    //等同于birth: birth
    birth,
    // 等同于hello: function ()...
    hello() { console.log('我的名字是', this.name); }
    };```

  * ##### 属性名表达式
  **JavaScript语言定义对象的属性，有两种方法。**
  ```
  // 方法一
  obj.foo = true;
  // 方法二
  obj['a' + 'bc'] = 123;```
  方法一是直接用标识符作为属性名<br>
  方法二是用表达式作为属性名，这时要将表达式放在方括号之内。<br>
  * ##### 方法的name属性<br>
  **函数的name属性，返回函数名。对象方法也是函数，因此也有name属性。**<br>
  ```
  const person = {
  sayName() {
    console.log('hello!');
    },
  };

  person.sayName.name   // "sayName"```
  上面代码中，方法的name属性返回函数名（即方法名）<br>
  * ##### Object.is()
  **它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。**<br>
  例：<br>
  ```
  Object.is('foo', 'foo')
  // true
  Object.is({}, {})
  // false```
  >ES5比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0。JavaScript缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。<br>
  ES6提出“Same-value equality”（同值相等）算法，用来解决这个问题。Object.is就是部署这个算法的新方法。<br>
  * ##### Object.is()
  **Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。**
  ```
  var target = { a: 1 };
  var source1 = { b: 2 };
  var source2 = { c: 3 };

  Object.assign(target, source1, source2);
  target // {a:1, b:2, c:3}```
  Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。
  >常见用途<br>
  （1）为对象添加属性<br>
  ```
  class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
  }```
  上面方法通过Object.assign方法，将x属性和y属性添加到Point类的对象实例。<br>
  （2）为对象添加方法<br>
  ```
  Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
  });```
  // 等同于下面的写法
  ```
  SomeClass.prototype.someMethod = function (arg1, arg2) {···};<br>
  SomeClass.prototype.anotherMethod = function () {···};```<br>
  上面代码使用了对象属性的简洁表示法，直接将两个函数放在大括号中，再使用assign方法添加到SomeClass.prototype之中。<br>
  （3）克隆对象<br>
  ```
  function clone(origin) {
  return Object.assign({}, origin);
    }```
  上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆。
  不过，采用这种方法克隆，只能克隆原始对象自身的值，不能克隆它继承的值。如果想要保持继承链，可以采用下面的代码。
  ```
  function clone(origin) {
  let originProto = Object.getPrototypeOf(origin);
  return Object.assign(Object.create(originProto), origin);
  }```
  （4）合并多个对象<br>
  将多个对象合并到某个对象。<br>
  ```
  const merge =
  (target, ...sources) => Object.assign(target, ...sources);```
  如果希望合并后返回一个新对象，可以改写上面函数，对一个空对象合并。
  ```
  const merge =
  (...sources) => Object.assign({}, ...sources);```
  （5）为属性指定默认值<br>
    ```
    const DEFAULTS = {
      logLevel: 0,
      outputFormat: 'html'
    };
    function processContent(options) {
      options = Object.assign({}, DEFAULTS, options);
        console.log(options);
        // ...
        }```
  上面代码中，DEFAULTS对象是默认值，options对象是用户提供的参数。Object.assign方法将DEFAULTS和options合并成一个新对象，如果两者有同名属性，则option的属性值会覆盖DEFAULTS的属性值。<br>
  注意，由于存在浅拷贝的问题，DEFAULTS对象和options对象的所有属性的值，最好都是简单类型，不要指向另一个对象。否则，DEFAULTS对象的该属性很可能不起作用。<br>
  ```
  const DEFAULTS = {
    url: {
      host: 'example.com',
      port: 7070
      },
    };
    processContent({ url: {port: 8000} })
    // {
      //   url: {port: 8000}
      // }```
  上面代码的原意是将url.port改成8000，url.host不变。实际结果却是options.url覆盖掉DEFAULTS.url，所以url.host就不存在了。<br>
  * ##### 属性的可枚举性<br>
  **对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。<br>
  Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象。**<br>
  例：<br>
  ```
  let obj = { foo: 123 };
  Object.getOwnPropertyDescriptor(obj, 'foo')
  //  {
  //    value: 123,
  //    writable: true,
  //    enumerable: true,
  //    configurable: true
  //  }```
  描述对象的enumerable属性，称为”可枚举性“，如果该属性为false，就表示某些操作会忽略当前属性。<br>
  ES6 新增了一个操作Object.assign()，会忽略enumerable为false的属性，只拷贝对象自身的可枚举的属性。<br>
  * ##### 属性的遍历
  ES6 一共有5种方法可以遍历对象的属性。<br>

  1. for...in<br>
  for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。<br>
  2. Object.keys(obj)<br>
  Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）。<br>
  3. Object.getOwnPropertyNames(obj)<br>
  Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）。<br>
  4. Object.getOwnPropertySymbols(obj)<br>
  Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性。<br>
  5. Reflect.ownKeys(obj)<br>
  Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管属性名是 Symbol 或字符串，也不管是否可枚举。<br>
  <br>
  以上的5种方法遍历对象的属性，都遵守同样的属性遍历的次序规则。<br>
    * 首先遍历所有属性名为数值的属性，按照数字排序。<br>
    * 其次遍历所有属性名为字符串的属性，按照生成时间排序。<br>
    * 最后遍历所有属性名为 Symbol 值的属性，按照生成时间排序。<br>

  ```
  Reflect.ownKeys({ [Symbol()]:0, b:0, 10:0, 2:0, a:0 })
  // ['2', '10', 'b', 'a', Symbol()]```

  上面代码中，Reflect.ownKeys方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的，首先是数值属性2和10，其次是字符串属性b和a，最后是 Symbol 属性。<br>
***
# 对象的拓展
  * ##### 属性的简洁表示法<br>
  **ES6 允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。**<br>
  ```
  var foo = 'bar';
  var baz = {foo};
  baz // {foo: "bar"}

  // 等同于
  var baz = {foo: foo};```
  上面代码表明，ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。<br>
  * ##### 属性名表达式
  JavaScript语言定义对象的属性，有两种方法。<br>
  ```
  // 方法一
  obj.foo = true;
  // 方法二
  obj['a' + 'bc'] = 123;```
  方法一是直接用标识符作为属性名<br>
  方法二是用表达式作为属性名，这时要将表达式放在方括号之内。<br>
  * ##### 方法的 name 属性<br>
  函数的name属性，返回函数名。对象方法也是函数，因此也有name属性。<br>
  例：
  ```
  const person = {
    sayName() {
    console.log('hello!');
    },
  };

  person.sayName.name   // "sayName"```
  上面代码中，方法的name属性返回函数名（即方法名）。<br>

  * ##### Object.is()<br>
  **它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。**<br>
  ES5比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0。JavaScript缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。<br>
  ```
  Object.is('foo', 'foo')
  // true
  Object.is({}, {})
  // false```

  * ##### Object.assign()<br>
  **Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。**
  ```
  var target = { a: 1 };

  var source1 = { b: 2 };
  var source2 = { c: 3 };

  Object.assign(target, source1, source2);
  target // {a:1, b:2, c:3}```
  Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。<br>

  * ##### 常见用途<br>
  （1）为对象添加属性<br>
  ```
  class Point {
    constructor(x, y) {
      Object.assign(this, {x, y});
    }
  }```
  上面方法通过Object.assign方法，将x属性和y属性添加到Point类的对象实例。<br>
  （2）为对象添加方法<br>
  ```
  Object.assign(SomeClass.prototype, {
    someMethod(arg1, arg2) {
      ···
      },
      anotherMethod() {
        ···
      }
      });```
      // 等同于下面的写法
      ```
      SomeClass.prototype.someMethod = function (arg1, arg2) {
        ···
      };
      SomeClass.prototype.anotherMethod = function () {
        ···
      };```
      上面代码使用了对象属性的简洁表示法，直接将两个函数放在大括号中，再使用assign方法添加到SomeClass.prototype之中。<br>
  （3）克隆对象<br>
  ```
  function clone(origin) {
    return Object.assign({}, origin);
    }```
    上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆。<br><br>

    不过，采用这种方法克隆，只能克隆原始对象自身的值，不能克隆它继承的值。如果想要保持继承链，可以采用下面的代码。<br>
    ```
    function clone(origin) {
      let originProto = Object.getPrototypeOf(origin);
      return Object.assign(Object.create(originProto), origin);
    }```
  （4）合并多个对象<br>
  将多个对象合并到某个对象。<br>
  ```
  const merge =
  (target, ...sources) => Object.assign(target, ...sources);```
  如果希望合并后返回一个新对象，可以改写上面函数，对一个空对象合并。<br>
  ```
  const merge =
  (...sources) => Object.assign({}, ...sources);```
  （5）为属性指定默认值<br>
  ```
  const DEFAULTS = {
    logLevel: 0,
    outputFormat: 'html'
  };
  function processContent(options) {
    options = Object.assign({}, DEFAULTS, options);
      console.log(options);
      // ...
    }```
    上面代码中，DEFAULTS对象是默认值，options对象是用户提供的参数。Object.assign方法将DEFAULTS和options合并成一个新对象，如果两者有同名属性，则option的属性值会覆盖DEFAULTS的属性值<br><br>

    注意，由于存在浅拷贝的问题，DEFAULTS对象和options对象的所有属性的值，最好都是简单类型，不要指向另一个对象。否则，DEFAULTS对象的该属性很可能不起作用。<br>
    ```
    const DEFAULTS = {
      url: {
        host: 'example.com',
        port: 7070
        },
      };

      processContent({ url: {port: 8000} })
      // {
        //   url: {port: 8000}
        // }```
    上面代码的原意是将url.port改成8000，url.host不变。实际结果却是options.url覆盖掉DEFAULTS.url，所以url.host就不存在了。<br>
***
# 数组的拓展
  * #### 扩展运算符
  **含义**<br>
  扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。<br>
  例：
  ```
  function push(array, ...items) {
    array.push(...items);
  }

  function add(x, y) {
    return x + y;
  }

  var numbers = [4, 38];
  add(...numbers) // 42```
  上面代码中，array.push(...items)和add(...numbers)这两行，都是函数的调用，它们的都使用了扩展运算符。该运算符将一个数组，变为参数序列
  * #### 替代数组的apply方法
  **由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了。**
  ```
  // ES5 的写法
  Math.max.apply(null, [14, 3, 77])

  // ES6 的写法
  Math.max(...[14, 3, 77])

  // 等同于
  Math.max(14, 3, 77);```
  上面代码中，由于 JavaScript 不提供求数组最大元素的函数，所以只能套用Math.max函数，将数组转为一个参数序列，然后求最大值。有了扩展运算符以后，就可以直接用Math.max了。
  * #### 扩展运算符的应用
    1. 合并数组
    2. 与解构赋值结合
    3. 函数的返回值
    4. 字符串
    5. 实现了 Iterator 接口的对象
    6. Map 和 Set 结构，Generator 函数
  * #### Array.from()
  **Array.from方法用于将两类对象转为真正的数组：类似数组的对象和可遍历的对象。**
  * #### Array.of()
  Array.of方法用于将一组值，转换为数组。
  ```
  Array.of(3, 11, 8) // [3,11,8]
  Array.of(3) // [3]
  Array.of(3).length // 1```
  这个方法的主要目的，是弥补数组构造函数Array()的不足。因为参数个数的不同，会导致Array()的行为有差异。
  * #### 数组实例的 find() 和 findIndex()
  数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。
  ```
  [1, 4, -5, 10].find((n) => n < 0)
  // -5```
  上面代码找出数组中第一个小于0的成员。
  * #### 数组实例的fill()
  fill方法使用给定值，填充一个数组。
  ```
  ['a', 'b', 'c'].fill(7)
  // [7, 7, 7]

  new Array(3).fill(7)
  // [7, 7, 7]```
  上面代码表明，fill方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。
  * #### 数组实例的 entries()，keys() 和 values()
  **ES6 提供三个新的方法——entries()，keys()和values()——用于遍历数组。**它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
  ```
  for (let index of ['a', 'b'].keys()) {
    console.log(index);
  }
  // 0
  // 1

  for (let elem of ['a', 'b'].values()) {
    console.log(elem);
  }
  // 'a'
  // 'b'

  for (let [index, elem] of ['a', 'b'].entries()) {
    console.log(index, elem);
  }
  // 0 "a"
  // 1 "b"```
  如果不使用for...of循环，可以手动调用遍历器对象的next方法，进行遍历。
  * #### 数组实例的 includes()
  Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。ES2016 引入了该方法。
  ```
  [1, 2, 3].includes(2)     // true
  [1, 2, 3].includes(4)     // false
  [1, 2, NaN].includes(NaN) // true```
  该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。
  * #### 数组的空位
  数组的空位指，数组的某一个位置没有任何值。比如，Array构造函数返回的数组都是空位。
  ```
  Array(3) // [, , ,]```
  上面代码中，Array(3)返回一个具有3个空位的数组。
***
# Promise对象
  * #### Promise 的含义
  Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象。
  所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。
    * Promise对象有以下两个特点:
      1. **对象的状态不受外界影响。**Promise对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和Rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
      2. **一旦状态改变，就不会再变，任何时候都可以得到这个结果。**Promise对象的状态改变，只有两种可能：从Pending变为Resolved和从Pending变为Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。


  > <font size=1>有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。<br><br>
  Promise也有一些缺点。首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。<br><br>
  如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择。<br>

  * #### Promise 的含义
  ES6 规定，Promise对象是一个构造函数，用来生成Promise实例。
  下面代码创造了一个Promise实例。
  ```
  var promise = new Promise(function(resolve, reject) {
    // ... some code

    if (/* 异步操作成功 */){
      resolve(value);
      } else {
        reject(error);
      }
      });```

  Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。
  * #### Promise.prototype.then()
  Promise 实例具有then方法，也就是说，then方法是定义在原型对象Promise.prototype上的。它的作用是为 Promise 实例添加状态改变时的回调函数。前面说过，then方法的第一个参数是Resolved状态的回调函数，第二个参数（可选）是Rejected状态的回调函数。

  then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。

  ```
  getJSON("/posts.json").then(function(json) {
    return json.post;
    }).then(function(post) {
      // ...
      });```
  上面的代码使用then方法，依次指定了两个回调函数。第一个回调函数完成以后，会将返回结果作为参数，传入第二个回调函数。
  * #### Promise.prototype.catch()
  Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。

  ```
  getJSON('/posts.json').then(function(posts) {
    // ...
  }).catch(function(error) {
    // 处理 getJSON 和 前一个回调函数运行时发生的错误
    console.log('发生错误！', error);
  });```
  上面代码中，getJSON方法返回一个 Promise 对象，如果该对象状态变为Resolved，则会调用then方法指定的回调函数；如果异步操作抛出错误，状态就会变为Rejected，就会调用catch方法指定的回调函数，处理这个错误。另外，then方法指定的回调函数，如果运行中抛出错误，也会被catch方法捕获。
  * #### Promise.all()
  Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。
  ```
  var p = Promise.all([p1, p2, p3]);```
  上面代码中，Promise.all方法接受一个数组作为参数，p1、p2、p3都是 Promise 实例，如果不是，就会先调用下面讲到的Promise.resolve方法，将参数转为 Promise 实例，再进一步处理。
  * #### Promise.race()
  Promise.race方法同样是将多个Promise实例，包装成一个新的Promise实例。
  ```
  var p = Promise.race([p1, p2, p3]);```
  上面代码中，只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。
  * #### Promise.resolve()
  有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。
  ```
  var jsPromise = Promise.resolve($.ajax('/whatever.json'));```
  上面代码将jQuery生成的deferred对象，转为一个新的Promise对象。
    * Promise.resolve方法的参数分成四种情况。
    1. 参数是一个Promise实例
    如果参数是Promise实例，那么Promise.resolve将不做任何修改、原封不动地返回这个实例。
    2. 参数是一个thenable对象
    thenable对象指的是具有then方法的对象，比如下面这个对象。

  推荐的两个有用的方法：
    * **done()**
      Promise对象的回调链，不管以then方法或catch方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为Promise内部的错误不会冒泡到全局）。因此，我们可以提供一个done方法，总是处于回调链的尾端，保证抛出任何可能出现的错误。
    * **finally()**
      finally方法用于指定不管Promise对象最后状态如何，都会执行的操作。它与done方法的最大区别，它接受一个普通的回调函数作为参数，该函数不管怎样都必须执行。
***
# Async
  **含义**
  ES2017 标准引入了 async 函数，使得异步操作变得更加方便。
  async 函数是什么？一句话，它就是 Generator 函数的语法糖。
  * #### 基本用法
  async函数返回一个 Promise 对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。
  例:
  ```
  async function getStockPriceByName(name) {
    var symbol = await getStockSymbol(name);
    var stockPrice = await getStockPrice(symbol);
    return stockPrice;
  }

  getStockPriceByName('goog').then(function (result) {
    console.log(result);
  });```
  上面代码是一个获取股票报价的函数，函数前面的async关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个Promise对象。
  * #### 语法
    * 返回 Promise 对象
      async函数返回一个 Promise 对象。
      async函数内部return语句返回的值，会成为then方法回调函数的参数。
      ```
      async function f() {
        return 'hello world';
      }

      f().then(v => console.log(v))
      // "hello world"```
      上面代码中，函数f内部return命令返回的值，会被then方法回调函数接收到。
    * Promise 对象的状态变化
    async函数返回的 Promise 对象，必须等到内部所有await命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到return语句或者抛出错误。也就是说，只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数。
    例:
    ```
    async function getTitle(url) {
      let response = await fetch(url);
      let html = await response.text();
      return html.match(/<title>([\s\S]+)<\/title>/i)[1];
    }
    getTitle('https://tc39.github.io/ecma262/').then(console.log)
    // "ECMAScript 2017 Language Specification"```
    上面代码中，函数getTitle内部有三个操作：抓取网页、取出文本、匹配页面标题。只有这三个操作全部完成，才会执行then方法里面的console.log。
    * await 命令
    正常情况下，await命令后面是一个 Promise 对象。如果不是，会被转成一个立即resolve的 Promise 对象。
    ```
    async function f() {
      return await 123;
    }

    f().then(v => console.log(v))
    // 123```
    上面代码中，await命令的参数是数值123，它被转成 Promise 对象，并立即resolve。
    * 错误处理
    如果await后面的异步操作出错，那么等同于async函数返回的 Promise 对象被reject。
    ```
    async function f() {
      await new Promise(function (resolve, reject) {
        throw new Error('出错了');
        });
      }
      f()
      .then(v => console.log(v))
      .catch(e => console.log(e))
      // Error：出错了```
    上面代码中，async函数f执行后，await后面的 Promise 对象会抛出一个错误对象，导致catch方法的回调函数被调用，它的参数就是抛出的错误对象。具体的执行机制，可以参考后文的“async 函数的实现原理”。
    例：
    假定某个 DOM 元素上面，部署了一系列的动画，前一个动画结束，才能开始后一个。如果当中有一个动画出错，就不再往下执行，返回上一个成功执行的动画的返回值。
    ```
    async function chainAnimationsAsync(elem, animations) {
      var ret = null;
      try {
        for(var anim of animations) {
          ret = await anim(elem);
        }
        } catch(e) {
          /* 忽略错误，继续执行 */
        }
        return ret;
      }```
  * #### for await...of
  前面介绍过，for...of循环用于遍历同步的 Iterator 接口。新引入的for await...of循环，则是用于遍历异步的 Iterator 接口。
  ```
  async function f() {
    for await (const x of createAsyncIterable(['a', 'b'])) {
      console.log(x);
    }
  }
  // a
  // b```
  上面代码中，createAsyncIterable()返回一个异步遍历器，for...of循环自动调用这个遍历器的next方法，会得到一个Promise对象。await用来处理这个Promise对象，一旦resolve，就把得到的值（x）传入for...of的循环体。

      >yield* 语句
      yield*语句也可以跟一个异步遍历器。
      async function* gen1() {
        yield 'a';
        yield 'b';
        return 2;
        }   
        async function* gen2() {
        // result 最终会等于 2
        const result = yield* gen1();
        }
      上面代码中，gen2函数里面的result变量，最后的值是2。
      与同步 Generator 函数一样，for await...of循环会展开yield*。
        (async function () {
        for await (const x of gen2()) {
          console.log(x);
        }
        })();
        // a
        // b
***
# Class的基本用法
  <font size=1>基本上，ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
  例：
  生成实例对象
    ```
    class Point {
    constructor(x, y) {
      this.x = x;
      this.y = y;
    }

    toString() {
      return '(' + this.x + ', ' + this.y + ')';
    }
  }```
  对比传统写法
    ```
    function Point(x, y) {
      this.x = x;
      this.y = y;
    }

    Point.prototype.toString = function () {
      return '(' + this.x + ', ' + this.y + ')';
    };

    var p = new Point(1, 2);```
  * #### 严格模式
  **ES6只有严格模式可以使用**
  * #### constructor 方法
  constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加。
  ```
  class Point {
  }

  // 等同于
  class Point {
    constructor() {}
  }```
  上面代码中，定义了一个空的类Point，JavaScript 引擎会自动为它添加一个空的constructor方法。
  * ####类的实例对象
  生成类的实例对象的写法，与 ES5 完全一样，也是使用new命令。前面说过，如果忘记加上new，像函数那样调用Class，将会报错。
  * #### Class表达式
  与函数一样，类也可以使用表达式的形式定义。
    ```
    const MyClass = class Me {
      getClassName() {
        return Me.name;
      }
    };```
  上面代码使用表达式定义了一个类。需要注意的是，这个类的名字是MyClass而不是Me，Me只在 Class 的内部代码可用，指代当前类。
  * #### 不存在变量提升
  ES6中不会吧类的声明提升到代码头部，所以如果在声明前调用，就会出
  * #### 私有方法 ？？？？？
  * #### 私有属性 ？？？？？
  * #### this的指向
  类的方法内部如果含有this，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错。
  ```
  class Logger {
    printName(name = 'there') {
      this.print(`Hello ${name}`);
    }

    print(text) {
      console.log(text);
    }
  }

  const logger = new Logger();
  const { printName } = logger;
  printName(); // TypeError: Cannot read property 'print' of undefined```
  上面代码中，printName方法中的this，默认指向Logger类的实例。但是，如果将这个方法提取出来单独使用，this会指向该方法运行时所在的环境，因为找不到print方法而导致报错
  * #### Class 的取值函数（getter）和存值函数（setter） § ⇧
  与 ES5 一样，在“类”的内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。
  ```
  class MyClass {
    constructor() {
      // ...
    }
    get prop() {
      return 'getter';
    }
    set prop(value) {
      console.log('setter: '+value);
    }
  }

  let inst = new MyClass();

  inst.prop = 123;
  // setter: 123

  inst.prop
  // 'getter'```
  上面代码中，prop属性有对应的存值函数和取值函数，因此赋值和读取行为都被自定义了。
  * #### Class 的 Generator 方法 § ⇧
  如果某个方法之前加上星号（*），就表示该方法是一个 Generator 函数。
  ```
  class Foo {
    constructor(...args) {
      this.args = args;
    }
    * [Symbol.iterator]() {
      for (let arg of this.args) {
        yield arg;
      }
    }
  }

  for (let x of new Foo('hello', 'world')) {
    console.log(x);
  }
  // hello
  // world```
  上面代码中，Foo类的Symbol.iterator方法前有一个星号，表示该方法是一个 Generator 函数。Symbol.iterator方法返回一个Foo类的默认遍历器，for...of循环会自动调用这个遍历器。
  * #### Class 的 Generator 方法 § ⇧
如果某个方法之前加上星号（*），就表示该方法是一个 Generator 函数。

class Foo {
  constructor(...args) {
    this.args = args;
  }
  * [Symbol.iterator]() {
    for (let arg of this.args) {
      yield arg;
    }
  }
}

for (let x of new Foo('hello', 'world')) {
  console.log(x);
}
// hello
// world
上面代码中，Foo类的Symbol.iterator方法前有一个星号，表示该方法是一个 Generator 函数。Symbol.iterator方法返回一个Foo类的默认遍历器，for...of循环会自动调用这个遍历器。
***
# Class继承
  class可以通过extends关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。
  ```
  class Point {
  }

  class ColorPoint extends Point {
  }```
  上面代码定义了一个ColorPoint类，该类通过extends关键字，继承了Point类的所有属性和方法。但是由于没有部署任何代码，所以这两个类完全一样，等于复制了一个Point类。下面，我们在ColorPoint内部加上代码。
  * #### Object.getPrototypeOf()
  Object.getPrototypeOf方法可以用来从子类上获取父类。
  ```
  Object.getPrototypeOf(ColorPoint) === Point
  // true```
  因此，可以使用这个方法判断，一个类是否继承了另一个类。
  * #### super 关键字
  super这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

        1. 第一种情况，super作为函数调用时，代表父类的构造函数。ES6 要求，子类的构造函数必须执行一次super函数。
        ```
        class A {}
        class B extends A {
          constructor() {
            super();
          }
        }```
        上面代码中，子类B的构造函数之中的super()，代表调用父类的构造函数。这是必须的，否则 JavaScript 引擎会报错。
        2. 第二种情况，super作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。
            ```
            class A {
              p() {
                return 2;
              }
            }

            class B extends A {
              constructor() {
                super();
                console.log(super.p()); // 2
              }
            }

            let b = new B();```
            上面代码中，子类B当中的super.p()，就是将super当作一个对象使用。这时，super在普通方法之中，指向A.prototype，所以super.p()就相当于A.prototype.p()。
