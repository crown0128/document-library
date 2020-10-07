1010 - 总持续时间可以被60整除的歌曲（pairs-of-songs-with-total-durations-divisible-by-60）
===

> Create by **jsliang** on **2020-01-29 18:15:57**  
> Recently revised in **2020-01-29 18:58:55**

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
* **题目地址**：https://leetcode-cn.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/
* **题目内容**：

```
在歌曲列表中，
第 i 首歌曲的持续时间为 time[i] 秒。

返回其总持续时间（以秒为单位）可被 60 整除的歌曲对的数量。

形式上，我们希望索引的数字 i < j，
且有 (time[i] + time[j]) % 60 == 0。

示例 1：

输入：[30,20,150,100,40]
输出：3
解释：这三对的总持续时间可被 60 整数：
(time[0] = 30, time[2] = 150): 总持续时间 180
(time[1] = 20, time[3] = 100): 总持续时间 120
(time[1] = 20, time[4] = 40): 总持续时间 60

示例 2：

输入：[60,60,60]
输出：3
解释：所有三对的总持续时间都是 120，可以被 60 整数。

提示：

1 <= time.length <= 60000
1 <= time[i] <= 500

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/pairs-of-songs-with-total-durations-divisible-by-60
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number[]} time
 * @return {number}
 */
var numPairsDivisibleBy60 = function(time) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 总持续时间可被60整除的歌曲
 * @param {number[]} time
 * @return {number}
 */
const numPairsDivisibleBy60 = (time) => {
  let result = 0;
  for (let i = 0; i < time.length; i++) {
    for (let j = i + 1; j < time.length; j++) {
      if ((time[i] + time[j]) % 60 === 0) {
        result++;
      }
    }
  }
  return result;
};

console.log(numPairsDivisibleBy60([30, 20, 150, 100, 40])); // 3
```

`node index.js` 返回：

```js
3
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 34/34 cases passed (7168 ms)
* Your runtime beats 11.84 % of javascript submissions
* Your memory usage beats 77.62 % of javascript submissions (37.5 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

先理解题目的规则：

1. 有数组 `time = [30, 20, 150, 100, 40]`；
2. 取 `time` 中任意两个数字，有 `(time[i] + time[j]) % 60 === 0`；
3. 返回符合条件 2 的次数。

> 暴力破解

```js
const numPairsDivisibleBy60 = (time) => {
  let result = 0;
  for (let i = 0; i < time.length; i++) {
    for (let j = i + 1; j < time.length; j++) {
      if ((time[i] + time[j]) % 60 === 0) {
        result++;
      }
    }
  }
  return result;
};
```

Submit 提交：

```js
Accepted
* 34/34 cases passed (7168 ms)
* Your runtime beats 11.84 % of javascript submissions
* Your memory usage beats 77.62 % of javascript submissions (37.5 MB)
```

## <a name="chapter-six" id="chapter-six"></a>六 进一步思考

> [返回目录](#chapter-one)

思来想去找不到其他法子，看看大佬怎么操作：

> 【题解区】

```js
const numPairsDivisibleBy60 = (time) => {
  let c = new Array(60).fill(0);
  return time.reduce((prev, curr) => {
    prev += c[(60 - curr % 60) % 60];
    c[curr % 60] += 1;
    return prev;
  }, 0);
};
```

Submit 提交：

```js
Accepted
* 34/34 cases passed (72 ms)
* Your runtime beats 89.35 % of javascript submissions
* Your memory usage beats 77.62 % of javascript submissions (37.5 MB)
```

如果小伙伴们有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。