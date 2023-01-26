# 과일장수
![image](https://user-images.githubusercontent.com/68845653/211226274-0379fc44-25e2-4063-82d9-24386af574fd.png)

## 문제 풀이
IntArray로 들어오는 사과들의 점수들중 높은 순서대로 m개당 나눠서(m개 미만은 버림) 각 묶음의 최하점을 m으로 곱한 값을 반환하는 문제이다.

## 나의 풀이
```kotlin
class Solution {
    fun solution(k: Int, m: Int, score: IntArray): Int {
        return if (m > score.size) {
            0
        } else {
            score.sortedDescending().chunked(m).filter {
                it.size >= m
            }.map {
                it.minOf { it }
            }.sumOf {
                it*m
            }
        }
    }
}
```
score를 내림차순하여 chunked로 m개당 나누고 나눈 각 묶음 속 사과 갯수가 m개 미만인 묶음은 버려서 최소값을 구해 m으로 곱했다.
