# 🔗 链表

## [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

思路：用一个 prev 节点保存向前指针，temp 保存向后的临时指针

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    for head != nil {
        // prev head   tmp = head.Next
        // null  1      2->3->4->5
        tmp := head.Next
        // prev   head
        // null <- 1   
        head.Next = prev
        prev = head
        head = tmp
    }
    return prev
}
```

## [92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseBetween(head *ListNode, left int, right int) *ListNode {
    dummy := &ListNode{Val: -1, Next: head}

    pre := dummy
    for i := 0; i < left - 1; i++ {
        pre = pre.Next
    }

    cur := pre.Next
    for i := 0; i < right - left; i++ {
        next := cur.Next
        cur.Next = next.Next
        next.Next = pre.Next
        pre.Next = next
    }
    return dummy.Next
}
```
