746 - 使用最小花费爬楼梯（min-cost-climbing-stairs）
===

> Create by **jsliang** on **2019-12-30 08:37:35**  
> Recently revised in **2019-12-30 09:50:28**

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
* **涉及知识**：数组、动态规划
* **题目地址**：https://leetcode-cn.com/problems/min-cost-climbing-stairs/
* **题目内容**：

```
数组的每个索引做为一个阶梯，
第 i 个阶梯对应着一个非负数的体力花费值 cost[i](索引从 0 开始)。

每当你爬上一个阶梯你都要花费对应的体力花费值，
然后你可以选择继续爬一个阶梯或者爬两个阶梯。

您需要找到达到楼层顶部的最低花费。

在开始时，
你可以选择从索引为 0 或 1 的元素作为初始阶梯。

示例 1:

输入: cost = [10, 15, 20]
输出: 15
解释: 最低花费是从 cost[1] 开始，
然后走两步即可到阶梯顶，一共花费 15。

示例 2:

输入: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
输出: 6
解释: 最低花费方式是从 cost[0] 开始，
逐个经过那些 1，跳过 cost[3]，一共花费 6。

注意：

cost 的长度将会在 [2, 1000]。
每一个 cost[i] 将会是一个 Integer 类型，范围为 [0, 999]。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 使用最小花费爬楼梯
 * @param {number[]} cost
 * @return {number}
 */
const minCostClimbingStairs = (cost) => {
  let result1 = 0,
      result2 = 0;
  for (let i = cost.length - 1; i >= 0; i--) {
    const temp = cost[i] + Math.min(result1, result2);
    result2 = result1;
    result1 = temp;
  }
  return Math.min(result1, result2);
};

console.log(minCostClimbingStairs([10, 15, 20])); // 15
console.log(minCostClimbingStairs([1, 100, 1, 1, 1, 100, 1, 1, 100, 1])); // 6
```

`node index.js` 返回：

```js
15
6
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 276/276 cases passed (72 ms)
* Your runtime beats 66.09 % of javascript submissions
* Your memory usage beats 47.83 % of javascript submissions (35.4 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

因为这道题标明是动态规划，又因为我这方面知识欠缺，所以就去搜索了下动态规划的玩法。

然后呢，值得注意的是，如果你网上翻到的文章，只讲下面这几块内容，就不用往下翻了，浪费时间：

1. 斐波那契数列
2. 最长公共子序列

在这里推荐几篇文章：

1. [动态规划难？读完这篇还不理解那就不要请我吃鸡了 -  zy445566](https://cnodejs.org/topic/5c1b091176c4964062a1ba44)
2. [JavaScript 版动态规划算法题：打家劫舍 - 刘一奇](https://www.liuyiqi.cn/2017/03/10/house-robber/)

当然，看完我还是不懂我这道题怎么解，先暴力试试：

> 暴力破解

```js
// 愣是没想出来
```

一想到还有动态规划这么巧妙的方法，就忍不住去想怎么解。

一开始的思路是顺序遍历，取前三者中最小一个 `i + 1` 或者最小两个 `i + (i + 2)`，但是想想我还要定位每次加到哪了，就嫌麻烦。

看了下官方题解，豁然开朗：

```js
const minCostClimbingStairs = (cost) => {
  let result1 = 0,
      result2 = 0;
  for (let i = cost.length - 1; i >= 0; i--) {
    const temp = cost[i] + Math.min(result1, result2);
    result2 = result1;
    result1 = temp;
  }
  return Math.min(result1, result2);
};
```

看代码，其实想法很简单，就是想不出来：

1. 最少的应该是 `cost[i] + min(f[f + 1], f[f + 2])`。即当前项和前两项中最小的相加。
2. 因为顺序遍历来说不方便，所以需要倒序遍历。
3. 通过 `result1 = f[f + 1]`，`result2 = f[f + 2]`，我们倒序相加。

最终输出结果：

```js
Accepted
* 276/276 cases passed (72 ms)
* Your runtime beats 66.09 % of javascript submissions
* Your memory usage beats 47.83 % of javascript submissions (35.4 MB)
```

真真想不到系列，看来【动态规划】还需要多练习一下，了解了解玄学~

如果小伙伴有更好的想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。