### 题目
```
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

  Given nums = [1,1,2],

  Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

  It doesn't matter what you leave beyond the returned length.
Example 2:

  Given nums = [0,0,1,1,1,2,2,3,3,4],

  Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

  It doesn't matter what values are set beyond the returned length.
Clarification:

  Confused why the returned value is an integer but your answer is an array?

  Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

  Internally you can think of this:

    // nums is passed in by reference. (i.e., without making a copy)
    int len = removeDuplicates(nums);

    // any modification to nums in your function would be known by the caller.
    // using the length returned by your function, it prints the first len elements.
    for (int i = 0; i < len; i++) {
        print(nums[i]);
    }
```
[leetcode原题](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

### 思路
![26.remove-duplicates-from-sorted-array](../assets/26.remove-duplicates-from-sorted-array.gif)
双指针，当前指针(a)固定，另一指针(b)向前遍历。
如果b指向的值与a不相同，则a、b往前挪,并且b处值要复制到a处；
b指向的值与a相同，a不动,b走一步
注意比较值的时候，不要比错

### 代码
 v暂存a指针**最新的**值
```
function removeDul(arr) {
  let a = 0
  let v = arr[a]
  for(let i = 0, j = arr.length; i < j; i++) {
    if (v !== arr[i]) {
      v = arr[i]
      a = a + 1;
      arr[a] = v;
    }
  }
  return a + 1;
}
```
