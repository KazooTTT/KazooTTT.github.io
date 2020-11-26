---
layout: post
title: '[读书笔记]学习JavaScript数据结构与算法（第3版）'
sort: '读书笔记'
header-style: text
tags:
  - JavaScript
  - 数据结构与算法
  - 读书笔记
---
# 第1章 JavaScript简述

# 第2章 ECMAScript和TypeScript概述

1. ECMA是一个将信息标准化的组织。很久以前，JavaScript被提交到ECMA进行标准化，由此诞生了一个新的**语言标准**，也就是我们所知道的ECMAScript。JavaScript是该**标准**（最流行）的一个**实现**。
2. Babel是一个JavaScript转译器，也称为源代码编译器。它将使用了ECMAScript语言特性的JavaScript代码转换成只使用广泛支持的ES5特性的等价代码。

    [https://babeljs.io/repl/](https://babeljs.io/repl/)

3. const
    1. 对于非对象类型的变量，比如数、布尔值甚至字符串，我们不可以改变变量的值。
    2. 当遇到对象时，只读的const允许我们修改或重新赋值对象的属性，但变量本身的引用（内存中的引用地址）不可以修改，也就是不能对这个变量重新赋值。

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014523.png)

4.  ES2015引入了数组解构的概念

    ```jsx
    let [a,b] = [1,2];

    let a = 1;
    let b = 2;

    [a,b] = [b,a];
    // 等价于swap(a,b);

    let [x, y] = ['a', 'b'];
    let obj = {
      x,
      y
    };
    console.log(obj); // { x: "a", y: "b" }
    ```

5. 乘方运算符**  r*r*r 等价于 r**3
6. 【不懂】2.2.9 模块 (整体都不太懂)
    1. **node.js** require语句（CommonJS模块）
    2. 异步模块定义（AMD）
    3. RequireJS是AMD最流行的实现。
7. typscript
    1. 定义：TypeScript是一个开源的、渐进式包含类型的JavaScript超集，由微软创建并维护。
    2. 目的：让开发者增强JavaScript的能力并使应用的规模扩展变得更容易
    3. 功能：为JavaScript变量提供类型支持

# 第4章 栈

**先进后出**

【不懂】怎么写私有属性

## 十进制到n进制

要把十进制转化成二进制，我们可以将该十进制数除以2（二进制是满二进一）并对商取整，直到结果是0为止。

[https://res.weread.qq.com/wrepub/epub_26211966_88](https://res.weread.qq.com/wrepub/epub_26211966_88)

**504. 七进制数** 

[力扣](https://leetcode-cn.com/problems/base-7/)

我的方法

```jsx
var convertToBase7 = function(num) {
    if (num == 0) {
        return "0";
    }
    if (num < 0) {
        num = -num;
        var flag = 1;
    }
    var array = [];
    while (num > 0) {
        let res = num % 7;
        array.push(res);
        num = Math.floor(num / 7);
    }
    var str = "";
    for (let index = array.length - 1; index >= 0; index--) {
        str += array[index];
    }
    return flag == 1 ? "-" + str : str;
};
```

更简单的方法：

```jsx
var convertToBase7 = function(num) {
    return num.toString(7);
};
```

# 第5章 队列

队列是遵循**先进先出**（FIFO，也称为先来先服务）原则的一组有序的项。

队列在尾部添加新元素，并从顶部移除元素。最新添加的元素必须排在队列的末尾

1. 队列
2. 双端队列
3. 循环队列 —— 热土豆问题/约瑟夫问题/击鼓传花

## 循环队列的应用

### 1. 热土豆问题/约瑟夫问题/击鼓传花

```jsx
class Queue {
    constructor() {
        this.count = 0;
        this.top = 0;
        this.items = {};
    }
    enQueue(element) {
        this.items[this.count] = element;
        this.count++;
    }
    dnQueue() {
        var element = this.items[this.top];
        this.top++;
        return element;
    }
    size() {
        return this.count - this.top;
    }
}

function hotPotato(list, num) {
    var resultList = [];
    var queue = new Queue();
    list.forEach((element) => {
        queue.enQueue(element);
    });
    while (queue.size() > 1) {
        for (let index = 0; index < num; index++) {
            queue.enQueue(queue.dnQueue());
        }
        resultList.push(queue.dnQueue());
    }
    return {
        resultList: resultList,
        winner: queue.dnQueue(),
    };
}
```

其实直接用array.shift() 删除头部元素，并返回

array.push() 删除尾部元素

### 2. 回文检测

# 第6章 链表

1. 单向链表
    1. node node.next; node.element
    2. current 
    3. head
    4. tail
2. 双向链表
3. 循环链表
4. 有序链表

# 第7章 集合

不允许值重复的顺序数据结构

## 扩展运算符

有一种计算并集、交集和差集的简便方法，就是使用扩展运算符，它包含在ES2015中，

整个过程包含三个步骤：(1) 将集合转化为数组；(2) 执行需要的运算；(3) 将结果转化回集合。

对于集合a、b

1. 并集(比较简单)

```jsx
new Set([...a,...b]);
```

那么我们对setA使用扩展运算符（...setA）会将它的值转化为一个数组（展开它的值），然后对setB也这样做。

2. 交集

a.length < b.length (选择去遍历a, 这样简单)

```jsx
new Set([...a].filter((x) => b.has(x)));
```

不要使用in来判断元素是否在数组中

# 第8章 字典和散列表

处理散列中的冲突的方式：分离链接、线性探查和双散列法

1. 分离链接

    分离链接法包括为散列表的每一个位置创建一个链表并将元素存储在里面。它是解决冲突的最简单的方法，但是在HashTable实例之外还需要额外的存储空间。

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%201.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014539.png)

2. 线性探查

3. 双散列

# 第9章 递归

# 第10章 树

子节点、父节点 

叶子节点（外部节点）、内部节点

深度

二叉树 、二叉搜索树

遍历方式：

1. 中序
2. 前序
3. 后序

# 第11章 堆

定义：它是一棵完全二叉树，表示树的每一层都有左侧和右侧子节点（除了最后一层的叶节点），并且最后一层的叶节点尽可能都是左侧子节点，这叫作结构特性。

二叉堆是二叉树，但并不一定是二叉搜索树。

最小堆：所有的节点都**小于等于**每个它的子节点。

最大堆：所有的节点都**大于等于**每个它的子节点。

二叉树的表示方式：

1. 指针
2. 数组

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%202.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014544.png)

    对于index

    ❑ 它的左侧子节点的位置是2 * index+1（如果位置可用）；

    ❑ 它的右侧子节点的位置是2 * index+2（如果位置可用）；

    ❑ 它的父节点位置是index / 2（如果位置可用）。

对于最小堆来说（最大堆反着来）

堆主要操作：

1. insert(value) 插入新的值
2. extract() 移除最小值，并返回这个值。
3. findMinimum() 返回最小值

## 堆排序算法

# 第12章 图

### 一些概念：

一个图G=(V, E)由以下元素组成。

❑ V：一组顶点

❑ E：一组边，连接V中的顶点

**一个顶点的度**是其相邻顶点的数量。比如，A和其他三个顶点相连接，因此A的度为3; E和其他两个顶点相连，因此E的度为2。

路径是顶点v 1, v2,…, vk的一个连续序列，其中vi和vi+1是相邻的。以上一示意图中的图为例，其中包含路径A B E I和A C D G。

如果图中不存在环，则称该图是无环的。如果图中每两个顶点间都存在路径，则该图是连通的。

![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%203.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014546.png)

如果图中每两个顶点间在双向上都存在路径，则该图是强连通的。C和D是强连通的，而A和B不是强连通的。

## 图的表示

1. 图最常见的实现是**邻接矩阵**

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%204.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014549.png)

2. 邻接表

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%205.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014551.png)

3. 关联矩阵

    ![%E5%AD%A6%E4%B9%A0JavaScript%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%EF%BC%88%E7%AC%AC3%E7%89%88%EF%BC%89%20959b1a7c46f2467eb984fbc1e61599cf/Untitled%206.png](https://kazoottt-1256684243.cos.ap-chengdu.myqcloud.com/014555.png)

    **关联矩阵通常用于边的数量比顶点多的情况，以节省空间和内存（为啥？）**
