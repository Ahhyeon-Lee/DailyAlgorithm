# 명예의 전당
![image](https://user-images.githubusercontent.com/68845653/211159049-58d6f1d5-19ae-4433-a048-eb60ee74fad6.png)

## 문제 풀이
매일 참가자의 점수가 담긴 IntArray의 score가 들어오면 매일 k명만 들어갈 수 있는 명예의 전당 리스트들에서 최소점만 뽑은 IntArray를 반환하는 문제이다.
## 나의 풀이
```kotlin
class Solution {
    fun solution(k: Int, score: IntArray): IntArray {
        val topList = mutableListOf<IntArray>()
        val range = if (score.size < k) (score.indices) else (0 until k)
        range.forEach { count ->
            topList.add(score.slice(0..count).toIntArray())
        }
        if (k < score.size) {
            (k until score.size).forEach { index ->
                val newArray = topList.last().plus(score[index])
                topList.add(newArray.sorted().drop(1).toIntArray())
            }
        }
        val answer = topList.map {
            it.sorted().first()
        }.toIntArray()
        return answer
    }
}
```
k일 까지는 새로 들어온 참가자의 점수가 모두 명예의 전당에 올라가므로 k일 전후로 명예의 전당 추가 로직을 나눠야 했다. 또한 k 순위 보다 적게 참가자 score 어레이가 들어왔을 수도 있으니 이 역시 구분해서
풀었다. 문제를 푼 순서는 1.k번째까지의 topList 구하기 2.k번 이후의 topList 구하기 3.만들어진 topList에서 최소값 뽑기였다. 솔루션을 작성하면서 순서를 정리했지만, 솔루션을 작성하기 전에 문제를 
먼저 해석하면서 순서를 정하고 솔루션을 도출하는게 어려운 문제일수록 좋은 접근법이 될거 같아 다음 문제부터는 순서를 바꿔보고자 한다.
