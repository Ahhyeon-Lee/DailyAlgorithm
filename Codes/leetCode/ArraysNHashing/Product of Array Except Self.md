### Description

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]

```

**Example 2:**

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]

```

**Constraints:**

- `2 <= nums.length <= 105`
- `30 <= nums[i] <= 30`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1)` extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

### Solution

- 이 문제의 핵심은 나누기 연산자를 사용하지 않고 O(n)의 시간 복잡도를 가지며 O(1)의 공간복잡도를 가지도록 해결하는 것이다.

```kotlin
fun productExceptSelf(nums: IntArray): IntArray {
    var prefix = 1
    val answer = IntArray(nums.size) { 0 }
    for (i in 0 until nums.size) {
        answer[i] = prefix
        prefix *= nums[i]
    }
    var postfix = 1
    for (i in nums.size-1 downTo 0) {
        answer[i] = answer[i]!! * postfix
        postfix *= nums[i]
    }
    return answer
}
```

- prefix는 반복문을 돌며 현재 인덱스 앞까지 수들의 곱, postfix는 현재 인덱스 뒷 수들의 곱을 뜻한다.
- 우선 현재 인덱스 앞까지 수들의 곱을 answer에 담은 후, 다시 nums를 뒤에서부터 돌면서 현재 인덱스 뒤까지의 수들을 다시 곱해주면 결국 answer에는 현재 인덱스를 제외한 수들의 곱이 들어가면서, 각 곱들을 구하는 것도 이전에 구했던 곱에 다음 수를 곱하기만 하면 되므로 같은 수를 반복적으로 곱하는 일도 없다.
