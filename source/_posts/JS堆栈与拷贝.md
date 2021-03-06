---
title: JS堆栈与拷贝
date: 2017-03-16 12:09:16
tags: 深拷贝 浅拷贝

---
1、栈（stack）和堆（heap）

　　stack为自动分配的内存空间，它由系统自动释放；而heap则是动态分配的内存，大小不定也不会自动释放。　　　　　　　

2、基本类型和引用类型

　　基本类型：存放在栈内存中的简单数据段，数据大小确定，内存空间大小可以分配。

　　5种基本数据类型有Undefined、Null、Boolean、Number 和 String，它们是直接按值存放的，所以可以直接访问。

　　引用类型：存放在堆内存中的对象，变量实际保存的是一个指针，这个指针指向另一个位置。每个空间大小不一样，要根据情况开进行特定的分配。

　　当我们需要访问引用类型（如对象，数组，函数等）的值时，首先从栈中获得该对象的地址指针，然后再从堆内存中取得所需的数据。

3、传值与传址

　　前面之所以要说明什么是内存中的堆、栈以及变量类型，实际上是为下文服务的，就是为了更好的理解什么是“浅拷贝”和“深拷贝”。

　　基本类型与引用类型最大的区别实际就是传值与传址的区别。测试用例：
复制代码
	
	 1     var a = [1,2,3,4,5];
	 2     var b = a;
	 3     var c = a[0];
	 4     alert(b);//1,2,3,4,5
	 5     alert(c);//1
	 6     //改变数值        
	 7     b[4] = 6;
	 8     c = 7;
	 9     alert(a[4]);//6
	10     alert(a[0]);//1

复制代码

　　从上面我们可以得知，当我改变b中的数据时，a中数据也发生了变化；但是当我改变c的数据值时，a却没有发生改变。

　　这就是传值与传址的区别。因为a是数组，属于引用类型，所以它赋予给b的时候传的是栈中的地址（相当于新建了一个不同名“指针”），而不是堆内存中的对象。而c仅仅是从a堆内存中获取的一个数据值，并保存在栈中。所以b修改的时候，会根据地址回到a堆中修改，c则直接在栈中修改，并且不能指向a堆内存中。

3、浅拷贝

　　前面已经提到，在定义一个对象或数组时，变量存放的往往只是一个地址。当我们使用对象拷贝时，如果属性是对象或数组时，这时候我们传递的也只是一个地址。因此子对象在访问该属性时，会根据地址回溯到父对象指向的堆内存中，即父子对象发生了关联，两者的属性值会指向同一内存空间。
复制代码
	
	 1 　　var a = {
	 2         key1:"11111"
	 3     }
	 4     function Copy(p) {
	 5         var c = {};
	 6         for (var i in p) { 
	 7         　　c[i] = p[i];
	 8         }
	 9         return c;
	10 　　}
	11     a.key2 = ['小辉','小辉'];
	12     var b = Copy(a);
	13 　　 b.key3 = '33333';
	14     alert(b.key1);     //1111111
	15     alert(b.key3);    //33333
	16     alert(a.key3);    //undefined

复制代码

　　a对象中key1属性是字符串，key2属性是数组。a拷贝到b，12属性均顺利拷贝。给b对象新增一个字符串类型的属性key3时，b能正常修改，而a中无定义。说明子对象的key3（基本类型）并没有关联到父对象中，所以undefined。

1 b.key2.push("大辉");
2 alert(b.key2);    //小辉，小辉，大辉
3 alert(a.key2);    //小辉，小辉，大辉

　　但是，若修改的属性变为对象或数组时，那么父子对象之间就会发生关联。从以上弹出结果可知，我对b对象进行修改，a、b的key2属性值（数组）均发生了改变。其在内存的状态，可以用下图来表示。

　　原因是key1的值属于基本类型，所以拷贝的时候传递的就是该数据段；但是key2的值是堆内存中的对象，所以key2在拷贝的时候传递的是指向key2对象的地址，无论复制多少个key2，其值始终是指向父对象的key2对象的内存空间。

4、深拷贝

 　　或许以上并不是我们在实际编码中想要的结果，我们不希望父子对象之间产生关联，那么这时候可以用到深拷贝。既然属性值类型是数组和或象时只会传址，那么我们就用递归来解决这个问题，把父对象中所有属于对象的属性类型都遍历赋给子对象即可。测试代码如下：
复制代码

	 1 　　function Copy(p, c) {
	 2         var c = c || {};
	 3         for (var i in p) {
	 4         　　if (typeof p[i] === 'object') {
	 5         　　　　　c[i] = (p[i].constructor === Array) ? [] : {};
	 6         　　　　　Copy(p[i], c[i]);
	 7         　　} else {
	 8         　　　　　c[i] = p[i];
	 9         　　}
	10         }
	11         return c;
	12 　　}    
	13     a.key2 = ['小辉','小辉'];
	14     var b={};
	15     b = Copy(a,b);        
	16     b.key2.push("大辉");
	17     alert(b.key2);    //小辉，小辉，大辉
	18     alert(a.key2);    //小辉，小辉

复制代码

　　由上可知，修改b的key2数组时，没有使a父对象中的key2数组新增一个值，即子对象没有影响到父对象a中的key2。其存储模式大致如下：

出处：
[关于JS堆栈与拷贝](http://www.cnblogs.com/chengguanhui/p/4737413.html)