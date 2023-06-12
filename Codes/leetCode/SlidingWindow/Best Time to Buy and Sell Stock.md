### Description

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

```

**Example 2:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.

```

**Constraints:**

- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 104`

### Solution

- 첫번째 풀이는 prices를 돌며 각 인덱스의 오른쪽의 최대값을 구해 각 인덱스의 값 사이의 차를 배열에 저장해두고 그 안에서 최대값을 찾았다.
- 역시 이렇게 푸니 각 인덱스의 오른쪽 값을 구할때 slice로 오른쪽의 범위를 잘라내고 거기에서 또 max를 구하므로 시간이 오래걸렸다.

```kotlin
// 첫번째 풀이
fun maxProfit(prices: IntArray): Int {
    if (prices.size == 1) return 0

    val slice = prices.slice(1 .. prices.lastIndex)
    var max = slice.max() ?: 0
    var min = slice.min() ?: 0
    println("max : $max")
    val gaps = IntArray(prices.size - 1) { 0 }
    prices.forEachIndexed { index, price ->
        if (index == prices.lastIndex) return@forEachIndexed
        if (max == price) {
            if (min == price) return gaps.max() ?: 0
            max = prices.slice(index+1 .. prices.lastIndex).max() ?: 0
            gaps[index] = 0
        } else {
            gaps[index] = (max - price).takeIf { 0 < it } ?: 0
        }
    }

    return gaps.max() ?: 0
}
```

![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/7a477585-7548-4bbd-82bf-0252bfba8def)


- 두번째 풀이는 prices를 한 번 돌면서 비교를 통해 min을 구하고 비교를 통해 최대 profit을 구했다.
- 배열을 한번만 돌면서 비교만을 통해 최대값을 구하므로 시간복잡도 O(n)의 간단한 풀이가 되었다.

```kotlin
// 두번째 풀이
fun maxProfit(prices: IntArray): Int {
    if (prices.size == 1) return 0
    var min = prices[0]
    var profit = 0
    prices.slice(1 until prices.size).forEach {
        min = Math.min(min, it)
        profit = Math.max(profit, it - min)
    }
    return profit
}
```

![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/c407ab70-44a9-420c-97ce-464121330a90)
