### 문제 링크

[https://school.programmers.co.kr/learn/courses/30/lessons/12954](https://school.programmers.co.kr/learn/courses/30/lessons/12954)

### **문제 설명**

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

### **제한 조건**

- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.

### **입출력 예**

| x | n | answer |
| --- | --- | --- |
| 2 | 5 | [2,4,6,8,10] |
| 4 | 3 | [4,8,12] |
| -4 | 2 | [-4, -8] |

### 나의 풀이

```kotlin
fun solution(x: Int, n: Int): LongArray {
    val answer = LongArray(n)
    (0 until n).forEach {
        answer[it] = x.toLong() + x.toLong()*it
    }
    return answer
}
```

```kotlin
// 다른 사람의 풀이
fun solution(x: Int, n: Int): LongArray = LongArray(n) { x.toLong() * (it + 1) }
```

- Number Array는 n(사이즈), init(초기화 시킬 값을 넣는 람다함수)를 인자로 가지며 init에는 인덱스가 리턴되므로 그걸 이용해 초기화 값을 넣었다.
