## 深度拷贝
> js深度拷贝使用递归，但是会遇到问题，一个是爆栈，一个是循环引用

### 爆栈解决办法
1. 使用尾递归
> 纯粹的函数式编程语言没有循环的命令，都通过递归实现；尾递归与柯里化

2. 循环
> 换个角度，这个对象就是一颗树；使用深度优先遍历用到栈就可以处理很多数据；但没法解决循环引用
> 栈空了也就遍历完了
> 没有考虑function和array
这个挺难理解的，要试着手写几遍，不行就抄着理解。看是看不懂的
以[深拷贝的终极探索（99%的人都不知道）](https://segmentfault.com/a/1190000016672263)为学习参考
```js
function cloneLoop(x) {
    const root = {}
    const stack = [
        // 关系需要描述成这样，节点的不同属性
        {
            parent: root,
            key: undefined,
            data: x,
        }
    ]

    while(stack.length) { // 栈空了说明遍历完成
        const node = stack.pop()
        const parent = node.parent
        const key = node.key
        const data = node.data

        let res = parent
        if (typeof key !== 'undefined') {
            res = parent[key] = {} // res变为parent的子，空对象
        }
        for (let k in data) {
            if (data.hasOwnProperty(k)) {
                if (typeof data[k] === 'object') { // 是对象需要复制里面的内容
                    stack.push({
                        parent: res,
                        key: k,
                        data: data[k]
                    })
                } else {
                    res[k] = data[k] // 非引用类型直接复制
                }
            }
        }
    }
    return root
}

// 判断是否为对象
function isObject(x) { // 使用toString方法
    // 函数 "[object Function]"，数组 "[object Array]"，对象 '[object Object]'
    return Object.prototype.toString.call(x) === '[object Object]'
}
```

### 解决循环引用
用数组`uniqueList`保存已经被复制了的对象，当下一轮复制遇到对象时，先去检查一遍是否已经存在

新增部分的代码不多
```js
function cloneForce(x) {
    const root = {}
    // ------ 新增的部分 --------
    const uniqueList = []
    // ------ 新增的部分 --------
    const stack = [
        // 关系需要描述成这样，节点的不同属性
        {
            parent: root,
            key: undefined,
            data: x,
        }
    ]

    while(stack.length) { // 栈空了说明遍历完成
        const node = stack.pop()
        const parent = node.parent
        const key = node.key
        const data = node.data

        let res = parent
        if (typeof key !== 'undefined') {
            res = parent[key] = {} // res变为parent的子，空对象
        }
        // ------ 新增的部分 -------- 需要好好理解source和target的作用，target存的是被复制对象的子项，source存的是被复制对象的值(经过处理后，值存在于data中，见stack初始赋值)
        let uniqueData = findU(uniqueList, data)
        if (uniqueData) { // 发现重复的
            parent[key] = uniqueData.target
            break
        }
        uniqueList.push({
            source: data,
            target: res,
        })
        // ------ 新增的部分 --------


        for (let k in data) {
            if (data.hasOwnProperty(k)) {
                if (typeof data[k] === 'object') { // 是对象需要复制里面的内容
                    stack.push({
                        parent: res,
                        key: k,
                        data: data[k]
                    })
                } else {
                    res[k] = data[k] // 非引用类型直接复制
                }
            }
        }
    }
    return root
}

// 寻找独特的对象
function findU(arr, item) {
    for(let i = 0; i < arr.length; i++) {
        if (arr[i].source === item) {
            return arr[i]
        }
    }
    return null
}

// 判断是否为对象
function isObject(x) { // 使用toString方法
    // 函数 "[object Function]"，数组 "[object Array]"，对象 '[object Object]'
    return Object.prototype.toString.call(x) === '[object Object]'
}
```
