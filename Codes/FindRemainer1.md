# 나머지가 1이 되는 수 찾기
![image](https://user-images.githubusercontent.com/68845653/212272599-fb0fe679-43ad-4c19-a9ec-bbee6c434777.png)


## 문제 풀이
- n을 나눈 나머지가 1이 되는 수 중 가장 작은 수를 리턴한다.

## 나의 풀이
```kotlin
fun solution(n: Int): Int {
    return (2 .. sqrt((n-1).toDouble()).toInt()).firstOrNull {
        (n-1) % it == 0
    } ?: (sqrt((n-1).toDouble()).toInt() .. n).first {
        (n-1) % it == 0
    }
}
```

- 나머지가 1이 돼야 하므로 n-1의 약수 중 가장 작은 수를 구한다. 이번에도 제곱근을 이용했는데, 제곱근 이하의 범위에서 1을 제외하고 n-1의 약수가 없으면 제곱근 이상에서 다시 한번 찾도록 했다.
