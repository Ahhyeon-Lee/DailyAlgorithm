# 푸드 파이트 대회
![image](https://user-images.githubusercontent.com/68845653/211832769-d16fef66-cd0b-41f7-a4aa-067dabe641a3.png)
![image](https://user-images.githubusercontent.com/68845653/211832848-e31a1752-8e61-453f-87f1-3e66e1b21210.png)

## 문제 풀이
파라미터로 들어오는 IntArray food의 0번 인덱스를 제외한 1번 인덱스부터 끝까지는 index번 음식이며 value는 index번 음식의 갯수이다. 이걸 index번 순서로 value개의 절반씩 양 옆에
배치하고 한 가운데에는 0을 배치한 문자열을 반환하는 문제이다.

## 나의 풀이
```kotlin
class Solution {
    fun solution(food: IntArray): String {
        var answer = ""
        val repeatCntList = food.slice(1 until food.size).map { it / 2 }
        for (index in repeatCntList.indices) {
            answer += ("${index+1}".repeat(repeatCntList[index]))
        }
        return answer + "0" + answer.reversed()
    }
}
```
절반씩 배치해야하므로 index 1번부터 마지막 까지의 value를 2로 나눠 나머지는 버리고 몫대로 index+1 문자를 반복해주었다. 절반만 만들면 나머지 절반은 만들어진 문자열을 뒤집기만 하면 되므로
구하지 않아도 된다. 나는 문자열 생성을 + 연산자를 이용했지만, 다른 사람의 풀이를 보니 StringBuilder를 만들어 append로 문자열을 더하는 방법도 있었다. 또한 나는 index+1로 더할 문자열을
구했지만 그냥 반복문에 돌아갈 IntRange를 1부터 시작하면 됐다. 또한 repeat(n)으로 단순히 문자열을 n번 반복할 수도 있지만, repeat(n:Int, action:(Int)->Unit)으로 주어진 action을 
n번 반복하는 함수도 있었다. 내 풀이에서 썼다면 answer += ("${index+1}".repeat(repeatCntList[index])) 부분의 순서만 바꾸는 정도가 됐겠지만 특정 횟수만큼 특정 액션을 반복하고 싶을때 
for문으로 반복횟수 IntRange를 만들지 않아도 이 함수로 간단히 쓸 수 있을거 같다.
