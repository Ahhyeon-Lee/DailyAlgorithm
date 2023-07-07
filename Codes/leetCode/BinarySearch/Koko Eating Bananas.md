### Description

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return *the minimum integer* `k` *such that she can eat all the bananas within* `h` *hours*.

**Example 1:**

```
Input: piles = [3,6,7,11], h = 8
Output: 4

```

**Example 2:**

```
Input: piles = [30,11,23,4,20], h = 5
Output: 30

```

**Example 3:**

```
Input: piles = [30,11,23,4,20], h = 6
Output: 23

```

**Constraints:**

- `1 <= piles.length <= 104`
- `piles.length <= h <= 109`
- `1 <= piles[i] <= 109`

### Solution

- k is the most smallest number that can cousumes all the elements in piles. So the range of k is 1 ≤ k ≤ piles.max(). In this range, the sum of times(=`hour`), the result of piles’s elements divided by k, should be less or same with h.
- Since we need to find the smallest k which satisfies the above condition, we should have a `minK` and if hour is less than h, we should update `minK` to smaller one comparing to k.
- We can you binary search to find smallest k in range of k.
- We should keep comparing hours dividing piles’s elements by all the elements in k range. But without binary search it takes O(piles.max() * piles.size) time complexity.
- With binary search, we can find smallest k with O(log(piles.max()) * piles.size) time complexity.

```kotlin
class Solution {
    fun minEatingSpeed(piles: IntArray, h: Int): Int {
        var l = 1
        var r = piles.max()!!
        var minK = r

        while (l <= r) {
            val k = (l + r) / 2
            val hour = piles.fold(0) { total, num ->
                total + Math.ceil(num.toDouble() / k).toInt()
            }
            if (hour in 1 .. h) {
                r = k - 1
                minK = Math.min(minK, k)
            } else {
                l = k + 1
            }
        }
        return minK
    }
}
```
