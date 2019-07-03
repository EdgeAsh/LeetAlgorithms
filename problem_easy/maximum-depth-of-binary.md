### 题目
```
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its depth = 3.
```
[leetcode原题](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

### 问题逐点分析
1. 数组表示二叉树，那么节点是怎么表示的？
> 父节点怎么表示？子节点呢，叶子节点有什么特征？
>> 根节点就是~~数组第一项~~；叶子节点=left,right都无
>> 这是一个愚蠢的问题，一个错问题；
如果数据给的不是正确的格式那根本无法读取(根本不是我应该考虑的问题，只需要知道数据是什么样就行！)！
这里给到的只是节点代表的值组成的数组

2. 求最深路径=父节点+1，最长的那一条怎么找？通过哪些特征找？
> 需要遍历二叉树


### 思路
需要栈结构
1. 第一个TreeNode入栈，判断left有没有值；有就入栈

### 代码
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
```

### 感想
~~二叉树居然是用数组表示的~~，平时看的图都是为了直观方便人理解(很抽象)。但在**代码里**可就大不一样了
**错**,二叉树不是用数组表示的！！！数据存储方式会展现出特定的规律=>抽象成二叉树

一开始就被给的数组给定死了，什么都往数组里去考虑。数据是什么样的都不清楚！！
