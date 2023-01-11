# 삼총사
![image](https://user-images.githubusercontent.com/68845653/211837804-94843301-6f74-4a54-8d8f-8d45d41cbafd.png)

## 문제 풀이
간단하다. 파라미터 number에서 세 수를 뽑아 더했을때 0이 되는 경우의 수를 구하는 문제다.

## 나의 풀이
```kotlin
class Solution {
    fun solution(number: IntArray): Int {
        var answer: Int = 0

        if (number.size == 3) {
            if (number.sum() == 0) answer++
        } else {
            (number.slice(0..number.size-3)).forEachIndexed { index, value -> // 첫번째 수 구하기
                if (index+1 == number.size-2) {
                    if (value + number[index+1] + number.last() == 0) {
                        answer++
                    }
                } else {
                    var sndIdx = index+1
                    (number.slice(index+1..number.size-2)).forEach { sndValue -> // 두번째 수 구하기
                        (number.slice(sndIdx+1..number.lastIndex)).forEach { thdValue -> // 세번째 수 구하기
                            if (value + sndValue + thdValue == 0) {
                                answer++
                            }
                        }
                        sndIdx+=1
                    }
                }
            }
        }

        return answer
    }
}
```
0번 인덱스부터 차례로 세 수의 조합을 만들어야 했다. 그래서 어레이의 0번 인덱스부터 차례로 세 수를 구해야 했지만 한번 만들어진 조합을 다시 만들면 안되므로 첫번째 숫자가 될 index+1 부터가 
두번째 숫자가 시작될 인덱스였다. 또한 세 수를 뽑아야 하므로 중복이 되지 않으려면 반복문 범위는 첫번째 수를 구할 땐 0번부터 끝에서 3번째 인덱스까지였고, 두번째 수를 구할 땐 끝에서 두번째
인덱스 까지였다. 이렇게 예외처리를 계속해줘야 해서 까다로운 문제였다. 이런 로직을 실전에서 쓰게 될 일이 있다면 human error가 날 확률이 매우 높다.
