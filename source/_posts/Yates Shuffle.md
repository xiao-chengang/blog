---
title: Fisher–Yates Shuffle洗牌算法
date: 2018-01-21 15:36:04
tags: 
- javaScript 
- 算法
categories: javaScript
---
# Fisher–Yates Shuffle洗牌算法
如果你想跟朋友一起玩德州扑克的话，你应该先洗牌，以随机的牌序来确保一个公平的游戏。但是怎么做呢？

有一个简单而有效的做法就是把牌随机选一叠放到另一边，形成一个新的牌堆，并且重复这一步。只要你从剩余的牌堆中随机选出来的牌的概率是相等的，那么你就会得到一个完美且公平的牌堆。如图1所示(**译注：为了不影响阅读，我把gif图都放到了文章末尾**)。

假设这不是一副实体的牌，你可能想写一段代码，用内存中的n个元素来做同样的事情。听起来很简单(某种程度上)，但你如何从最初的牌堆中精确的选择一个随机的剩余的元素？
<!---more--->
有一个很慢的方法：从开始的地方，在数组中(在[0, n - 1]中)选择一个随机的元素，然后判断是否已经是被打乱了。这个方法可以运行，但是随着剩余元素的减少会变得越来越慢，你会一直选择已经被打乱的元素。观察那些导致洗牌变慢的重复的选择（红色）。如图2所示。

这里有一段用JavaScript实现的代码，但是你不应该使用它。

```js
    function shuffle(array) {
      var copy = [], n = array.length, i;

      // 如果还有剩余的需要打乱的元素...
      while (n) {

        // 选择一个剩余的元素
        i = Math.floor(Math.random() * array.length);

        // 如果已经打乱，把它移动到新的数组
        if (i in array) {
          copy.push(array[i]);
          delete array[i];
          n--;
        }
      }

      return copy;
    }
```

这个实现是不好的，我们能够做的更好。你可以只选择剩余的元素，避免重复选择。在[0, m - 1]之间选择一个随机数，在每一次循环后，m也会随着n的递减而递减。换句话说，m指的是需要打乱的剩余的元素。当你移动卡牌的时候并且合并剩余的牌，因此你能够很容易的选出下一张要洗的牌。如图3所示。

```js
    function shuffle(array) {
      var copy = [], n = array.length, i;

      // 如果还有剩余的需要打乱的元素...
      while (n) {

        // 选择一个剩余的元素
        i = Math.floor(Math.random() * n--);

        // 把它移动到新的数组
        copy.push(array.splice(i, 1)[0]);
      }

      return copy;
    }
```

这段程序运行的非常好，但是还能再次优化性能。主要的问题是当你从原始数组中移动每个元素(array.splice)，你不得不移动该元素后续的所有元素，平均来说，打乱每个元素需要移动n/2个元素。复杂度是 O(n<sup>2</sup>)

但是有一个非常有意思的地方，如果你认真的观察：每一个被打乱过的元素的数量(n - m)加上剩余的元素的数量(m)会一直等于总长度n。这意味着我们可以原地洗牌，不需要额外的空间！我们在数组的后面的部分存储打乱过的元素，在数组的前面的部分存储剩余的元素。我们不需要关心剩余元素的顺序，只要我们在选择的时候样本一致！

为了实现这个O(n)复杂度的原地洗牌算法，随机选择一个剩余的元素(从数组的前面)，然后放在新的位置(数组的后面)，还未被打乱的元素交换到数组前面，如图4所示。

``` js
    function shuffle(array) {
      var m = array.length, t, i;

      // 如果还有剩余的需要打乱的元素...
      while (m) {

        // 选择一个剩余的元素
        i = Math.floor(Math.random() * m--);

        // 和当前元素交换
        [array[i],array[m]]=[array[m],array[i]]
      }

      return array;
    }
```

更多的关于Fisher–Yates shuffle内容请看[Wikipedia article](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)和Jeff Atwood的文章[The Danger of Naïveté](http://www.codinghorror.com/blog/2007/12/the-danger-of-naivete.html)。

---------------------------------------
图1
![demo1.gif](http://7xo525.com1.z0.glb.clouddn.com/demo1.gif)
---------------------------------------
图2
![demo2.gif](http://7xo525.com1.z0.glb.clouddn.com/demo2.gif)
---------------------------------------
图3
![demo3.gif](http://7xo525.com1.z0.glb.clouddn.com/demo3.gif)
---------------------------------------
图4
![demo4.gif](http://7xo525.com1.z0.glb.clouddn.com/demo4.gif)


>原文地址 [Fisher–Yates Shuffle](https://bost.ocks.org/mike/shuffle/)