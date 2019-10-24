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
    let result = [];  
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
    let middle = array.length>>1       //求出中点  
    let left = array.slice(0, middle);               //分割数组  
    let right = array.slice(middle);  
    return merge(divide(left), divide(right)); //递归合并与排序  
}  

let arr = divide([32,12,56,78,76,45,36]);
console.log(arr);   // [12, 32, 36, 45, 56, 76, 78]
```

### 堆排序(in-place)(不稳定) TODO  
有关堆的知识[在这](../basic-data-structure.md#堆);  
用大顶堆排序得到的是升序结果(小 -> 大)  
这是因为堆排序的特点是in-place;拿到堆顶，把这个元素放在数组的空处；  
因为最大值拿出，再次堆化后最后一位就空出来了  

步骤： 
调整i(元素)使之符合堆特性(下沉)    
建堆   
堆排   
放入  
取最大元  
对节点开权O(longN)   
最大元 O(1)  

代码
```js
function shiftDown(arr, i) {
    // 来到这里都是子大于父的，只需要互换就行
    while(arr[i] < arr[2*i+1])
}

function heapSort(arr) {
    // 最后一个父节点
    let lf = (arr.lenght>>1)-1;
    for(let i = lf; i > 0; i--) {
        if (arr[i] >= arr[2*i+1] && arr[i] >= arr[2*i+2]) {

        } else {
            shiftDown(arr, i)
        }
    }
}
```
进展缓慢已经开始超出我的预期，需要做出调整了。


### 快速排序(in-place)(不稳定)  TODO  
划分算法，分治递归。  
枢纽元的概念，大概是根据枢纽元将数组分成多少部分(比如两部分)  

划分算法怎么做？（Lomuto划分算法还有Hoare划分）  

Lomuto划分：  
此方法默认将数组A最后一位作为枢纽元x，目的是将数组划分成两部分(<=x和>x的)  
借助两个下标，i和j。主要处理A[j]，即j自增，j < len-1(不包括x)  
当A[j] <= x 时，A[j]与A[i]互换，i++  
遍历到最后，将x与i位置值互换，返回i


## 时间复杂度O(N)

### 桶排序(out-place)(稳定)
桶排序是对计数排序的优化，划分成多个范围；一个范围就算一个'桶'

```js
function bucketSort(arr, bucketSize) {
    if (arr.length === 0) {
      return arr;
    }

    let i;
    let minValue = arr[0];
    let maxValue = arr[0];
    for (i = 1; i < arr.length; i++) {
      if (arr[i] < minValue) {
          minValue = arr[i];                // 输入数据的最小值
      } else if (arr[i] > maxValue) {
          maxValue = arr[i];                // 输入数据的最大值
      }
    }

    //桶的初始化
    let DEFAULT_BUCKET_SIZE = 5;            // 设置桶的默认数量为5
    bucketSize = bucketSize || DEFAULT_BUCKET_SIZE;
    let bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;  
    let buckets = new Array(bucketCount);
    for (i = 0; i < buckets.length; i++) {
        buckets[i] = [];
    }

    //利用映射函数将数据分配到各个桶中
    for (i = 0; i < arr.length; i++) {
        buckets[Math.floor((arr[i] - minValue) / bucketSize)].push(arr[i]);
    }

    arr.length = 0;
    for (i = 0; i < buckets.length; i++) {
        insertionSort(buckets[i]);                      // 对每个桶进行排序，这里使用了插入排序
        for (let j = 0; j < buckets[i].length; j++) {
            arr.push(buckets[i][j]);                      
        }
    }

    return arr;
}
```

### 计数排序(out-place)(稳定)
统计数字i出现的次数，i在带排序数组的范围内(找出最大&最小)；  
以i为key，相同数字出现的次数为value(这是大概的思路)  
i是数组下标，counter[i]存储i出现的次数；  

单纯用这个来排序的话，应该是很垃圾的吧。或许会被当成组合用法，不会是个无用的排序。

```js
function countingSort(arr, maxValue) {
    
}
```

### 基数排序(out-place)(稳定)
比较正整数,从个位数开始比较。比较的次数取决于最大数的位数  
0-9,组成基本单元。根据位数位置存储在0-9中  
后一位的排序必定是基于前一次排序结果的。  

#### 如何取某一位数
求余+整除  
例如569，取十位(6)；方式为 569%100/10>>0  
余数是要取位数的10倍(取10位数，求原数与100的余数->69)，除数与位数同位。

```js
/**
* 目前是对于正整数的排序
* arg1: 要排序的数组
* arg2: 最大数的位数
*/
function radixSort(arr, maxDigit) {
    let mod = 10; // 模
    let div = 1; // 除数
    let counter = [];
    // 每位都要从新排序，到最后一位就是最终的结果
    for(let i = 0; i < maxDigit; i++, mod *= 10, div *= 10) {
        // 存数，是一个循环
        for(let ii = 0; ii < arr.length; ii++) {
            let temp = arr[ii];
            let bit = temp%mod/div>>0;
            if (!counter[bit]) {
                counter[bit] = [];
            }
            counter[bit].push(temp);
        }

        // 取数又是一个循环，先在原数组上变化
        for(let jj = 0, j = 0; jj < counter.length; jj++) {
            let tarr = counter[jj];
            while(tarr && tarr.length) {
                arr[j++] = tarr.shift(); // shift是会修改数组的，所以counter不需要重新赋值
            }
        }
    }
    return arr;
}
```

## 相关概念
稳定与不稳定是怎么分的？


in-place是指在原数组上排序
