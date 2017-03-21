---
title: ES6--箭头函数
date: 2017-03-21 10:46:25
tags:
---

三个demo解释es6的箭头函数   
	 
		 {
	      ...
	      addAll: function addAll(pieces) {
	        var self = this;
	        _.each(pieces, function (piece) {
	          self.add(piece);
	        });
	      },
	      ...
	    }  
  


		 // ES6
		    {
		      ...
		      addAll: function addAll(pieces) {
		        _.each(pieces, piece => this.add(piece));
		      },
		      ...
		    }



		   // ES6的方法语法
		    {
		      ...
		      addAll(pieces) {
		        _.each(pieces, piece => this.add(piece));
		      },
		      ...
		    }

tips：
箭头函数与非箭头函数间还有一个细微的区别，箭头函数不会获取它们自己的arguments对象。诚然，在ES6中，你可能更多地会使用不定参数和默认参数值这些新特性。

    通过object.method()语法调用的方法使用非箭头函数定义，这些函数需要从调用者的作用域中获取一个有意义的this值。
    其它情况全都使用箭头函数。
