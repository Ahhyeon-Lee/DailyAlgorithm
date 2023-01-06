# 가장 가까운 같은 문자
![image](https://user-images.githubusercontent.com/68845653/210936156-bb62a74d-a6aa-4bda-869f-5590a3d08128.png)
## 문제 풀이
문자열 s에서 각 문자마다 그 앞 문자열 중 같은, 가장 가까운 인덱스의 문자를 찾아 그 문자와의 거리를 구해 Int 컬렉션을 반환하는 문제이다.
## 나의 풀이
```kotlin
fun solution(s: String): IntArray {
    var answer: IntArray = intArrayOf()
    val sList = s.chunked(1)
    sList.forEachIndexed { index, s ->
        val sameElementIndex = sList.subList(0, index).lastIndexOf(s)
        val distance = sameElementIndex.takeIf { it == -1 } ?: (index - sameElementIndex)
        answer = answer.plus(distance)
    }
    return answer
}
```
문자열 s에서 차례로 비교할 문자와 인덱스를 뽑아 해당 인덱스 앞까지 문자열 s를 잘라 비교했다. 비교할 문자와 해당 문자의 인덱스가 필요했기에 forEachIndexed 함수를 사용했지만,
다른 사람의 풀이를 보니 String의 withIndex 함수로 IndexedValue<Char>을 받을 수도 있었다. IndexedValue<T>는 index와 T 타입의 value를 갖는 데이터 클래스이다. 따라서 문자열 s를
  각 한 글자 List로 쪼개기 전에 문자열의 각 문자와 인덱스를 받을 수 있는 것이었다. 유용한 함수 하나를 알아간다.
