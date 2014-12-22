title: "Javscript Event研究（2）"

date: 2014-08-28 13:37:29  

tags: [html5 js]  
categories:
  js
---
 拖延了10天，今天继续Javascript Event研究( ͡° ͜ʖ ͡°) 。  
 
## DOM事件  
[例子点我](http://sandbox.runjs.cn/show/ij4rih6x)  

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <style type="text/css">
         #p { width: 300px; height: 300px; padding: 10px;  border: 1px solid black; }
         #c { width: 100px; height: 100px; border: 1px solid red; }
    </style>
</head>
<body>
    <div id="p">
        parent
        <div id="c">
            child
        </div>
    </div>
    <script type="text/javascript">
        var p = document.getElementById('p'),
        c = document.getElementById('c');
        c.addEventListener('click', function () {
            alert('子节点捕获')
        }, true);

        c.addEventListener('click', function () {
            alert('子节点冒泡')
        }, false);

        p.addEventListener('click', function () {
            alert('父节点捕获')
        }, true);

        p.addEventListener('click', function () {
            alert('父节点冒泡')
        }, false);
    </script>
</body>
</html>
```   

解释一下：   
- 点击parent，事件首先再document上然后parent捕获到事件，处于目标阶段然后event.target也等于parent，此时可以认为捕获事件结束。  
- 当currentTarget与target相同时，js就处于处理目标阶段，之后开始冒泡，执行冒泡事件。   
- 点击child情况有所不同，事件由document传向parent执行事件，然后传向child最后开始冒泡。  

## 事件对象  
>所谓事件对象，是与特定对象相关，并且包含该事件详细信息的对象。
 
各个事件的事件参数不一样，比如鼠标事件就会有相关坐标，包含和创建他的特定事件有关的属性和方法，触发的事件不一样，参数也不一样（比如鼠标事件就会有坐标信息）。比较重要的有一下几个   
1. bubbles    
	- 事件是否冒泡   
2. cancelable    
	- 事件是否可以取消默认行为
3. currentTarget    
4. defaultPrevent   
	- 为true表明已经调用了preventDefault     
5. eventPhase       
	- 调用事件处理程序的阶段：1 捕获；2 处于阶段；3 冒泡阶段（需要打断点查看）
6. traget		
	- 事件目标		    
7. trusted    
8. type		
9. view			
10. preventDefault		
	- 取消事件默认行为，cancelable是true时可以使用	   
11. stopPropagation		
	- 取消事件捕获/冒泡，bubbles为true才能使用		
12. stopImmediatePropagation		
	- 取消事件进一步冒泡，并且组织任何事件处理程序被调用
13. createEvent			

> 现在是上班时间，所以剩下的以后再写。（╯－＿－）╯╧╧
> 真相是拖延症又犯了。。。。。	



   
 

