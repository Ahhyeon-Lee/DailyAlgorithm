# 크기가 작은 부분 문자열
![image](https://user-images.githubusercontent.com/68845653/210803449-f92b7fd7-e9fa-47f2-83c6-422c79259e46.png)

## 문제 풀이
숫자로 이루어진 문자열 t와 p에서 t를 p 문자열 길이만큼 잘라 p 보다 작거나 같은 값이 있으면 갯수를 반환하는 문제이다.

## 나의 풀이
```kotlin
class Solution {
    fun firstSolution(t:String, p:String) : Int {
        var answer = 0
        val tArrayList = arrayListOf<Long>()
        for(index in 0..(t.length-p.length)) {
            val tPart = t.substring(index, index+p.length)
            tArrayList.add(tPart.toLong())
        }
        tArrayList.filter { it <= p.toLong() }.let { answer = it.size }
        return answer
    }

    fun secondSolution(t:String, p:String) : Int {
        var answer = 0
        (0..(t.length - p.length))
            .map { t.substring(it, it+p.length).toLong() }
            .filter { it <= p.toLong() }
            .let { answer = it.size }
        return answer
    }
}
```
처음에는 t 문자열을 for문을 돌려 p 길이대로 자른 값을 어레이리스트에 담아놓고 리스트의 아이템들을 p와 비교해서 문제를 풀었다.
다른 사람의 풀이를 보고 map 연산자를 쓸 수 있음을 깨달았다. t 문자열을 자를 start index의 최대값까지의 IntRange를 생성해 컬렉션 함수인 map 함수로 t 문자열을 p 문자열 길이 만큼 자른 값들의
리스트를 반환 받아 p보다 작거나 같은 아이템을 걸러내 갯수를 구했다. 그리고 다른 풀이를 보니 filter로 조건에 맞는 리스트를 받환 받을 필요 없이 count로 조건에 맞는 아이템 갯수를 바로 구할 수 있다는
것을 알았다.
