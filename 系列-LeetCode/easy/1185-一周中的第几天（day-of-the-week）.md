1185 - 一周中的第几天（day-of-the-week）
===

> Create by **jsliang** on **2020-01-31 19:38:14**  
> Recently revised in **2020-01-31 20:32:54**

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
* **题目地址**：https://leetcode-cn.com/problems/day-of-the-week/
* **题目内容**：

```
给你一个日期，请你设计一个算法来判断它是对应一周中的哪一天。

输入为三个整数：day、month 和 year，分别表示日、月、年。

您返回的结果必须是这几个值中的一个
{
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday"
}。

示例 1：

输入：day = 31, month = 8, year = 2019
输出："Saturday"

示例 2：

输入：day = 18, month = 7, year = 1999
输出："Sunday"

示例 3：

输入：day = 15, month = 8, year = 1993
输出："Sunday"

提示：

给出的日期一定是在 1971 到 2100 年之间的有效日期。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/day-of-the-week
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {number} day
 * @param {number} month
 * @param {number} year
 * @return {string}
 */
var dayOfTheWeek = function(day, month, year) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 一周中的第几天
 * @param {number} day
 * @param {number} month
 * @param {number} year
 * @return {string}
 */
const dayOfTheWeek = (day, month, year) => {
  if (month === 1 || month === 2) {
    month += 12;
    year -= 1;
  }
  const result = (day + 1 + 2 * month + Math.floor(3 * (month + 1) / 5) + year + Math.floor(year / 4) - Math.floor(year / 100) + Math.floor(year / 400)) % 7;
  return ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][result];
};

console.log(dayOfTheWeek(31, 1, 2020)); // 'Firday'
console.log(dayOfTheWeek(18, 7, 1999)); // 'Sunday'
```

`node index.js` 返回：

```js
'Firday'
'Sunday'
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 39/39 cases passed (64 ms)
* Your runtime beats 59.11 % of javascript submissions
* Your memory usage beats 76.88 % of javascript submissions (33.8 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

众所周知，**jsliang** 在题目《1154-一年中的第几天》放了水，直接讲解了别人的答案。

没想到天道有轮回，一下子又要求《一周中的第几天》了，咱们试试吧：

> 暴力破解

```js
const dayOfTheWeek = (day, month, year) => {
  if (month === 1 || month === 2) {
    month += 12;
    year -= 1;
  }
  const result = (day + 1 + 2 * month + Math.floor(3 * (month + 1) / 5) + year + Math.floor(year / 4) - Math.floor(year / 100) + Math.floor(year / 400)) % 7;
  return ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][result];
};
```

罪过罪过，网上找到公式直接套用~

Submit 提交：

```js
Accepted
* 39/39 cases passed (64 ms)
* Your runtime beats 59.11 % of javascript submissions
* Your memory usage beats 76.88 % of javascript submissions (33.8 MB)
```

## <a name="chapter-six" id="chapter-six"></a>六 进一步思考

> [返回目录](#chapter-one)

在【题解区】和【评论区】，除了套公式的，还有套 JavaScript 原生 API 的：

> 使用 API

```js
const dayOfTheWeek = (day, month, year) => {
  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  let x = `${year}/${month}/${day}`;
  let date = new Date(Date.parse(x));
  return days[date.getDay()];
};
```

Submit 提交：

```js
Accepted
* 39/39 cases passed (52 ms)
* Your runtime beats 95.57 % of javascript submissions
* Your memory usage beats 35.63 % of javascript submissions (34.1 MB)
```

搞定，收工。

那么这道题就写到这里啦~

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。