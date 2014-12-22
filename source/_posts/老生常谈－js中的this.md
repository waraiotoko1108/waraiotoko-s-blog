title: "老生常谈－js中的this"   
date: 2014-09-19 23:37:29  

tags: [html5 js]  
categories:
  js
---
为了战胜拖延症，今天来总结一下Javascript中的this关键字。  
> Javascript中this将永远是指向调用它的对象。		－－W3School  

## 看例一 纯代码解释对象方法调用  
	var x =1;
	function testThis(){
		console.log(this.x);
	}
	testThis();
	//这个例子中声明了一个全局变量x和一个全局方法（函数），上述两个对象都绑定在Window上，因此当执行testThis()时this就是当前环境对象Window，结果是1。  
	var o={};
	o.x = 5;
	o.method = testThis;
	o.method();
	//此时this指向o，因此结果是5。    
	
  对象调用方法的时候，方法里面的this就是指向调用他或者是拥有他的对象。
## 例子二 慢慢解释构造函数创建
	var x = 2;
	function test(){
		this.x = 1;
	}
	
	var o = new test();
	console.log(o.x);
	//Javascript中的构造函数，通过new来创建一个实例，此时this为对象o，因此结果是1。
	//下面这个例子是Angular(快忘了！！！)中的Service
	app.service("MyService",function(){
		this.test = function(){
			console.log(this);
			test2();
		}
		function test2(){
			console.log(this);		
		}
	}
		MyService.test();		//结果为MyService{test: function}和Window{}
	);
	//test2()是MyService的闭包（closure）。
	
## 改变this的指向  
	function test() {
		console.log(this.x);
	}
	var o = {};
	o.x = 1;
	o.m = test;
	
	o.m.apply({x:5});	//5
	o.m.call();		//undefine
	
	//apply与call懂可以制定调用函数的上下文，默认是Global;
	
可以看到this的指向是不确定的，this值在进入上下文时确定，并且在上下文运行期间永久不变。上面的例子改变this的上下文，导致两次结果不一致也是最好的证据。   

## 解决之道  
血泪的教训：  
1. Angular要将属性和方法给你提供一个$scope来绑定属性。  
2. 在js实践中不妨定义"val self = this"，在之后的作用域里面用self来操作对象的属性。
	
**收工睡觉**
	