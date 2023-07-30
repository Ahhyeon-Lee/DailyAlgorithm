### Description

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return *the head of the merged linked list*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]

```

**Example 2:**

```
Input: list1 = [], list2 = []
Output: []

```

**Example 3:**

```
Input: list1 = [], list2 = [0]
Output: [0]

```

**Constraints:**

- The number of nodes in both lists is in the range `[0, 50]`.
- `100 <= Node.val <= 100`
- Both `list1` and `list2` are sorted in **non-decreasing** order.

### Solution

- The approach to solving problem is not difficult. To a dummy ListNode, add a smaller number comparing list1 and list2.
- But the problem to me was to understand `tail` and `dummy`.
    1. `tail` has a reference of `dummy`. So putting a value in `tail.next` equals to putting value in `dummy.next`.
    2. Update tail value of dummy by reassigning `tail.next` to `tail`.
- I think the point is to understand two above things.

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
    fun mergeTwoLists(list1: ListNode?, list2: ListNode?): ListNode? {
        val dummy = ListNode(0)
        var tail = dummy
        
        var curr1 = list1
        var curr2 = list2
        
        while (curr1 != null && curr2 != null) {
            if (curr1.`val` < curr2.`val`) {
                tail.next = curr1
                curr1 = curr1.next
            } else {
                tail.next = curr2
                curr2 = curr2.next
            }
            tail = tail.next
        }
        
        if (curr1 != null) {
            tail.next = curr1
        } else if (curr2 != null) {
            tail.next = curr2
        }
        
        return dummy.next
    }
}
```
