496 - 下一个更大元素I（next-greater-element-i）
===

> Create by **jsliang** on **2019-10-29 10:40:59**  
> Recently revised in **2019-10-29 20:13:05**

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
* **涉及知识**：栈
* **题目地址**：https://leetcode-cn.com/problems/next-greater-element-i/
* **题目内容**：

```
给定两个没有重复元素的数组 nums1 和 nums2，其中nums1 是 nums2 的子集。

找到 nums1 中每个元素在 nums2 中的下一个比其大的值。

nums1 中数字 x 的下一个更大元素是指：

x 在 nums2 中对应位置的右边的第一个比 x 大的元素。

如果不存在，对应位置输出-1。

示例 1:
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
  对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
  对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
  对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。

示例 2:
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于num1中的数字2，第二个数组中的下一个较大数字是3。
    对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
注意:

nums1和nums2中所有元素是唯一的。
nums1和nums2 的数组大小都不超过1000。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var nextGreaterElement = function(nums1, nums2) {
  
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
const nextGreaterElement = (nums1, nums2) => {
  const result = [];
  for (let i = 0; i < nums1.length; i++) {
    const index = nums2.findIndex(item2 => item2 === nums1[i]);
    const afterList = nums2.slice(index);
    const afterListIndex = afterList.findIndex(item3 => item3 > nums1[i]);
    if (afterListIndex > -1) {
      result.push(afterList[afterListIndex]);
    } else {
      result.push(afterListIndex);
    }
  }
  return result;
};

// const nums1 = [4, 1, 2];
// const nums2 = [1, 3, 4, 2];
const nums1 = [2, 4];
const nums2 = [1, 2, 3, 4];
console.log(nextGreaterElement(nums1, nums2));
```

`node index.js` 返回：

```js
[3, -1]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 17/17 cases passed (100 ms)
* Your runtime beats 23.6 % of javascript submissions
* Your memory usage beats 5.97 % of javascript submissions (41.2 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

暴力有时候可以快速解决问题，但是肯定不是最优的解决方式。

**首先**，在这题的破解中，我们遍历 `nums1`，因为 `nums1` 是 `nums2` 的子集，所以在 `nums2` 中 `findIndex` 查找 `nums1` 的元素必定是有的，我们通过 `index` 来记录对应的位置。

**然后**，我们裁剪该 `index` 后 `nums2` 的数组，并在当中查找是否有元素比 `nums1[i]` （当前元素）更大。

**最后**，我们判断是否存在，如果存在则存入该位置对应的值；如果不存在则返回 `-1`（`findIndex` 不存在的时候返回的值）。

这样，我们就完成这个题目啦！（最暴力的方式，排名垫底）

## <a name="chapter-six" id="chapter-six"></a>六 进一步思考

> [返回目录](#chapter-one)

由于现在 2019-10-29 20:12:13 **jsliang** 还在加班，所以乘测试还在走业务流程，顺带写了这道题，如果小伙伴们有更好的题解或者思路，欢迎留言评论私聊~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。