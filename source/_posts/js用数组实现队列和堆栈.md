---
title: js用数组实现队列和堆栈
date: 2017-03-15 22:52:52
tags:js 队列 堆栈

---
#feature
##基本概念
队列：FIFO （先进先出)
堆栈：LIFO (后进先出)
###js数组方法
shift:从数组中把第一个元素删除，并返回这个元素的值。
		shift有数据移位的意思 数组执行shift相当于把整个数组向前移动。

unshift: 在数组的开头添加一个或更多元素，并返回新的长度
反shift
push:在数组的中末尾添加元素，并返回新的长度
正常插入数组

pop:从数组中把最后一个元素删除，并返回这个元素的值。
用于倒序输出
###队列实现demo  

 	//创建一个数组来模拟队列
        var a=new Array();
        console.log(a);
        //unshift: 在数组的开头添加一个或更多元素，并返回新的长度
        console.log("入队");
       							a.unshift(1)
        console.log(a);//----->1
       							a.unshift(2);
        console.log(a);//----->2,1
        						a.unshift(3);
        console.log(a);//----->3,2,1
       							 a.unshift(4);
        console.log(a);//----->4,3,2,1
        console.log("出队，先进先出");
        console.log(a);
        //pop：从数组中把最后一个元素删除，并返回这个元素的值
        a.pop();//----->1
        console.log(a);
        a.pop();//----->2
        console.log(a);
        a.pop();//----->3
        console.log(a);
        a.pop();//----->4
        console.log(a);
###实现堆栈
	//创建一个数组来模拟堆栈
	        var a=new Array();
	        console.log(a);
	        //push: 在数组的末尾添加一个或更多元素，并返回新的长度
	        console.log("入栈");
	        a.push(1)
	        console.log(a);//----->1
	        a.push(2);
	        console.log(a);//----->1,2
	        a.push(3);
	        console.log(a);//----->1,2,3
	        a.push(4);
	        console.log(a);//----->1,2,3,4
	        console.log("出栈，后进先出");
	        console.log(a);
	        //pop：从数组中把最后一个元素删除，并返回这个元素的值
	        a.pop();//----->4
	        console.log(a);
	        a.pop();//----->3
	        console.log(a);
	        a.pop();//----->2
	        console.log(a);
	        a.pop();//----->1
	        console.log(a);