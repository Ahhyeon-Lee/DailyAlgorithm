# 없는 숫자 더하기

날짜: January 14, 2023
태그: level 1

## 없는 숫자 더하기

![Untitled](%E1%84%8B%E1%85%A5%E1%86%B9%E1%84%82%E1%85%B3%E1%86%AB%20%E1%84%89%E1%85%AE%E1%86%BA%E1%84%8C%E1%85%A1%20%E1%84%83%E1%85%A5%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%201a4e0ded47fd46ba9f800ce203aeafd5/Untitled.png)

## 나의 풀이

```kotlin
fun solution(numbers: IntArray): Int {
    numbers.sort()
    val newList = (0..9).toMutableList()
    newList.removeAll(numbers.asList())
    return newList.sum()
}
```

- 0부터 9까지의 리스트를 만들어 numbers에 해당하는 수들을 제거하고 합계를 냈다.

## 다른 사람의 풀이

```kotlin
fun solution1(numbers: IntArray): Int = 
	(0..9).filterNot(numbers::contains).sum()

fun sameWith1(numbers: IntArray): Int = 
	(0..9).filterNot {
        numbers.contains(it)
    }.sum()

fun solution2(numbers: IntArray): Int = 
	45 - numbers.sum()
```

- solution1은 더블 콜론 함수 참조로 numbers에 없는 값을 뽑아 더했다. 내 풀이와 동일한 로직이지만 코틀린 문법에 대한 이해도가 훨씬 높은 풀이이다.
- solution2는 기발한 방법이었다.