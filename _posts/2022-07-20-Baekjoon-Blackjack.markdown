---
layout: post
title:  "백준 블랙잭 문제풀이"
date:   2022-07-20 08:55:11 +0900
categories: coding_test data_structure baekjoon
---

문제 제목 : 2798번 [블랙잭]  
문제 난이도 : 하   
문제 유형 : 배열, 완전탐색


<br>   

# ✏️ 문제

카지노에서 제일 인기 있는 게임 블랙잭의 규칙은 상당히 쉽다.     
카드의 합이 21을 넘지 않는 한도 내에서, 카드의 합을 최대한 크게 만드는 게임이다.      
블랙잭은 카지노마다 다양한 규정이 있다.

한국 최고의 블랙잭 고수 김정인은 새로운 블랙잭 규칙을 만들어 상근, 창영이와 게임하려고 한다.    
김정인 버전의 블랙잭에서 각 카드에는 양의 정수가 쓰여 있다.     
그 다음, 딜러는 N장의 카드를 모두 숫자가 보이도록 바닥에 놓는다.     
그런 후에 딜러는 숫자 M을 크게 외친다.

이제 플레이어는 제한된 시간 안에 N장의 카드 중에서 3장의 카드를 골라야 한다.     
블랙잭 변형 게임이기 때문에, 플레이어가 **고른 카드의 합은 M을 넘지 않으면서 M과 최대한 가깝게** 만들어야 한다.   

N장의 카드에 써져 있는 숫자가 주어졌을 때, **M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합**을 구해 출력하시오.

- ## 입력   
  첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다.    
  둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는 양의 정수이다.    
  합이 M을 넘지 않는 카드 3장을 찾을 수 있는 경우만 입력으로 주어진다.


<br> 

--- 

<br>


## 🔔 아이디어
주어진 카드에서 세 장을 뽑는 방법 ➜ itertools, for문    
M보다 작거나 같은 합 중 가장 큰 합을 찾기

<br>


## 입력받기
두 줄에 걸쳐 입력이 주어지는 경우    
``` python 
card_len, M = map(int, input().split(' ')) # 첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다.    
cards = list(map(int, input().split(' '))) # 둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는 양의 정수이다.    
```


<br>


## 방법 1. itertools 사용
## itertools로 조합의 합 구하기   
* itertools의 combination      
  combinations 함수를 사용하면 모든 조합의 경우가 출력됨    
  ``` python
  from itertools import combination
  combinations(cards, 3)
  >>> (5, 6, 7)
  (5, 6, 8)
  (5, 6, 9)
  (5, 7, 8)
  (5, 7, 9)
  (5, 8, 9)
  (6, 7, 8)
  (6, 7, 9)
  (6, 8, 9)
  (7, 8, 9)
  ```

* 이 문제에서는 합을 구해야하므로 합 계산을 바로 수행하기
  ``` python
  from itertools import combinations
  
  for card in combinations(cards, 3):
    cardsum = sum(card)
  ```


<br>


## temp 변수 활용하여 비교하기
``` python
sum_result = 0 # 최종으로 프린트해줄 합

for card in combinations(cards, 3):
    # cardsum = sum(card) 
    sum_temp = sum(card) # 합 변수를 temp 변수로 생각
    
    if sum_result < sum_temp <= M: # 합이 이제껏 저장했던 합(sum_result)보다 크면서 M 이하일 때
        sum_result = sum_temp # 프린트해줄 값(sum_result)을 현재 들어온 합(sum_temp)으로 업데이트해주기

  print(sum_temp)
  ```


<br>


## 방법 2. for문 사용
## for문으로 조합의 합 구하기
인덱스 세 개 추출해서 합을 구하기
``` python
for a in range(0, card_len): # 0 ~ (길이-1) 에서 하나 뽑고
  for b in range(a+1, card_len): # (뽑은 인덱스의 다음 인덱스) ~ (길이-1) 에서 또 하나 뽑고
    for c in range(b+1, card_len): # (뽑은 인덱스의 다음 인덱스) ~ (길이-1) 에서 또 하나 뽑기
      cardsum = cards[a]+cards[b]+cards[c] # 인덱스 세 개로 값을 얻어 모두의 합 구하기
```


<br>


## M보다 크지 않으면서 가장 가까운 값을 구하기    
모든 값의 합으로 구한 cardsum이 M보다 크지 않는 경우에 한해서    
M보다 가장 가까운 경우를 리턴해주어야 함     
``` python
result = 0 # 비교대상 변수를 두기

if cardsum <= M: # cardsum이 M보다 크지 않다면
  result = max(cardsum, result)

print(result)
```


<br> 

--- 

<br>


## <span style="background-color:#fff5b1;">총정리-itertools를 사용하는 방법</span>    
메모리 : 30840     
시간 : 104ms   
``` python
from itertools import combinations

card_len, M = map(int, input().split(' ')) 
cards = list(map(int, input().split(' '))) 

sum_result = 0 

for card in combinations(cards, 3):
    sum_temp = sum(card) 
    
    if sum_result < sum_temp <= M:
        sum_result = sum_temp

print(sum_temp)
```


<br>


## <span style="background-color:#fff5b1;">총정리-for문을 사용하는 방법</span>     
메모리 : 30840     
시간 : 140ms        
``` python
card_len, M = map(int, input().split(' ')) 
cards = list(map(int, input().split(' '))) 

result = 0 

for a in range(0, card_len): 
  for b in range(a+1, card_len):
    for c in range(b+1, card_len):
      cardsum = cards[a]+cards[b]+cards[c]

      if cardsum <= M:
        result = max(cardsum, result)

print(result)
```

[블랙잭]: https://www.acmicpc.net/problem/2798