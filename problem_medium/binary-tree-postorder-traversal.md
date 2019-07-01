### 题目
```
Given a binary tree, return the postorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
Follow up: Recursive solution is trivial, could you do it iteratively?
```

### 思路
后序遍历就是`左-右-根`
1. 递归方式
   - 读取左节点值，右节点值，最后是根节点；想象成只有三个节点时的处理方式，然后对每个节点都使用同一个函数处理
2. 利用栈结构，属于leetcode困难程度；节点入栈顺序是`根-右-左`
   - 根节点入栈
   - 

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
 * @return {number[]}
 * 递归方式
 */
var postorderTraversal = function(root, arr = []) {
   if(!root) return []
   if(root.left) {
      postorderTraversal(root.left, arr)
   }

   if(root.right) {
      postorderTraversal(root.right, arr)
   }
   arr.push(root.val)
   return arr
};

/**
 * @param {TreeNode} root
 * @return {number[]}
 * 利用栈结构
 */
var postorderTraversal = function(root, arr = []) {
   
};
```
