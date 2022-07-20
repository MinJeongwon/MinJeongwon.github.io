---
layout: post
title:  "알고리즘의 복잡도"
date:   2022-07-18 08:43:11 +0900
categories: algorithm
use_math: true
comments: true
---
Big O 표기법


<br>   

## ✏️ **알고리즘의 복잡도 계산이 왜 필요할까?** 

* 동일한 문제를 풀 때 사람마다 다양한 방법으로 접근    
* **복잡도**는 여러 알고리즘 중 어떤 알고리즘이 가장 좋은지 판단하는 기준이 됨  
* 알고리즘의 성능 표기
  1. 시간 복잡도 - 알고리즘을 수행하는 데 요구되는 연산의 횟수
     * $O$  : 가장 일반적으로 사용되는 복잡도 표현 방식으로, 최악의 실행 시간을 나타냄
     * $\Omega$ : 최선의 실행 시간을 나타냄
     * $\Theta$ : 평균 실행 시간을 나타냄
  2. 공간 복잡도 : 알고리즘을 수행하는 데 필요한 메모리의 크기 

<br>

---
# 표기법 : $O(  )$
### $O(1)<O(logn)<O(n)<O(nlogn)<O(n^2)<O(2^n)<O(n!)$ 

<p align="center">
  <img src="https://velog.velcdn.com/images/leeseungsoo0701/post/17715e7a-f599-44f9-9359-ca0470d84326/big-O.png" width="500">    
</p>



### $O(1)$ 
입력에 상관 없이 무조건 상수 회 실시하기 때문에,    
입력해주는 값이 매우 크더라도 실행 시간이 일정함     
``` python
if n>100:
  print("Hello world!")
```



### $O(n)$  
입력과 코드 실행에 걸리는 시간이 비례함     
``` python
for i in range(n):
  print(i)
```
n이 1이면 1번 수행, n이 10이면 10번 수행



### $O(n^2)$    
코드 실행 시간이 입력의 제곱만큼 드는 경우
``` python
for i in range(n):
  for j in range(n):
    print(i)
```
n이 1이면 1번 수행, n이 10이면 10번 수행

<br>

## 🖍️예시로 이해해보기    
1부터 n까지의 정수를 모두 더하는 코드   
* 1번 코드 
  ```python
  def sum_n(n):
    total = 0
    for i in range(1, n+1):
      total+=i
    return total
  ```
* 2번 코드 
  ```python
  def sum_n(n):
    total = int(0.5*n*(n+1))
    return total
  ```

1번 코드는 n이 큰 수일수록 여러 라인(for문)을 실행하여야 하지만  $O(n)$      
2번 코드는 n이 큰 수이든 작은 수이든 한 라인을 실행 $O(1)$ 하고 실행을 종료한다.    
즉, **같은 작업을 수행하는 코드이더라도 <span style="background-color:#fff5b1;">복잡도</span>에 따라 다른 성능을 가질 수 있다**


<br>

== reference ==  
[big O 그래프]

[big O 그래프]: https://velog.io/@leeseungsoo0701/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9D%B8%ED%84%B0%EB%B7%B04%EC%9E%A5%EB%B9%85%EC%98%A4%EC%9E%90%EB%A3%8C%ED%98%95