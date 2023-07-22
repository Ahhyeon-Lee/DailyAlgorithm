### Description

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
Input: head = [1,2]
Output: [2,1]

```

**Example 3:**

```
Input: head = []
Output: []

```

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `5000 <= Node.val <= 5000`

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

### Solution
- ListNode in the problem is LinkedList which has next node’s reference.
![KakaoTalk_Photo_2023-07-22-23-18-27](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/8e4243c2-09b9-4815-9a64-44f8d7fe1c59)
- `head` has a reference in the direction of the black arrow like in above picture, but what we need to do is to change the reference of `next` to the direction of blue arrow in the picture.
- Therefore we need to save the previous node in `prev` and set it to current node’s `next`.
1. At first, initialize the `prev` to null and set it the first node’s `next`.
2. Then update `prev` to first node and set it to second node’s `next` when we go through the `head`.
3. `curr`, the current value of head’s loop, is updated to second node, which was `next` of first node.

After going through the process above, prev will have reversed ListNode of head. Then we return it.
```kotlin
/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun reverseList(head: ListNode?): ListNode? {
        if (head == null) return head

        var prev: ListNode? = null
        var curr = head

        while (curr != null) {
            val next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        }

        return prev
    }
}
```
