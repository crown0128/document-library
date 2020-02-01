1304 - 和为零的唯一整数（find-n-unique-integers-sum-up-to-zero）
===

> Create by **jsliang** on **2020-02-01 19:45:26**  
> Recently revised in **2020-02-01 19:56:53**

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
* **题目地址**：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero/
* **题目内容**：

```
给你一个整数 n，
请你返回 任意 一个由 n 个 各不相同 的整数组成的数组，
并且这 n 个数相加和为 0 。

示例 1：

输入：n = 5
输出：[-7,-1,1,3,4]
解释：这些数组也是正确的 [-5,-1,1,2,3]，[-3,-1,2,-2,4]。

示例 2：

输入：n = 3
输出：[-1,0,1]

示例 3：

输入：n = 1
输出：[0]

提示：

1 <= n <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var sumZero = function(n) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 和为零的n个唯一整数
 * @param {number} n
 * @return {number[]}
 */
const sumZero = (n) => {
  let number = n,
      flag = false;
  const result = [];
  for (let i = 0; i < n; i++) {
    if (flag) {
      result.push(-number);
      number--;
      flag = false;
    } else {
      result.push(number);
      flag = true;
    }
  }
  if (result.length % 2 === 1) {
    result[result.length - 1] = 0;
  }
  return result;
};

console.log(sumZero(5)); // [ 5, -5, 4, -4, 0 ]
```

`node index.js` 返回：

```js
[ 5, -5, 4, -4, 0 ]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 42/42 cases passed (64 ms)
* Your runtime beats 87.12 % of javascript submissions
* Your memory usage beats 83.1 % of javascript submissions (34.9 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

这道题给了 **jsliang** 最大程度的自由，所以可以随心所欲，任性发挥：

> 暴力破解

```js
const sumZero = (n) => {
  // 1. 定义变量
  let number = n,
      flag = false;
  
  // 2. 定义结果值
  const result = [];
  for (let i = 0; i < n; i++) {
    // 2.1 判断是输入正数还是负数
    if (flag) {
      result.push(-number);
      number--;
      flag = false;
    } else {
      result.push(number);
      flag = true;
    }
  }

  // 3. 判断是否为奇数长度位
  if (result.length % 2 === 1) {
    result[result.length - 1] = 0;
  }

  // 4. 输出结果
  return result;
};
```

是的，正如上面所写，如果 `n` 为 5，那么输出：

* [5, -5, 4, -4, 0]

如果 `n` 为 4，那么输出：

* [4, -4, 3, -3]

Submit 提交：

```js
Accepted
* 42/42 cases passed (64 ms)
* Your runtime beats 87.12 % of javascript submissions
* Your memory usage beats 83.1 % of javascript submissions (34.9 MB)
```

那么本题题解就到这里。

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。