832 - 翻转图像（flipping-an-image）
===

> Create by **jsliang** on **2020-01-08 18:38:10**  
> Recently revised in **2020-01-08 19:18:14**

## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 前言](#chapter-two) |
| <a name="catalog-chapter-three" id="catalog-chapter-three"></a>[三 解题及测试](#chapter-three) |
| <a name="catalog-chapter-four" id="catalog-chapter-four"></a>[四 LeetCode Submit](#chapter-four) |
| <a name="catalog-chapter-five" id="catalog-chapter-five"></a>[五 解题思路](#chapter-five) |
| <a name="catalog-chapter-six" id="catalog-chapter-six"></a>[六 进一步思考](#chapter-six) |

## <a name="chapter-two" id="chapter-two"></a>二 前言

> [返回目录](#chapter-one)

* **难度**：简单
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/flipping-an-image/
* **题目内容**：

```
给定一个二进制矩阵 A，
我们想先水平翻转图像，
然后反转图像并返回结果。

水平翻转图片就是将图片的每一行都进行翻转，即逆序。
例如，水平翻转 [1, 1, 0] 的结果是 [0, 1, 1]。

反转图片的意思是图片中的 0 全部被 1 替换， 
1 全部被 0 替换。
例如，反转 [0, 1, 1] 的结果是 [1, 0, 0]。

示例 1:

输入: [[1,1,0],[1,0,1],[0,0,0]]
输出: [[1,0,0],[0,1,0],[1,1,1]]
解释: 首先翻转每一行: [[0,1,1],[1,0,1],[0,0,0]]；
     然后反转图片: [[1,0,0],[0,1,0],[1,1,1]]

示例 2:

输入: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
输出: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
解释: 
首先翻转每一行: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]；
然后反转图片: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]

说明:

1 <= A.length = A[0].length <= 20
0 <= A[i][j] <= 1
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} A
 * @return {number[][]}
 */
var flipAndInvertImage = function(A) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 翻转图像
 * @param {number[][]} A
 * @return {number[][]}
 */
const flipAndInvertImage = (A) => {
  for (let i = 0; i < A.length; i++) {
    A[i] = A[i].reverse().map(item => item === 1 ? 0 : 1);
  }
  return A;
};

console.log(flipAndInvertImage(
  [ [1, 1, 0], [1, 0, 1], [0, 0, 0] ]
));
// [ [ 1, 0, 0 ], [ 0, 1, 0 ], [ 1, 1, 1 ] ]
```

`node index.js` 返回：

```js
[ [ 1, 0, 0 ], [ 0, 1, 0 ], [ 1, 1, 1 ] ]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 82/82 cases passed (76 ms)
* Your runtime beats 75.42 % of javascript submissions
* Your memory usage beats 42.51 % of javascript submissions (35.1 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

放开心态，将这道题当成小白题：

* 翻转图片步骤：将 `A` 中每一项数组进行数组反转，然后将每一项进行替换（1 => 0; 0 => 1）。

咦，突然好像无话可说了：

> 超暴力破解

```js
const flipAndInvertImage = (A) => {
  for (let i = 0; i < A.length; i++) {
    A[i] = A[i].reverse().map(item => item === 1 ? 0 : 1);
  }
  return A;
};
```

怎样，是不是很简单，我们通过 `reverse()` 将数组反转了，然后我们通过 `map` 遍历其中每一项，将 1 转换成 0，将 0 转换成 1，就完成了最终翻转！

Submit 提交：

```js
Accepted
* 82/82 cases passed (76 ms)
* Your runtime beats 75.42 % of javascript submissions
* Your memory usage beats 42.51 % of javascript submissions (35.1 MB)
```

## <a name="chapter-six" id="chapter-six"></a>六 进一步思考

> [返回目录](#chapter-one)

仔细想了想，用自己方式遍历会不会好点：

> 暴力破解

```js
const flipAndInvertImage = (A) => {
  for (let i = 0; i < A.length; i++) {
    const tempArr = [];
    for (let j = A[i].length - 1; j >= 0; j--) {
      if (A[i][j] === 0) {
        tempArr.push(1);
      } else {
        tempArr.push(0);
      }
    }
    A[i] = tempArr;
  }
  return A;
};
```

Submit 提交：

```js
Accepted
* 82/82 cases passed (76 ms)
* Your runtime beats 75.42 % of javascript submissions
* Your memory usage beats 5.26 % of javascript submissions (36.1 MB)
```

好吧，运行效率一样，空间用得更多了~

然后瞅了下【题解区】和【评论区】，看到一个有意思的破解：

> 一行求解

```js
const flipAndInvertImage = (A) => {
  return A.map(a => a.map(i => i ^ 1).reverse());
};
```

Submit 提交：

```js
Accepted
* 82/82 cases passed (72 ms)
* Your runtime beats 88.27 % of javascript submissions
* Your memory usage beats 19.03 % of javascript submissions (35.5 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。