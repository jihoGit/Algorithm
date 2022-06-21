# Lv1.약수의 개수와 덧셈

## [문제 출처](https://programmers.co.kr/learn/courses/30/lessons/77884)
&nbsp;

## 1. 설계

- 제곱근 값이 정수이면 제곱수

1. left부터 right까지 제곱근값이 제곱근을 정수처리한 값과 같은지 하나씩 비교

&nbsp;

## 2. 풀이

```python
'''
약수의 개수가 홀수인 수 : 1, 4, 9, ... 제곱수
약수의 개수가 짝수인 수 : 2, 3, 5, 6, 7, ...그 외
'''

def solution(left, right):
    answer = 0
    for v in range(left, right+1) :
        isSquare = False
        # 제곱근 값이 정수이면 제곱수
        if (v**(1/2) == int(v**(1/2))) :
            isSquare = True
        if isSquare :
            answer -= v
        else :
            answer += v
                
    return answer
```

&nbsp;

## 3. 개선할 점

- v**(1/2)대신 v**0.5쓰면 괄호를 줄일 수 있다.

