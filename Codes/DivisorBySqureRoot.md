# 기사단원의 무기
<img width="806" alt="image" src="https://user-images.githubusercontent.com/68845653/211183341-f6becac8-4450-4f58-9521-52a6f4ff53c7.png">
<img width="795" alt="image" src="https://user-images.githubusercontent.com/68845653/211183351-e591d982-2dc1-4bf4-99d4-c6206de0005b.png">

## 문제 풀이
1부터 number까지의 번호의 약수의 갯수 중 limit이 넘는 수는 power로 치환하여 나온 값들을 모두 더하여 반환하는 것이다.

## 나의 풀이
```kotlin
class Solution {
    fun solution(number: Int, limit: Int, power: Int): Int {
        return (1 .. number).map { num ->
            var count = 0
            (1..sqrt(num.toDouble()).toInt()).forEach {
                if (num % it == 0) {
                    count += if (num / it == it) { 1 } else { 2 }
                }
            }
            count
        }.sumOf {
            it.takeIf { it <= limit } ?: power
        }
    }
}
```
이 문제의 핵심은 약수의 갯수를 구할때 시간을 단축시키는 것이다. 평범하게 1..num까지의 수를 모두 돌아가면서 나머지가 0인 값의 갯수를 구하는 식으로 하면 시간 초과 오류가 난다.
약수는 숫자의 제곱근 이하 숫자까지만 구하면 나눈 몫이 또다른 약수가 되기 때문에 숫자를 전부 돌면서 구할 필요가 없다. 따라서 제곱근을 통해 문제를 풀 수 있다. 제곱근 이하의 숫자들로 나눠서
약수를 구해 약수와 약수로 나눈 몫이 같다면 총 약수 갯수에는 1만 더해 주고 다르다면 2를 더해주었다. 제곱근은 스스로만 두번 곱하면 되므로 약수가 한개 이고, 제곱근이 아니라면 약수가 두개로 한 쌍이 되므로
그렇게 더했다. 이렇게 제곱근을 이용해서 풀면 시간 복잡도가 O(√N)이 되므로 들어오는 값이 커질수록 연산 시간이 증가하긴 하겠지만 기울기는 완만할 것으로 보인다. 다른 사람의 풀이를 보니 sumOf 대신 fold
함수를 쓴 풀이도 있었다. 이 문제에서는 둘다 동일한 방식으로 작동했지만 다른 문제를 풀때 fold 함수를 써볼 수 있을거 같다.
