## 字符串匹配
匹配(或者叫搜索)是一个有与没有的问题，返回的默认是boolean值  

### 朴素(BF)算法


### RK算法


### KMP算法

#### 思路
kmp主要体现在不匹配后字符位移位数  
```

移动位数 = 已匹配的字符数 - 对应的部分匹配值

```

#### 代码

#### 部分匹配表如何产生;  
根据搜索字符串来建立部分匹配表，在当前字符截取到的子字符串；  
根据该子串分前、后缀，寻找前缀中与后缀相同的缀字符串，该缀字符串长度就是匹配值(前面被截取位置的字符)；  

例如 `bread` 的前后缀
> 前缀: [b, br, bre, brea]  
> 后缀: [read, ead, ad, d]

~~相同位置前后缀组合成原字符串~~


**使用 ABCDABD 演示部分匹配表的产生**

- A  没有前后缀，A匹配值为0
- AB  前[A],后[B]；没有相同字符串，匹配值为0
- ABC  前[A, AB],后[BC, C]；没有相同字符串，匹配值为0
- ABCD  前[A, AB, ABC],后[BCD, CD, D]; 没有相同字符串，匹配值为0
- ABCDA  前[A, AB, ABC, ABCD],后[BCDA, CDA, DA, A]; 都有A，A长度为1，匹配值为1
- ABCDAB  前[A, AB, ABC, ABCD, ABCDA],后[BCDAB, CDAB, DAB, AB, B]; 都有AB，AB长度为2，匹配值为2
- ABCDABD  前[A, AB, ABC, ABCD, ABCDA, ABCDAB],后[BCDABD, CDABD, DABD, ABD, BD, D]; 无相同字符串，匹配值为0

*会不会出现多个相同的字符串？如果有那么匹配值怎么计算*

| 搜索词 | ABCDABD |
| --- | --- |
| 部分匹配值 | 0 0 0 0 1 2 0 |

##### 部分匹配值产生方法代码
```js
function partialMatchTable(word) {

}
```


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

