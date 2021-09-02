## [删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

**进阶：**你能尝试使用一趟扫描实现吗？

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```



**快慢指针**

- 因为链表没有下标，无法直接定位到倒数第n个位置，可以用两个指针，一快一慢来解决
- 先定义虚拟头部，把虚拟头部的指针指向head，为了可以找回来head
- 然后定义fast，先移动n个位置
- 然后快慢指针一起移动，当fast的next指针为空时，证明已经到了底部节点，这时slow的节点刚好是要删除元素的上级，方便我们转换指针
- 然后把slow的指针指向要删除元素的下一个元素，要删除元素的指针变为null，这样gc就能回收要删除指针
- 再把虚拟头部的指针return出去

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
    const vi = new ListNode(0, head)
    let  fast = vi, slow = vi
    //快指针先移动
    for(let i = 0; i < n; i++) {
        fast = fast.next
    }
   
	  //一起移动，找删除元素的上级
    while(fast.next) {
        fast = fast.next
        slow = slow.next
    }
	  //删除指针
    const deleNode = slow.next
    slow.next = deleNode.next
    deleNode.next = null

   
    return vi.next
};
```

