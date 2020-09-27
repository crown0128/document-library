Number - 数字化金额
===

> Create by **jsliang** on **2020-09-27 23:15:09**  
> Recently revised in **2020-09-27 23:24:58**

<!-- 目录开始 -->
## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 前言](#chapter-two) |
| <a name="catalog-chapter-three" id="catalog-chapter-three"></a>[三 for 遍历](#chapter-three) |
| <a name="catalog-chapter-four" id="catalog-chapter-four"></a>[四 API 方案一](#chapter-four) |
| <a name="catalog-chapter-five" id="catalog-chapter-five"></a>[五 API 方案二](#chapter-five) |
| <a name="catalog-chapter-six" id="catalog-chapter-six"></a>[六 正则](#chapter-six) |
<!-- 目录结束 -->

## <a name="chapter-two" id="chapter-two"></a>二 前言

> [返回目录](#chapter-one)
  
将 `1234567890` 转为 `1,234,567,890`。

参考文献：

* [js，正则实现金钱格式化](https://blog.csdn.net/qq_36279445/article/details/78889305)

## <a name="chapter-three" id="chapter-three"></a>三 for 遍历

> [返回目录](#chapter-one)
  
```js
const num = String(1234567890);
let result = '';

for (let i = num.length - 1; i >= 0; i--) {
  if (i !== num.length - 1 && i % 3 === 0) {
    result = num[i] + ',' + result;
  } else {
    result = num[i] + result;
  }
}

console.log(result);
```

## <a name="chapter-four" id="chapter-four"></a>四 API 方案一

> [返回目录](#chapter-one)
  
```js
console.log(
  String(1234567890).split('').reverse().reduce((prev, next, index) => (index % 3) === 0 ? next + ',' + prev : next + prev)
);
```

## <a name="chapter-five" id="chapter-five"></a>五 API 方案二

> [返回目录](#chapter-one)
  
```js
console.log(
  (1234567890).toLocaleString('en-US')
);
```

## <a name="chapter-six" id="chapter-six"></a>六 正则

> [返回目录](#chapter-one)
  
```js
String(1234567890).replace(/\B(?=(\d{3})+(?!\d))/g, ',');
```

---

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。