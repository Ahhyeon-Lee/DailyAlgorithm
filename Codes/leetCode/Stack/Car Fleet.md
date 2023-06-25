### Description

There are `n` cars going to the same destination along a one-lane road. The destination is `target` miles away.

You are given two integer array `position` and `speed`, both of length `n`, where `position[i]` is the position of the `ith` car and `speed[i]` is the speed of the `ith` car (in miles per hour).

A car can never pass another car ahead of it, but it can catch up to it and drive bumper to bumper **at the same speed**. The faster car will **slow down** to match the slower car's speed. The distance between these two cars is ignored (i.e., they are assumed to have the same position).

A **car fleet** is some non-empty set of cars driving at the same position and same speed. Note that a single car is also a car fleet.

If a car catches up to a car fleet right at the destination point, it will still be considered as one car fleet.

Return *the **number of car fleets** that will arrive at the destination*.

**Example 1:**

```
Input: target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
Output: 3
Explanation:
The cars starting at 10 (speed 2) and 8 (speed 4) become a fleet, meeting each other at 12.
The car starting at 0 does not catch up to any other car, so it is a fleet by itself.
The cars starting at 5 (speed 1) and 3 (speed 3) become a fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.
Note that no other cars meet these fleets before the destination, so the answer is 3.

```

**Example 2:**

```
Input: target = 10, position = [3], speed = [3]
Output: 1
Explanation: There is only one car, hence there is only one fleet.

```

**Example 3:**

```
Input: target = 100, position = [0,2,4], speed = [4,2,1]
Output: 1
Explanation:
The cars starting at 0 (speed 4) and 2 (speed 2) become a fleet, meeting each other at 4. The fleet moves at speed 2.
Then, the fleet (speed 2) and the car starting at 4 (speed 1) become one fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.

```

**Constraints:**

- `n == position.length == speed.length`
- `1 <= n <= 105`
- `0 < target <= 106`
- `0 <= position[i] < target`
- All the values of `position` are **unique**.
- `0 < speed[i] <= 106`

### Solution

- 1차선 도로에서 position에 위치한 추월할 수 없는 차들이 target 지점의 도착지에 도착할때 들어올 차 무리(fleet)의 갯수를 반환하는 문제이다.
- 1차선이므로 position 순서대로 위치한 차들은 각각 속력이 달라도 추월할 수 없고, 앞의 차를 만나면 기존에 속력이 높았더라도 앞 차의 속력으로 달려야 한다.
- 이 문제의 핵심은 target과 가까운 position부터 `(target - position) / speed` 로 각 position이 target에 도달할 수 있는 횟수를 계산하여 이전 횟수보다 적은 횟수가 나오면 하나의 fleet이 된다는 점이다.
- 우선 position 어레이는 정렬되어 있지 않으므로 speed와 묶고, target과 가까운 position 부터 계산해야하므로 이를 내림차순 정렬한다.
- 그리고 Stack을 이용하여 target과 가까운 position 부터 횟수를 계산해 스택에 넣고 peek을 뽑아 비교하면서 carList를 돌아, 최종적으로 스택에 남아있는 차의 갯수를 반환하면 fleet의 갯수를 알 수 있다.

```kotlin
import java.util.*

class Solution {
    fun carFleet(target: Int, position: IntArray, speed: IntArray): Int {
        val carList = position.zip(speed).sortedByDescending { pair -> pair.first}
        val stack = Stack<Pair<Int, Int>>()
        carList.forEach { pair ->
            if (stack.isNotEmpty()) {
                val curLeftCnt = (target - pair.first) / pair.second.toFloat()
                val peekLeftCnt = (target - stack.peek().first) / stack.peek().second.toFloat()
                if (peekLeftCnt < curLeftCnt) {
                    stack.push(pair)
                }
            } else {
                stack.push(pair)
            }
        }
        return stack.size
    }
}
```
