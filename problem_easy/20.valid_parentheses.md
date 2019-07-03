### 题目
```
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
  1.Open brackets must be closed by the same type of brackets.
  2.Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

Example 1:
  Input: "()"
  Output: true

Example 2:
  Input: "()[]{}"
  Output: true

Example 3:
  Input: "(]"
  Output: false

Example 4:
  Input: "([)]"
  Output: false

Example 5:
  Input: "{[]}"
  Output: true
```
[leetcode原题](https://leetcode.com/problems/valid-parentheses/description/)

### 思路
使用栈结构，符号先入栈，遇到匹配的出栈；全部匹配的话，str遍历之后栈内就是空的


### 代码
```
function validParen(str){
  let stack = []
  let obj = str.split('')
  let match = {
    '(': ')',
    '[': ']',
    '{': '}',
  }
  
  for(let i = 0; i < obj.length; i++) {
    // 确定符号左部分，如果是undefined，说明是符号右侧部分
    let itm = match[obj[i]]
    if (itm) {
      stack.push(obj[i])
    } else if(match[stack.pop()] === obj[i]) { // pop会返回最后一位，不需要length-1那种读取方式
      // stack末位匹配当前符号
      // stack.pop()
    } else {
      return false
    }
  }
  return stack.length === 0
}
```
