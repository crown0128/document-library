937 - 重新排列日志文件（reorder-data-in-log-files）
===

> Create by **jsliang** on **2020-01-27 11:04:09**  
> Recently revised in **2020-01-27 12:38:37**

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
* **涉及知识**：字符串
* **题目地址**：https://leetcode-cn.com/problems/reorder-data-in-log-files/
* **题目内容**：

```
你有一个日志数组 logs。
每条日志都是以空格分隔的字串。

对于每条日志，
其第一个字为字母数字标识符。

然后，要么：

标识符后面的每个字将仅由小写字母组成，或；
标识符后面的每个字将仅由数字组成。
我们将这两种日志分别称为字母日志和数字日志。
保证每个日志在其标识符后面至少有一个字。

将日志重新排序，
使得所有字母日志都排在数字日志之前。
字母日志按内容字母顺序排序，
忽略标识符；
在内容相同时，
按标识符排序。
数字日志应该按原来的顺序排列。

返回日志的最终顺序。

示例 ：

输入：
[
  "a1 9 2 3 1",
  "g1 act car",
  "zo4 4 7",
  "ab1 off key dog",
  "a8 act zoo"
]
输出：
[
  "g1 act car",
  "a8 act zoo",
  "ab1 off key dog",
  "a1 9 2 3 1",
  "zo4 4 7"
]

提示：

0 <= logs.length <= 100
3 <= logs[i].length <= 100
logs[i] 保证有一个标识符，并且标识符后面有一个字。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reorder-data-in-log-files
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string[]} logs
 * @return {string[]}
 */
var reorderLogFiles = function(logs) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 重新排列日志文件
 * @param {string[]} logs
 * @return {string[]}
 */
const reorderLogFiles = (logs) => {
  const letters = []; // 字母日志
  const nums = [];
  // 1. 先区分 字母日志 和 数字日志
  for (let i = 0; i < logs.length; i++) {
    const content = logs[i].split(' ').slice(1).join(' ');
    if (/[0-9]/.test(content)) {
      nums.push(logs[i]);
    } else {
      letters.push(logs[i]);
    }
  }
  // 2. 进一步排序 字母日志
  letters.sort((a, b) => {
    // 2.1 字符 a 的标志和内容
    const flagA = a.split(' ')[0];
    const contentA = a.split(' ').slice(1).join(' ');
    // 2.2 字符 b 的标志和内容
    const flagB = b.split(' ')[0];
    const contentB = b.split(' ').slice(1).join(' ');
    // 2.3 内容相同比较标志，否则比较内容
    if (contentA === contentB) {
      return flagA.localeCompare(flagB);
    } else {
      return contentA.localeCompare(contentB);
    }
  });
  return [...letters, ...nums];
};

console.log(reorderLogFiles([
  'a1 9 2 3 1',
  'g1 act car',
  'zo4 4 7',
  'ab1 off key dog',
  'a8 act zoo',
]));
// [
//   'g1 act car',
//   'a8 act zoo',
//   'ab1 off key dog',
//   'a1 9 2 3 1',
//   'zo4 4 7',
// ]
```

`node index.js` 返回：

```js
[
  'g1 act car',
  'a8 act zoo',
  'ab1 off key dog',
  'a1 9 2 3 1',
  'zo4 4 7',
]
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 63/63 cases passed (76 ms)
* Your runtime beats 72.22 % of javascript submissions
* Your memory usage beats 25 % of javascript submissions (38.6 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

重新定义本题内容：

1. 给定一串日志，例如：`['a1 9 2 3 1', 'g1 act car']`；
2. 【定义】`a1 9 2 3 1` 这类，除了开头标志 `a1` 外，仅由数字组成的，叫 **数字日志**；
3. 【定义】`a1 act car` 这类，除了开头标志 `al` 外，仅由小写字母组成的，叫 **字母日志**；
4. 【排序规则】将日志重新排序，使得所有 **字母日志** 都排在 **数字日志** 之前；
5. 【排序规则】**字母日志** 在内容不同时，忽略标识符后，按内容字母顺序排序；在内容相同时，按标识符排序；
6. 【排序规则】**数字日志** 按原来的顺序排列；

解读完毕，开始解题：

> 暴力破解 - 获取数字日志

```js
const reorderLogFiles = (logs) => {
  const nums = [];
  for (let i = 0; i < logs.length; i++) {
    const content = logs[i].split(' ').slice(1).join(' ');
    if (/[0-9]/.test(content)) {
      nums.push(logs[i]);
    }
  }
  return nums;
};
```

以上为获取数字日志的方式~

接下来进一步完善获取 字母日志：

> 暴力破解

```js
const reorderLogFiles = (logs) => {
  const letters = []; // 字母日志
  const nums = [];
  // 1. 先区分 字母日志 和 数字日志
  for (let i = 0; i < logs.length; i++) {
    const content = logs[i].split(' ').slice(1).join(' ');
    if (/[0-9]/.test(content)) {
      nums.push(logs[i]);
    } else {
      letters.push(logs[i]);
    }
  }
  // 2. 进一步排序 字母日志
  letters.sort((a, b) => {
    // 2.1 字符 a 的标志和内容
    const flagA = a.split(' ')[0];
    const contentA = a.split(' ').slice(1).join(' ');
    // 2.2 字符 b 的标志和内容
    const flagB = b.split(' ')[0];
    const contentB = b.split(' ').slice(1).join(' ');
    // 2.3 内容相同比较标志，否则比较内容
    if (contentA === contentB) {
      return flagA.localeCompare(flagB);
    } else {
      return contentA.localeCompare(contentB);
    }
  });
  return [...letters, ...nums];
};
```

Submit 提交如下：

```js
Accepted
* 63/63 cases passed (76 ms)
* Your runtime beats 72.22 % of javascript submissions
* Your memory usage beats 25 % of javascript submissions (38.6 MB)
```

> 写代码的时候，像足了小时候不会写作业，想抄答案又不敢抄的样子。

经过近一个多小时的编写，终于搞定了这道【简单题】，咬牙切齿（中间跑去吃午饭了）。

如果小伙伴有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。