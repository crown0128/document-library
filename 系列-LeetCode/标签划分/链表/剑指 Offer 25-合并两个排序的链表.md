剑指 Offer 25 - 合并两个排序的链表
===

> Create by **jsliang** on **2020-08-10 16:56:44**  
> Recently revised in **2020-09-04 14:34:45**

## <a name="chapter-one" id="chapter-one"></a>一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| <a name="catalog-chapter-two" id="catalog-chapter-two"></a>[二 题目](#chapter-two) |
| <a name="catalog-chapter-three" id="catalog-chapter-three"></a>[三 解题思路](#chapter-three) |
| <a name="catalog-chapter-four" id="catalog-chapter-four"></a>[四 解题套路](#chapter-four) |

## <a name="chapter-two" id="chapter-two"></a>二 题目

> [返回目录](#chapter-one)

```
输入两个递增排序的链表，
合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

限制：
0 <= 链表长度 <= 1000

注意：本题与主站 21 题相同：https://leetcode-cn.com/problems/merge-two-sorted-lists/

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {

};
```

根据上面的已知函数，小伙伴们可以先尝试破解本题，确定了自己的答案后再看下面代码。

## <a name="chapter-three" id="chapter-three"></a>三 解题思路

> [返回目录](#chapter-one)

* 递归（未优化，详尽注释）

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @name 构造函数-构造链表
 * @param {*} val 初始化的值，可以不传，默认为 0
 * @param {*} next 初始化的下一个链表，可以不传，默认为 null
 */
const ListNode = function(val, next) {
  this.val = val || 0;
  this.next = next || null;
}

/**
 * @name 解题函数
 * @param {ListNode} l1 第一个链表
 * @param {ListNode} l2 第二个链表
 * @return {ListNode} 返回的新链表
 */
const mergeTwoLists = (l1, l2) => {
  // 1. 初始化一个链表
  const newListNode = new ListNode();
  
  // 3. 开始递归
  const recursion = (tempListNode, l1, l2) => {
    // 3.1 如果左链表和右链表都空了，那就结束本次递归
    if (!l1 && !l2) {
      return;
    }

    // 3.2 如果左链表或者右链表空了，那么当前的 result 追加有的那个，也结束本次递归
    if (!l1 || !l2) {
      tempListNode.next = l1 || l2;
      return;
    }

    // 3.3 重点：初始化一个新链表，用来获取下一个新节点
    // 这里配合点 4 来看比较容易懂
    tempListNode.next = new ListNode();
    tempListNode = tempListNode.next;

    // 3.4 排序，同时将采纳了的链表往后挪一位
    if (l1.val >= l2.val) {
      tempListNode.val = l2.val;
      l2 = l2.next;
    } else {
      tempListNode.val = l1.val;
      l1 = l1.next;
    }

    // 3.4 继续下一次递归
    recursion(tempListNode, l1, l2);
  };
  // 2. 传入这个链表，和 l1、l2
  recursion(newListNode, l1, l2);

  // 4. 重点：我们初始化的时候，有一个没用的链表，记得往后挪一位
  return newListNode.next;
};

const l1 = {
  val: 1,
  next: {
    val: 2,
    next: { val: 4, next: null },
  },
};

const l2 = {
  val: 1,
  next: {
    val: 3,
    next: { val: 4, next: null },
  },
};

console.log(mergeTwoLists(l1, l2));
```

* 递归（优化）

下面这种解法一般不容易搞出来，如果对递归不熟，那还是看前面那种解法吧。

```js
const mergeTwoLists = (l1, l2) => {
  if (!l1) {
    return l2;
  } else if (!l2) {
    return l1;
  } else if (l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l2.next, l1);
    return l2;
  }
};
```

* 迭代

如果递归的第一种解法通了，那么迭代的方法也是可以相通的：

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
const mergeTwoLists = (l1, l2) => {
  const newList = {
    val: -1,
    next: null,
  };
  let tempList = newList;

  while (l1 && l2) {
    if (l1.val <= l2.val) {
      tempList.next = l1;
      l1 = l1.next;
    } else if (l1.val > l2.val) {
      tempList.next = l2;
      l2 = l2.next;
    }
    tempList.next.next = null;
    tempList = tempList.next;
  }

  tempList.next = l1 || l2;

  return newList.next;
};

const l1 = {
  val: 1,
  next: {
    val: 2,
    next: { val: 4, next: null },
  },
};

const l2 = {
  val: 1,
  next: {
    val: 3,
    next: { val: 4, next: null },
  },
};

console.log(mergeTwoLists(l1, l2));
```

## <a name="chapter-four" id="chapter-four"></a>四 套路分析

> [返回目录](#chapter-one)

本题暂未发现任何套路，如果有但是 **jsliang** 后面发现了的话，会在 GitHub 进行补充。

如果小伙伴有更好的思路想法，或者没看懂其中某种解法，欢迎评论留言或者私聊 **jsliang**~

---

**不折腾的前端，和咸鱼有什么区别！**

![图](https://github.com/LiangJunrong/document-library/blob/master/public-repertory/img/z-index-small.png?raw=true)

**jsliang** 会每天更新一道 LeetCode 题解，从而帮助小伙伴们夯实原生 JS 基础，了解与学习算法与数据结构。

**浪子神剑** 会每天更新面试题，以面试题为驱动来带动大家学习，坚持每天学习与思考，每天进步一点！

扫描上方二维码，关注 **jsliang** 的公众号（左）和 **浪子神剑** 的公众号（右），让我们一起折腾！

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">jsliang 的文档库</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。