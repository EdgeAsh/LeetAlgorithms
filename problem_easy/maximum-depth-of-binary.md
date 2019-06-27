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

### 问题逐点分析
1. 数组表示二叉树，那么节点是怎么表示的？
> 父节点怎么表示？子节点呢，叶子节点有什么特征？
>> 根节点就是数组第一项
2. 求最深路径=父节点+1，最长的那一条怎么找？通过哪些特征找？
> 需要遍历二叉树


### 思路

### 代码

### 感想
二叉树居然是用数组表示的，平时看的图都是为了直观方便人理解。但在计算机里可就大不一样了
