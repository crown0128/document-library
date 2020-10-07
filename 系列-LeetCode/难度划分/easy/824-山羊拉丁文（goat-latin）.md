824 - 山羊拉丁文（goat-latin）
===

> Create by **jsliang** on **2020-01-08 08:43:55**  
> Recently revised in **2020-01-08 09:06:00**

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
* **题目地址**：https://leetcode-cn.com/problems/goat-latin/
* **题目内容**：

```
给定一个由空格分割单词的句子 S。
每个单词只包含大写或小写字母。

我们要将句子转换为 “Goat Latin”
（一种类似于 猪拉丁文 - Pig Latin 的虚构语言）。

山羊拉丁文的规则如下：

如果单词以元音开头（a, e, i, o, u），
在单词后添加"ma"。

例如，单词"apple"变为"applema"。

如果单词以辅音字母开头（即非元音字母），
移除第一个字符并将它放到末尾，之后再添加"ma"。
例如，单词"goat"变为"oatgma"。

根据单词在句子中的索引，
在单词最后添加与索引相同数量的字母'a'，
索引从1开始。

例如，在第一个单词后添加"a"，
在第二个单词后添加"aa"，以此类推。
返回将 S 转换为山羊拉丁文后的句子。

示例 1:

输入: "I speak Goat Latin"
输出: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
示例 2:

输入: "The quick brown fox jumped over the lazy dog"
输出: "heTmaa uickqmaaa
rownbmaaaa oxfmaaaaa umpedjmaaaaaa
overmaaaaaaa hetmaaaaaaaa
azylmaaaaaaaaa ogdmaaaaaaaaaa"

说明:

S 中仅包含大小写字母和空格。单词间有且仅有一个空格。
1 <= S.length <= 150。
```

## <a name="chapter-three" id="chapter-three"></a>三 解题及测试

> [返回目录](#chapter-one)

小伙伴可以先自己在本地尝试解题，再回来看看 **jsliang** 的解题思路。

* **LeetCode 给定函数体**：

```js
/**
 * @param {string} S
 * @return {string}
 */
var toGoatLatin = function(S) {
    
};
```

根据上面的已知函数，尝试破解本题吧~

确定了自己的答案再看下面代码哈~

> index.js

```js
/**
 * @name 山羊拉丁文
 * @param {string} S
 * @return {string}
 */
const toGoatLatin = (S) => {
  S = S.split(' ');
  for (let i = 0; i < S.length; i++) {
    switch (S[i][0]) {
      case 'a': case 'e': case 'i': case 'o': case 'u':
      case 'A': case 'E': case 'I': case 'O': case 'U':
        S[i] += 'ma' + new Array(i + 2).join('a');
        break;
      default:
        S[i] = S[i].slice(1) + S[i][0] + 'ma' + new Array(i + 2).join('a');
    }
  }
  return S.join(' ');
};

console.log(toGoatLatin('I speak Goat Latin'));
// Imaa peaksmaaa oatGmaaaa atinLmaaaaa
```

`node index.js` 返回：

```js
Imaa peaksmaaa oatGmaaaa atinLmaaaaa
```

## <a name="chapter-four" id="chapter-four"></a>四 LeetCode Submit

> [返回目录](#chapter-one)

```js
Accepted
* 99/99 cases passed (68 ms)
* Your runtime beats 61.45 % of javascript submissions
* Your memory usage beats 17.39 % of javascript submissions (35.2 MB)
```

## <a name="chapter-five" id="chapter-five"></a>五 解题思路

> [返回目录](#chapter-one)

之前说过，越长的题目，反而越发清晰怎么计算：

```js
const toGoatLatin = (S) => {
  S = S.split(' ');
  for (let i = 0; i < S.length; i++) {
    switch (S[i][0]) {
      case 'a': case 'e': case 'i': case 'o': case 'u':
      case 'A': case 'E': case 'I': case 'O': case 'U':
        S[i] += 'ma' + new Array(i + 2).join('a');
        break;
      default:
        S[i] = S[i].slice(1) + S[i][0] + 'ma' + new Array(i + 2).join('a');
    }
  }
  return S.join(' ');
};
```

在这题中，我们牢记 3 个准则：

1. 开头字母为元音字母 `a/e/i/o/u` 或者 `A/E/I/O/U` 的单词后面添加 `ma`；
2. 除元音字母外开头的单词，先将开头字母移动到后面，再添加 `ma`；
3. 从 `index = 0` 的字母添加一个 `a` 开始，往后不停增长 `a` 的长度到 `S.length`；

这样，我们就有了这个题解。

Submit 提交：

```js
Accepted
* 99/99 cases passed (68 ms)
* Your runtime beats 61.45 % of javascript submissions
* Your memory usage beats 17.39 % of javascript submissions (35.2 MB)
```

enm...这么说这样子还是挺无聊的，也没有在【题解区】和【评论区】找到比较有意思的题解~

如果你有更好的思路想法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](../../../public-repertory/img/z-index-small.png)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。