Array - 多维数组转一维数组
===

> Create by **jsliang** on **2019-11-20 16:07:46**  
> Recently revised in **2019-11-20 17:21:20**

## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- | 
| [一 目录](#chapter-one) | 
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 前言](#chapter-two) |
| <a name="catalog-chapter-three" id="catalog-chapter-three"></a>[三 二维降一维](#chapter-three) |
| <a name="catalog-chapter-four" id="catalog-chapter-four"></a>[四 递归降维](#chapter-four) |
| <a name="catalog-chapter-five" id="catalog-chapter-five"></a>[五 flat() 降维](#chapter-five) |
| <a name="catalog-chapter-six" id="catalog-chapter-six"></a>[六 参考文献](#chapter-six) |

## <a name="chapter-two" id="chapter-two"></a>二 前言

> [返回目录](#chapter-one)

在业务场景或者刷 LeetCode 的时候，曾经碰到多次碰到一个问题：

* 如何将二维甚至多维的数组转换成一维数组？

> 讲起将多维转成一维，突然想起一个词叫做【降维打击】，下面将这种二维甚至多维的打成一维数组的方法，叫做【降维】

这篇文章和你一起探讨下转换的方法~

## <a name="chapter-three" id="chapter-three"></a>三 二维降一维

> [返回目录](#chapter-one)

我们先来个简单的：

* 二维数组如何降级成一维数组？

很多时候，我们的数组层次并没有那么深，只有个二维数组，所以我们可以了解下一些快捷的使用方法。

> `reduce()` 二维降一维

```js
const oldArr = [1, 2, [3, 4]];

const newArr = oldArr.reduce((prev, curr) => (prev.concat(curr)), []);

console.log(newArr);
// [1, 2, 3, 4]
```

> `concat()` 二维将一维

```js
const oldArr = [1, 2, [3, 4]];

const newArr = [].concat(...oldArr);
const newnewArr = Array.prototype.concat.apply([], oldArr);

console.log(newArr);
// [1, 2, 3, 4]
console.log(newnewArr);
// [1, 2, 3, 4]
```

> `flat()` 二维降一维

```js
const oldArr = [1, 2, [3, 4]];

const newArr = oldArr.flat();

console.log(newArr);
// [1, 2, 3, 4]
```

## <a name="chapter-four" id="chapter-four"></a>四 递归降维

> [返回目录](#chapter-one)

既然二维降一维的小伙伴们看过之后，我们就可以进一步了解多维降一维数组了。

我们先了解下通过递归降维。

关于递归降维，这里有两个方法：

* `forEach` 递归
* `reduce` 递归

下面一一分析：

> forEach 递归降维

```js
const oldArr = [
  1,
  [
    2, [3],
    [4, 5, 6],
    [7, 8, 9],
    10,
    11,
  ],
  12,
  13,
  14,
  [15, 16, 17],
];

const newArr = [];

const ergodic = (arr) => {
  arr.forEach((item) => {
    if (Array.isArray(item)) {
      ergodic(item);
    } else {
      newArr.push(item);
    }
  })
}

ergodic(oldArr, newArr);

console.log(newArr);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 ]
```

> `Array.isArray()` 用于确定传递的值是否是一个 `Array`，返回 `true` 或者 `false`。

在这个递归方法中，我们判断每一项是不是数组。

如果是，则进一步递归，直到其不是为止。

如果不是，则用新数组接收它。

> reduce 递归降维

```js
const oldArr = [
  1,
  [
    2, [3],
    [4, 5, 6],
    [7, 8, 9],
    10,
    11
  ],
  12,
  13,
  14,
  [15, 16, 17],
];

const ergodic = (arr) => arr.reduce((prev, curr, index, list) => {
  if (Array.isArray(curr)) {
    return prev.concat(...ergodic(curr));
  }
  return prev.concat(curr);
}, []);

const newArr = ergodic(oldArr);

console.log(newArr);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 ]
```

* 提问：请说出 `reduce` 对应的 4 个参数代表什么？

## <a name="chapter-five" id="chapter-five"></a>五 flat() 降维

> [返回目录](#chapter-one)

`flat()` 是 ES6 提供的一个将嵌套的数组 “拉平” 的方法。

> flat 降维

```js
const oldArr = [
  1,
  [
    2, [3],
    [4, 5, 6],
    [7, 8, 9],
    10,
    11
  ],
  12,
  13,
  14,
  [15, 16, 17],
];

const newArr = oldArr.flat(Infinity);

console.log(newArr);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 ]
```

关于 `flat()`，更多的可以查阅 **MDN**：

* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat

或者查看 **阮一峰** 大佬的 ES6 讲解：

* http://es6.ruanyifeng.com/?search=%E4%B8%80%E7%BB%B4&x=0&y=0#docs/array#%E6%95%B0%E7%BB%84%E5%AE%9E%E4%BE%8B%E7%9A%84-flat%EF%BC%8CflatMap

这里大致讲下这个方法：

* **入参**：

`arr.flat(depth)`。

这个 `depth` 即拉平几层的意思，就好比：

```js
// 二维数组：默认拉平一层
[1, 2, [3, 4, [5]]].flat();
// [1, 2, 3, 4, [5]]

// 四维数组：设置拉平两层
[1, 2, [3, 4, [5, [6, 7]]]].flat(2);
// [1, 2, 3, 4, 5, [6, 7]]

// 设置拉平所有层
[1, 2, [3, 4, [5]]].flat(Infinity);
// [1, 2, 3, 4, 5]
```

* **注意事项**：

值得注意的是：使用 `flat()` 拉平数组过程中，会移除数组的空项：

```js
[1, 2, , 4, 5].flat();
// [1, 2, 4, 5]
```

* **扩展了解**：

在你运用 `flat()` 自如的时候，不妨了解下它的同辈 `flatMap()`？

* 阮一峰 - flatMap：http://es6.ruanyifeng.com/?search=%E4%B8%80%E7%BB%B4&x=0&y=0#docs/array#%E6%95%B0%E7%BB%84%E5%AE%9E%E4%BE%8B%E7%9A%84-flat%EF%BC%8CflatMap
* MDN - flatMap：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap

`flatMap()` 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。

这里不一一介绍，感兴趣的可以了解下。

> flatMap() 使用

```js
const arr = [1, 2, 3, 4];

arr.flatMap(x => x * 2);
// [2, 4, 6, 8]

arr.flatMap(x => [[x * 2]])
// [[2], [4], [6], [8]]
```

## <a name="chapter-six" id="chapter-six"></a>六 参考文献

> [返回目录](#chapter-one)

致敬在前端路上不断探索的大佬们，本篇文章参考自：

1. [《JavaScript 学习笔记 - 多维数组变为一维数组》 - MADAO是不会开花的](https://juejin.im/post/5c9dd01ef265da612647d022)
2. [《es6--javascript数组降维，从es5分析到es6，（详解reduce方法）欢迎补充》 - 程序喵timy](https://blog.csdn.net/liuchao1987330/article/details/78903151)
3. [《数组实例的-flat，flatMap》 - 阮一峰](http://es6.ruanyifeng.com/?search=%E4%B8%80%E7%BB%B4&x=0&y=0#docs/array#%E6%95%B0%E7%BB%84%E5%AE%9E%E4%BE%8B%E7%9A%84-flat%EF%BC%8CflatMap)
4. [《Array.prototype.flat() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

---

> **jsliang** 广告推送：  
> 也许小伙伴想了解下云服务器  
> 或者小伙伴想买一台云服务器  
> 或者小伙伴需要续费云服务器  
> 欢迎点击 **[云服务器推广](https://github.com/LiangJunrong/document-library/blob/master/other-library/Monologue/%E7%A8%B3%E9%A3%9F%E8%89%B0%E9%9A%BE.md)** 查看！

[![图](../../../public-repertory/img/z-small-seek-ali-3.jpg)](https://promotion.aliyun.com/ntms/act/qwbk.html?userCode=w7hismrh)
[![图](../../../public-repertory/img/z-small-seek-tencent-2.jpg)](https://cloud.tencent.com/redirect.php?redirect=1014&cps_key=49f647c99fce1a9f0b4e1eeb1be484c9&from=console)

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。