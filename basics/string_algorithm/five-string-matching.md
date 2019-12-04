## 字符串匹配
匹配(或者叫搜索)是一个有与没有的问题，返回的默认是boolean值  

### 朴素算法


### KMP算法
部分匹配表如何产生

### RK算法


### BM算法
头部对齐，从尾部开始匹配；


### Trie树(前缀/字典树)
用空间换时间，树的结构是怎么样的？目的是快速搜索，什么样的树结构才能快   
用我自己的话说就是将共同的字母拿出来，接着下一个，不行就散开直到最后在树上表示了所有的内容  
文字可以这么表示，图片表示就更简单。但是体现在代码上就是要绕-绕-绕了吧  

#### 思路
多叉树嘛，就是层级关系。子父节点，将源存起来，单个字符集；搜索的时候从头匹配，  

#### 代码
```js
class TreeNode {
  constractor(data) {
    this.data = data;
    this.isEnding = false;
    this.children = {};
  }
}

class TrieTree{
  constructor() {
    // 创建根节点
    this.root = new TreeNode('/');
  }

  // 存入
  insert(text) {
    for(let chart of text) {

    }
  }

  // 查找
  find(word) {
    for(let chart of word) {
      
    }
  }
}
```