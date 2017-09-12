# EJS

***

## EJS特点
* 快速编译和渲染<br>
* 简单的模板标签<br>
* 自定义标记分隔符<br>
* 文件的包含<br>
* 支持浏览器段和服务器端<br>
* 模板静态缓存<br>
* 支持express视图系统<br>

***

ejs网页的主体使用`<SCRIPT>`标签是因为这个标签会被浏览器识别成脚本，运行其中内容，而不是直接显示

## EJS成员函数
* Render(str,data,[option}):直接渲染字符串，生成HTML标签<br>
  -str 需要解析的字符串<br>
  -data 数据<br>
  -option 配置选项<br>
      --Cache[boolean]:是否缓存(需要filename)<br>
      —-Filename [string]:缓存名称，会用作缓存的key<br>
      —-Context[object]:执行上下文函数<br>
      —-compileDebug[boolean]:标示是否编译debug，如果为true，将显示堆 栈信息<br>
      —-Client[boolean]:标示是否在客户端执行，如果为true,则返回函数<br>
      —-Delimiter[string]:指定分隔符，默认 “％”<br>
      —-Debug[boolean]:标示是否设置为debug状态，如果为true则会在控制台 显示生成函数源码<br>
      —-with[boolean]:是否使用"with(){}〃函数，如果为false,数据将会保存在 locals变量中<br>
* Compile(str.[option]):编译字符串得到模板数据<br>
      --str 需要解析的字符串<br>
      --option 配置选项<br>

***

## EJS常用标签
`<% %>流程控制标签<br>
  >判断循环  逻辑代码  <br>

<%= %>输出标签(原文输出HTML标签)<br>
  >将其中的内容输出到html(会对其中的代码进行转义)<br>

<%- %>输出标签(HTML会被浏览器解析)<br>
  >相比上面的方法，不会进行转义<br>

<%# %>注释标签<br>
% 对标记转义<br>
-%>去掉没用的空格`<br>


>app.set('名','值')
>app.get('名')//可以取到值
>可以设置路


## 过滤器
* 数值操作<br>
  plus(+)是在原始值上加<br>
  minus(-)减<br>
  times(+)乘<br>
  divided_by(/)除<br>
