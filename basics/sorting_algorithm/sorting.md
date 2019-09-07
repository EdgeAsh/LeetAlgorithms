## 时间复杂度O(N^2)

### 插入排序
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

## 时间复杂度O(NlogN)


## 时间复杂度O(N)
