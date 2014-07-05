title: "JSON知识整理"

date: 2014-07-05 21:15:41

tags: [JSON]
categories:
 JS
---
今天写公司移动项目接口时要用到JSON，借这个机会把过去一知半解的知识梳理一遍。
## 基本概念  

- JSON 即 **J**ava**S**cript **O**bject **N**otation
- JSON独立于语言  

## 将文本转换成JavaScript对象  

- JSON 文本格式在语法上与创建 JavaScript 对象的代码相同。
- 由于这种相似性，无需解析器，JavaScript 程序能够使用内建的 eval()函数，用 JSON 数据来生成原生的 JavaScript 对象。  

## JSON Value  

JSON值可以是:
- 数字(整数或浮点数)
- 字符串(在双引号中)
- 逻辑值(true 或 false)
- 数组(在方括号中)
- 对象(在花括号中)
- null

## JSON Object  

看例子`{ "foo":"Hello" , "bar":"World" }`
  
## JSON Array  

还是看例子 
```js
{"foo":[{ "foo":"Hello" , "bar":"World" },{ "foo":"Hello" , "bar":"World" }]}
```  

## JSON 使用 JavaScript语法  

看例子
```js
var json = {"foo":[{ "foo":"Hello" , "bar":"World" },   
                   { "foo":"Hello" , "bar":"World" }]}
```  
取值：  

```js
json.foo[0].bar;  
```  

修改:  

```js
json.foo[0].bar = 'BSP';  
```  

## JSON 实例  

创建一个包含JSON的JS String:  
```js
var json_string = "{"foo":[{ 'foo':'Hello' , 'bar':'World' },   
                   { 'foo':'Hello' , 'bar':'World' }]}";
```  
将字符串包含在括号中，用eval()函数生成JS对象: 
```js
var json = eval("("+json_string+")");
```  
**eval() 函数可编译并执行任何 JavaScript 代码。这之中有潜在的注入安全问题。**好在现代的浏览器提供了专门的JSON解析器。它只能识别文本，不进行编译，因此比eval函数更安全。  
> 最后一句我自己也不懂(๑>◡<๑) 
