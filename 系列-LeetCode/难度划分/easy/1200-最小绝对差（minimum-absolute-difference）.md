1200 - 最小绝对差（minimum-absolute-difference）
===

> Create by **jsliang** on **2020-01-31 21:27:03**  
> Recently revised in **2020-01-31 21:39:36**

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
* **涉及知识**：数组
* **题目地址**：https://leetcode-cn.com/problems/minimum-absolute-difference/
* **题目内容**：

```
给你个整数数组 arr，其中每个元素都 不相同。

请你找到所有具有最小绝对差的元素对，并且按升序的顺序返回。

示例 1：

输入：arr = [4,2,1,3]
输出：[[1,2],[2,3],[3,4]]

示例 2：

输入：arr = [1,3,6,10,15]
输出：[[1,3]]

示例 3：

输入：arr = [3,8,-10,23,19,-4,-14,27]
输出：[[-14,-10],[19,23],[23,27]]

提示：

2 <= arr.length <= 10^5
-10^6 <= arr[i] <= 10^6

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-absolute-difference
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} arr
 * @return {number[][]}
 */
var minimumAbsDifference = function(arr) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 最小绝对差
 * @param {number[]} arr
 * @return {number[][]}
 */
const minimumAbsDifference = (arr) => {
  arr.sort((a, b) => a - b);
  let result = [];
  let min = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < arr.length - 1; i++) {
    const dValue = arr[i + 1] - arr[i];
    if (dValue < min) {
      result = [[arr[i], arr[i + 1]]];
      min = dValue;
    } else if (dValue === min) {
      result.push([arr[i], arr[i + 1]]);
    }
  }
  return result;
};

console.log(minimumAbsDifference([4, 2, 1, 3])); // [ [ 1, 2 ], [ 2, 3 ], [ 3, 4 ] ]
```

`node index.js` 返回：

```js
[ [ 1, 2 ], [ 2, 3 ], [ 3, 4 ] ]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 36/36 cases passed (204 ms)
* Your runtime beats 76.19 % of javascript submissions
* Your memory usage beats 74.03 % of javascript submissions (43.8 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

**首先**，我们需要思考一个问题：

* 怎样的数字会产生最小绝对差

OK，相信你也想到了：

* 顺序（逆序）排序数组下相邻的两个数字可能产生最小绝对差

那么，我们顺势就知道了大半部分答案：

> 暴力破解

```js
const minimumAbsDifference = (arr) => {
  arr.sort((a, b) => a - b);
  let result = [];
  let min = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < arr.length - 1; i++) {
    const dValue = arr[i + 1] - arr[i];
    if (dValue < min) {
      result = [[arr[i], arr[i + 1]]];
      min = dValue;
    } else if (dValue === min) {
      result.push([arr[i], arr[i + 1]]);
    }
  }
  return result;
};
```

步骤如下：

1. 将数组 `arr` 进行从小到大排序。
2. 判断目前的 `arr[i + 1] - arr[i]` 的值是多少。如果它比最小值还小，那么 `result` 和 `min` 都需要重置；如果它等于最小值，那么最小值数组添加一个二维数组；如果它大于最小值，不用理会。
3. 最后返回 `result` 即可。

Submit 提交：

```js
Accepted
* 36/36 cases passed (204 ms)
* Your runtime beats 76.19 % of javascript submissions
* Your memory usage beats 74.03 % of javascript submissions (43.8 MB)
```

> 似乎这才是【简单】难度该有的节奏~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。