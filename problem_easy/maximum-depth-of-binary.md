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
>> 根节点就是~~数组第一项~~；叶子节点是无子节点的节点
>> 这是一个愚蠢的问题，一个错问题；
如果数据给的不是正确的格式那根本无法读取(根本不是我应该考虑的问题，只需要知道数据是什么样就行！)！
这里给到的只是节点代表的值组成的数组

2. 求最深路径=父节点+1，最长的那一条怎么找？通过哪些特征找？
> 需要遍历二叉树，也就是层序遍历，每层结束深度加一

### 思路
递归求深度
从叶子节点开始算起，左右子节点的深度，返回大值
递归的话就是从叶子节点开始考虑了，或者以三节点(父-左-右)为单位考虑问题

[层序遍历](../problem_medium/binary-tree-level-order-traversal.md)求深度
1. 使用队列
2. 首先将根节点入队，再入null(层尾标志)
3. 队首元素P出队，如过P是节点则将其子节点入队列；判断队列首元素是否为null如是则表明目前P是上一层最后一个节点，需要为下一层加入结尾标志
4. 循环，直到队列为空

### 代码
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 * 递归
 */
var maxDepth = function(root) {
    if(!root) return 0;
    if(!root.left && !root.right) return 1;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right))
}

/**
 * @param {TreeNode} root
 * @return {number}
 * 层序遍历
 */
var maxDepth = function(root) {
    if(!root) return 0;
    const queue = [root, null];
    let node = root;
    let deep = 0;
    while(queue.length) {
      node = queue.shift()
      if(node) {
        if(node.left) queue.push(node.left);
        if(node.right) queue.push(node.right);
        if(!queue[0] && queue.lenght > 1) queue.push(null) // 这一步会使循环多一次
      } else { // 一层结束
        deep++ // 双null使deep多+1
      }
    }
    return deep - 1
};
```

### 感想
~~二叉树居然是用数组表示的~~，平时看的图都是为了直观方便人理解(很抽象)。但在**代码里**可就大不一样了
**错**,二叉树不是用数组表示的！！！数据存储方式会展现出特定的规律=>抽象成二叉树

一开始就被给的数组给定死了，什么都往数组里去考虑。数据是什么样的都不清楚！！

如果一开始就看别人思路，那自己就被限定死了；不过有优点，速度快；
所以，需要自己确定看别人思路的时机
