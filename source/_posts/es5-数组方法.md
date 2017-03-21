---
title: ES5--数组方法
date: 2017-03-21 12:17:20
tags:
---
>数组方法一直都在用，最近在学习ES6的时候，发现这些数组方法都是ES5的标准，故统一整理一下。

ES5中新增的数组方法，如下：

    forEach (js v1.6)
    map (js v1.6)
    filter (js v1.6)
    some (js v1.6)
    every (js v1.6)
    indexOf (js v1.6)
    lastIndexOf (js v1.6)
    reduce (js v1.8)
    reduceRight (js v1.8)

浏览器支持

    Opera 11+
    Firefox 3.6+
    Safari 5+
    Chrome 8+
    Internet Explorer 9+
##feature
###forEach
forEach是Array新方法中最基本的一个，就是遍历，循环。例如下面这个例子：

    [1, 2 ,3, 4].forEach(alert);

等同于下面这个传统的for循环：

    var array = [1, 2, 3, 4];

    for (var k = 0, length = array.length; k < length; k++) {
      alert(array[k]);
    }

Array在ES5新增的方法中，参数都是function类型，默认有传参。
forEach方法中的function回调支持3个参数。  
第1个是遍历的数组内容； 第2个是对应的数组索引，第3个是数组本身。
因此，我们有：

    [].forEach(function(value, index, array) {
        // ...
    });

对比jQuery中的$.each方法：

    $.each([], function(index, value, array) {
        // ...
    });
会发现，第1个和第2个参数正好是相反的，大家要注意了，不要记错了。后面类似的方法，例如$.map也是如此。

现在，我们就可以使用forEach卖弄一个稍显完整的例子了，数组求和：

    var sum = 0;

    [1, 2, 3, 4].forEach(function (item, index, array) {
      console.log(array[index] == item); // true
      sum += item;
    });

    alert(sum); // 10

再下面，更进一步，forEach除了接受一个必须的回调函数参数，还可以接受一个可选的上下文参数（改变回调函数里面的this指向）（第2个参数）。

    array.forEach(callback,[ thisObject])
 例子更能说明一切：

    var database = {
      users: ["张含韵", "江一燕", "李小璐"],
      sendEmail: function (user) {
        if (this.isValidUser(user)) {
          console.log("你好，" + user);
        } else {
          console.log("抱歉，"+ user +"，你不是本家人");	
        }
      },
      isValidUser: function (user) {
        return /^张/.test(user);
      }
    };

    // 给每个人法邮件
    database.users.forEach(  // database.users中人遍历
      database.sendEmail,    // 发送邮件
      database               // 使用database代替上面标红的this
    );

    // 结果：
    // 你好，张含韵
    // 抱歉，江一燕，你不是本家人
    // 抱歉，李小璐，你不是本家

    如果这第2个可选参数不指定，则使用全局对象代替（在浏览器是为window），严格模式下甚至是undefined.

另外，forEach不会遍历纯粹“占着官位吃空饷”的元素的，例如下面这个例子：

    var array = [1, 2, 3];

    delete array[1]; // 移除 2
    alert(array); // "1,,3"

    alert(array.length); // but the length is still 3

    array.forEach(alert); // 弹出的仅仅是1和3

###map
这里的map不是“地图”的意思，而是指“映射”。[].map(); 基本用法跟forEach方法类似：

    array.map(callback,[ thisObject]);

callback的参数也类似：

    [].map(function(value, index, array) {
        // ...
    });

map方法的作用不难理解，“映射”嘛，也就是原数组被“映射”成对应新数组。下面这个例子是数值项求平方：

    var data = [1, 2, 3, 4];

    var arrayOfSquares = data.map(function (item) {
      return item * item;
    });

    alert(arrayOfSquares); // 1, 4, 9, 16
callback需要有return值，如果没有，就会发生下面这样的问题：

    var data = [1, 2, 3, 4];
    var arrayOfSquares = data.map(function() {});

    arrayOfSquares.forEach(console.log);

结果如下图，可以看到，数组所有项都被映射成了undefined：
全部项都成了undefined

在实际使用的时候，我们可以利用map方法方便获得对象数组中的特定属性值们。例如下面这个例子（之后的兼容demo也是该例子）：

    var users = [
      {name: "张含韵", "email": "zhang@email.com"},
      {name: "江一燕",   "email": "jiang@email.com"},
      {name: "李小璐",  "email": "li@email.com"}
    ];

    var emails = users.map(function (user) { return user.email; });

   
###filter
filter为“过滤”、“筛选”之意。指数组filter后，返回过滤后的新数组。用法跟map极为相似：

    array.filter(callback,[ thisObject]);
filter的callback函数需要返回布尔值true或false. 如果为true则表示，恭喜你，通过啦！如果为false, 只能高歌“我只能无情地将你抛弃……”。

可能会疑问，一定要是Boolean值吗？我们可以简单测试下嘛，如下：

    var data = [0, 1, 2, 3];
    var arrayFilter = data.filter(function(item) {
        return item;
    });
    console.log(arrayFilter); // [1, 2, 3]

有此可见，*返回值只要是弱等于== true/false就可以了*，而非非得返回 === true/false.
 

###some
some意指“某些”，指是否“某些项”合乎条件。与下面的every算是好基友，every表示是否“每一项”都要靠谱。用法如下：

    array.some(callback,[ thisObject]);

例如下面的简单使用：

    var scores = [5, 8, 3, 10];
    var current = 7;

    function higherThanCurrent(score) {
      return score > current;
    }

    if (scores.some(higherThanCurrent)) {
      alert("朕准了！");
    }

结果弹出了“朕准了”文字。 some要求至少有1个值让callback返回true就可以了。显然，8 > 7，因此scores.some(higherThanCurrent)值为true.
我们自然可以使用forEach进行判断，不过，相比some, 不足在于，***some只有有true即返回不再执行了。***

###indexOf
indexOf方法在字符串中自古就有，string.indexOf(searchString, position)。数组这里的indexOf方法与之类似。

    array.indexOf(searchElement[, fromIndex])

返回整数索引值，如果没有匹配（严格匹配），返回-1. fromIndex可选，表示从这个位置开始搜索，若缺省或格式不合要求，使用默认值0，我在FireFox下测试，发现使用字符串数值也是可以的，例如"3"和3都可以。

    var data = [2, 5, 7, 3, 5];

    console.log(data.indexOf(5, "x")); // 1 ("x"被忽略)
    console.log(data.indexOf(5, "3")); // 4 (从3号位开始搜索)

    console.log(data.indexOf(4)); // -1 (未找到)
    console.log(data.indexOf("5")); // -1 (未找到，因为5 !== "5")

  
###lastIndexOf
lastIndexOf方法与indexOf方法类似：

    array.lastIndexOf(searchElement[, fromIndex])

只是lastIndexOf是从字符串的末尾开始查找，而不是从开头。还有一个不同就是fromIndex的默认值是array.length - 1而不是0.

  
##reduce
reduce是JavaScript 1.8中才引入的，中文意思为“减少”、“约简”。不过，从功能来看，我个人是无法与“减少”这种含义联系起来的，反而更接近于“迭代”、“递归(recursion)”，擦，因为单词这么接近，不会是ECMA-262 5th制定者笔误写错了吧~~

此方法相比上面的方法都复杂，用法如下：

    array.reduce(callback[, initialValue])

callback函数接受4个参数：之前值、当前值、索引值以及数组本身。initialValue参数可选，表示初始值。若指定，则当作最初使用的previous值；如果缺省，则使用数组的第一个元素作为previous初始值，同时current往后排一位，相比有initialValue值少一次迭代。

    var sum = [1, 2, 3, 4].reduce(function (previous, current, index, array) {
      return previous + current;
    });

    console.log(sum); // 10

说明：
        因为initialValue不存在，因此一开始的previous值等于数组的第一个元素。
        从而current值在第一次调用的时候就是2.
        最后两个参数为索引值index以及数组本身array.

以下为循环执行过程：

    // 初始设置
    previous = initialValue = 1, current = 2

    // 第一次迭代
    previous = (1 + 2) =  3, current = 3

    // 第二次迭代
    previous = (3 + 3) =  6, current = 4

    // 第三次迭代
    previous = (6 + 4) =  10, current = undefined (退出)

    有了reduce，我们可以轻松实现二维数组的扁平化：

    var matrix = [
      [1, 2],
      [3, 4],
      [5, 6]
    ];

    // 二维数组扁平化
    var flatten = matrix.reduce(function (previous, current) {
      return previous.concat(current);
    });

    console.log(flatten); // [1, 2, 3, 4, 5, 6]


###reduceRight
reduceRight跟reduce相比，用法类似：

    array.reduceRight(callback[, initialValue])

实现上差异在于reduceRight是从数组的末尾开始实现。看下面这个例子：

    var data = [1, 2, 3, 4];
    var specialDiff = data.reduceRight(function (previous, current, index) {
      if (index == 0) {
        return previous + current;
      }
      return previous - current;
    });

    console.log(specialDiff); // 0
结果0是如何得到的呢？
我们一步一步查看循环执行：

    // 初始设置
    index = 3, previous = initialValue = 4, current = 3

    // 第一次迭代
    index = 2, previous = (4- 3) = 1, current = 2

    // 第二次迭代
    index = 1, previous = (1 - 2) = -1, current = 1

    // 第三次迭代
    index = 0, previous = (-1 + 1) = 0, current = undefined (退出)


三、更进一步的应用

我们还可以将上面这些数组方法应用在其他对象上。

例如，我们使用forEach遍历DOM元素。

	var eleDivs = document.getElementsByTagName("div");
	Array.prototype.forEach.call(eleDivs, function(div) {
	    console.log("该div类名是：" + (div.className || "空"));
	});

可以输出页面所有div的类名，您可以狠狠地点击这里：Array新方法forEach遍历DOM demo
出处:[张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2013/04/es5%e6%96%b0%e5%a2%9e%e6%95%b0%e7%bb%84%e6%96%b9%e6%b3%95/) 