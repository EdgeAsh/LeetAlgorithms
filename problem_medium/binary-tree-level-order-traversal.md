### 题目
```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```
[leetcode原题](https://leetcode.com/problems/binary-tree-level-order-traversal/)

### 问题点
使用队列
1. 一层结束的标志是什么
  - 标志可以自定义，关键是什么时候放标志
2. 循环什么时候结束
  - 队列空时终止循环
3. 同层节点的子节点都已入队列的条件是什么
  - 队列首元素为null时，同层子节点都已入队列，队列尾入null

### 思路
层序遍历用队列；一层结束的标志是null
1. 将根节点入队列，再入null
2. 队首元素P出队列，P非null则取P值并且将P的子节点入队列；
3. 如果当前队列首元素为null,则上一层节点全被遍历，子节点都已入队列需加入结束标志;
4. 当队列为空时，终止循环
![层序遍历-BFS](../assets/binary-tree-traversal-bfs.gif);
[图源](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/tree/breadth-first-search)

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
 * @return {number[][]}
 */
var levelOrder = function(root) {
    if(!root) return []
    const queue = [root, null];
    let node = root
    let tempArr = [] // 存一层的值
    const arr = []
    while(queue.length) {
      node = queue.shift();
      if(node) {
        tempArr.push(node.val)
        if(node.left) queue.push(node.left)
        if(node.right) queue.push(node.right);
        if(!queue[0]) queue.push(null); // 若队列首元素非空，则同层元素未遍历完
      } else { // 一层结束
        if(tempArr.length) arr.push(tempArr)
        tempArr = []
      }
    }
    return arr
};
```
