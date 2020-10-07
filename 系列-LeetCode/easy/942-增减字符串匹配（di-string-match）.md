942 - 增减字符串匹配（di-string-match）
===

> Create by **jsliang** on **2020-01-27 17:34:12**  
> Recently revised in **2020-01-27 18:13:43**

## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 前言](#chapter-two) |
| <a name="catalog-chapter-three" id="catalog-chapter-three"></a>[三 解题及测试](#chapter-three) |
| <a name="catalog-chapter-four" id="catalog-chapter-four"></a>[四 LeetCode Submit](#chapter-four) |
| <a name="catalog-chapter-five" id="catalog-chapter-five"></a>[五 解题思路](#chapter-five) |

## <a name="chapter-two" id="chapter-two"></a>二 前言

> [返回目录](#chapter-one)

* **难度**：简单
* **涉及知识**：数学
* **题目地址**：https://leetcode-cn.com/problems/di-string-match/
* **题目内容**：

```
给定只含 "I"（增大）或 "D"（减小）的字符串 S ，
令 N = S.length。

返回 [0, 1, ..., N] 的任意排列 A，
使得对于所有 i = 0, ..., N-1，都有：

如果 S[i] == "I"，那么 A[i] < A[i+1]
如果 S[i] == "D"，那么 A[i] > A[i+1]

示例 1：

输出："IDID"
输出：[0,4,1,3,2]

示例 2：

输出："III"
输出：[0,1,2,3]

示例 3：

输出："DDI"
输出：[3,2,0,1]

提示：

1 <= S.length <= 1000
S 只包含字符 "I" 或 "D"。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/di-string-match
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} S
 * @return {number[]}
 */
var diStringMatch = function(S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 增减字符串匹配
 * @param {string} S
 * @return {number[]}
 */
const diStringMatch = (S) => {
  const nums = Array.from(Array(S.length + 1), (value, index) => index);
  const result = [];
  for (let i = 0; i < S.length; i++) {
    if (S[i] === 'I') {
      result.push(nums.shift());
    } else {
      result.push(nums.pop());
    }
  }
  return [...result, ...nums];
};

console.log(diStringMatch('IDID')); // [ 0, 4, 1, 3, 2 ]
console.log(diStringMatch('III')); // [ 0, 1, 2, 3 ]
console.log(diStringMatch('DDI')); // [ 3, 2, 0, 1 ]
```

`node index.js` 返回：

```js
[ 0, 4, 1, 3, 2 ]
[ 0, 1, 2, 3 ]
[ 3, 2, 0, 1 ]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 95/95 cases passed (112 ms)
* Your runtime beats 17.39 % of javascript submissions
* Your memory usage beats 11.02 % of javascript submissions (39.8 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

……这道题，有点意思：

> 暴力破解

```js
const diStringMatch = (S) => {
  const nums = Array.from(Array(S.length + 1), (value, index) => index);
  const result = [];
  for (let i = 0; i < S.length; i++) {
    if (S[i] === 'I') {
      result.push(nums.shift());
    } else {
      result.push(nums.pop());
    }
  }
  return [...result, ...nums];
};
```

方法很简单：

1. 生成一个数组 `nums`，里面是从 `[0, S.length + 1]` 范围的数字。
2. 设置 `result` 获取最终值。
3. 通过 `for` 遍历数组。如果当前数组元素是 `I`，那么就将 `nums` 的队列头通过 `shift` 操作推出来；如果当前元素不是 `I`，即 `D`（题目只包含 `I` 和 `D` 两种操作），那么将其 `pop` 出来给 `result`。

依次，最终返回 `[...result, ...nums]` 即可，因为不管如何，`nums` 还会剩余 1 个长度。

Submit 提交：

```js
Accepted
* 95/95 cases passed (112 ms)
* Your runtime beats 17.39 % of javascript submissions
* Your memory usage beats 11.02 % of javascript submissions (39.8 MB)
```

仔细想想小脑袋瓜就这种解法了，但是最后还是想讲讲生成 0 到 n 数字组成的数组的三种方式：

> ... 扩展

```js
const arr1 = [...Array(3)].map((value, index) => index);
console.log(arr1);
// [0, 1, 2]
```

> Array.from

```js
const arr2 = Array.from(Array(3), (value, index) => index);
console.log(arr2);
// [0, 1, 2]
```

> 愚蠢法子

```js
const arr3 = [];
for (let i = 0; i < 3; i++) {
  arr3.push(i);
}
console.log(arr3);
// [0, 1, 2]
```

以后小伙伴可以多尝试各种技巧~

如果小伙伴对于这道题有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。