### Description

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![Untitled](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9

```

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

### Solution

- 이 문제를 풀기 위해 알아야할 포인트
    1. 현재 인덱스를 기준으로 현재 인덱스 제외 **왼쪽과 오른쪽 각각의 Max**가 현재 인덱스에 물을 담을 수 있는 벽이다. (이걸 알아내는게 중요할거 같다.)
    2. 왼쪽과 오른쪽 각 Max 중 작은 값이 담을 수 있는 물의 높이이다.
    3. (작은 값 - 현재 인덱스의 높이)가 현재 인덱스에 담기는 물의 양이다. (0 초과일 경우)
- 첫번째 풀이(오답 : 정답률 반토막 / Two Pointer 방법)
    
    ```kotlin
    fun trap(height: IntArray): Int {
        var l = 0
        var r = height.lastIndex
        var lMax = height[l]
        var rMax = height[r]
        var total = 0
    
        while(l < r) {
            if (lMax <= height[l]) {
                lMax = height[l]
                l++
            } else {
                while (l <= r && height[l] < lMax) {
                    total += (lMax - height[l])
                    l++
                }
            }
    
            if (rMax <= height[r]) {
                rMax = height[r]
                r--
            } else {
                while (l <= r && height[r] < rMax) {
                    total += (rMax - height[r])
                    r--
                }
            }
        }
    
        return total
    }
    ```
    
    - 첫번째 풀이의 문제는 번갈아가며 l과 r을 옮기는 시점이 틀렸다는 것이다.
    - Two Pointer는 l과 r을 번갈아 가며 폭을 좁혀오는 시점이 중요한거 같다..

- 두번째 풀이(정답 : Two Pointer 안씀)
    
    ```kotlin
    fun trap(height: IntArray): Int {
        if (height.size == 2) return 0
        var curIndex = 1
        var lMax = height[0]
        var rMax = height.slice(curIndex+1 until height.size).max() ?: 0
        var total = 0
    
        while (curIndex < height.lastIndex) {
            total += (Math.min(lMax, rMax) - height[curIndex]).coerceAtLeast(0)
            curIndex++
            lMax = Math.max(lMax, height[curIndex-1])
            rMax = if (height[curIndex] >= rMax) {
                height.slice(curIndex+1 until height.size).max() ?: 0
            } else rMax
        }
    
        return total
    }
    ```
    
    - 현재 인덱스를 기준으로 왼쪽과 오른쪽의 Max 값을 찾는데 원론적인 방법을 쓴 풀이이다.
    - 포인터를 하나만 써서 height를 한 번만 돌면서 현재 인덱스 양 옆의 맥스 값을 구했다.
    - 이후 나오는 Two Pointer 사용 정답보다 런타임 시간이 약 10배 더 걸렸다.
    - 오른쪽의 Max 값을 구할때 slice 해서 그 안에서 max() 값을 찾아서 그런거 같다.
    
    ![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/61de2529-00ef-4c74-9a85-b413d3f940fc)
    

- 두번째 풀이(정답 : Two Pointer 방법)
    
    ```kotlin
    fun trap(height: IntArray): Int {
        var total = 0
        var l = 0
        var r = height.lastIndex
        var lMax = height[l]
        var rMax = height[r]
    
        while (l < r) {
            if (height[l] <= height[r]) {
                l++
                lMax = max(lMax, height[l])
                total += (lMax - height[l]).coerceAtLeast(0)
            } else {
                r--
                rMax = max(rMax, height[r])
                total += (rMax - height[r]).coerceAtLeast(0)
            }
        }
        return total
    }
    ```
    
    - 첫번째 풀이에서는 l과 r을 움직여야 하는 시점을 판단하는게 잘못됐던거 같다.
    - 정답 풀이에서는 l과 r 포인터의 값 대소를 비교해 어느쪽을 움직여야할지 정한다. (l ≤r 인지 r ≤ l 인지는 상관 없다. 중요한건 양 포인터 값의 대소를 비교해서 포인터를 옮긴다는 것.)
    - l과 r을 비교하는 이유는 각 사이드의 최대값을 유지하고, 나머지 한 쪽이 막혀있다는 것을 보장하기 위해서이다.
    - 왼쪽이 오른쪽보다 작을때 움직여야 오른쪽은 막혀있다는 것을 보장한 상태로 왼쪽의 최대값에서 현재 포인터의 값을 빼서 현재 포인터에서 담을 수 있는 물의 양을 알 수 있기 때문이다.
    - 이걸 알아야 포인터를 움직이면서 1. 각 포인터의 현재 인덱스의 왼쪽과 오른쪽 벽이 막혀있는지 알 수 있고(물을 담을 수 있는지), 2. 두 쪽 중 최소값을 알아 어느 높이까지 물을 담을 수 있을지 알수 있으며, 3. 그 상태에서 현재 인덱스의 높이와 비교해 담을 수 있는 물의 양을 계산할 수 있다.
    
    ![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/ec1773e8-b1ed-4522-8533-db2dd6820d23)
