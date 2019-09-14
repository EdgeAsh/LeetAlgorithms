# 基础的排序算法，共十种
按时间复杂度分成三类，每种算法的特点包括是否稳定，in/out-place.

## 时间复杂度O(N^2)

### 插入排序(in-place)(稳定)
它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入  
采用`in-place排序`，即在原容器里排序

#### js代码
测试数组[3,6,8,2,7,9,1,5,4]
默认按升序排列
```js
/**
 * 从第二位元素开始，第一位做比较。
 * 如果需要插入的元素(arr[i])并不在有序部分的末尾，则需要考虑清楚挪位的问题
*/

function insertionSort(arr) {
    // 从数组第二位开始，第一位不用排
    for(let i=1; i<arr.length; i++) {
        let n = i;
        let m = n - 1; // m,n用来挪位
        let temp = arr[i]; // 要被插入的数
        while(temp < arr[m]) {
            arr[n] = arr[m]; // 挪位
            arr[m] = temp;
            n--;
            m = n - 1;
            if(m < 0) break;
        }
    }
    return arr
}
```

### 选择排序(in-place)(不稳定)

### 希尔排序(in-place)(不稳定)

### 冒泡排序(in-place)(稳定)

## 时间复杂度O(NlogN)

### 归并排序(out-place)(稳定)
是分治思想的典型例子。

三个主要步骤：  
分：将复杂问题分解成若干元问题  
治：处理元问题  
合：将元问题的解合成复杂问题的解  

分解的函数divide将原始数组一分为二，递归下去，直到数组不可再分
合并是另一个函数merge，接收两个参数。是两个数组，将两个数组合并成一个(排序在此)
注意较长的数组处理

递归怎么用还是不好想的

#### js代码
```js
function merge(leftArr, rightArr){  
    var result = [];  
    while (leftArr.length > 0 && rightArr.length > 0){  
      if (leftArr[0] < rightArr[0])  
        result.push(leftArr.shift()); //把最小的最先取出，放到结果集中   
      else   
        result.push(rightArr.shift());  
    }   
    return result.concat(leftArr).concat(rightArr);  //剩下的就是合并，这样就排好序了  
}  

function divide(array){  
    if (array.length == 1) return array;  
    var middle = array.length>>1       //求出中点  
    var left = array.slice(0, middle);               //分割数组  
    var right = array.slice(middle);  
    return merge(divide(left), divide(right)); //递归合并与排序  
}  

var arr = divide([32,12,56,78,76,45,36]);
console.log(arr);   // [12, 32, 36, 45, 56, 76, 78]
```

### 堆排序(in-place)(不稳定)

### 快速排序(in-place)(稳定)


## 时间复杂度O(N)

### 桶排序(out-place)(稳定)

### 计数排序(out-place)(稳定)

### 基数排序(out-place)(稳定)


## 相关概念
稳定与不稳定是怎么分的？


in-place是指在原数组上排序
