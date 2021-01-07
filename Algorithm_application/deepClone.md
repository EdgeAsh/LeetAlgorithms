## 深度拷贝
> js深度拷贝使用递归，但是会遇到问题，一个是爆栈，一个是循环引用

### 爆栈解决办法
1. 消除尾递归

2. 循环
> 换个角度，这个对象就是一颗树；使用深度优先遍历用到栈就可以处理很多数据
> 栈空了也就遍历完了
> 没有考虑function和array
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