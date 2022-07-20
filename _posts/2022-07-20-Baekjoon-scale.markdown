---
layout: post
title:  "백준 음계 문제풀이"
date:   2022-07-20 07:37:11 +0900
categories: coding_test data_structure baekjoon
---

문제 제목 : 2920번 [음계]  
문제 난이도 : 하   
문제 유형 : 배열, 구현


<br>   

# ✏️ 문제

다장조는 c d e f g a b C, 총 8개 음으로 이루어져있다.    
이 문제에서 8개 음은 다음과 같이 숫자로 바꾸어 표현한다. c는 1로, d는 2로, ..., C를 8로 바꾼다.

1부터 8까지 차례대로 연주한다면 ascending, 8부터 1까지 차례대로 연주한다면 descending, 둘 다 아니라면 mixed 이다.    

연주한 순서가 주어졌을 때, **이것이 ascending인지, descending인지, 아니면 mixed인지 판별하는 프로그램을 작성하시오.**
* ## 입력
  첫째 줄에 8개 숫자가 주어진다.    
  이 숫자는 문제 설명에서 설명한 음이며, 1부터 8까지 숫자가 한 번씩 등장한다.


<br> 

--- 

<br>


## 🔔 아이디어
배열의 앞뒤 원소를 비교해서,    
커지면 ascending, 작아지면 descending,    
두 경우 모두 해당되지 않으면 mixed를 프린트하기


<br>


## 리스트 입력받기 
``` python
mylist = list(map(int, input().split(' ')))
```

* 입력된 문자열을 공백 기준으로 쪼개어서 리스트형으로 변환해주기   
입력 시 공백을 기준으로 입력되기 떄문!    
``` python
input().split(' ')

>> 1 2 3 4 5 6 7 8 입력 시
>> ['1', '2', '3', '4', '5', '6', '7', '8']을 반환
```
      
    
     
* 리스트 내 문자열 요소를 정수형으로 매핑해주기
``` python
map(int, input().split(' '))

>> ['1', '2', '3', '4', '5', '6', '7', '8']을 [1, 2, 3, 4, 5, 6, 7, 8]로 변환
```


<br>


## ascending, descending 변수 설정  
초기값은 ascending, descending 모두 true로 설정
``` python
ascending = True
descending = True
```


<br>


## 앞 요소, 뒷 요소의 대소 비교    
가능한 이유 : 이 문제에서는 리스트의 길이가 8로 정해져 있음    
따라서 앞뒤 요소 비교를 위해 for문을 사용하여도 크게 부담이 되지 않음!
``` python
for i in range(1, 8): # 인덱스를 for문으로 받기
                      # 뒷 요소와 앞 요소를 비교해줄 것이기 때문에 0이 아닌 1부터 시작

  if scale[i] > scale[i-1]: # 뒷 요소가 앞 요소보다 크면
    descending = False      # True였던 descending에 False로 할당

  elif scale[i] < scale[i-1]: # 뒷 요소가 앞 요소보다 작으면
    ascending = False         # True였던 ascending에 False로 할당
```
n이 1이면 1번 수행, n이 10이면 10번 수행


<br>


## 최종 결과 판단    
위 대소 비교 코드를 실행 완료한 후에는     
ascending과 descending 변수에 False나 True가 할당되어 있을 것     

* [1, 2, 3, 4, 5, 6, 7, 8] 이라면 ascending은 True, descending은 False일 것!   
* [8, 7, 6, 5, 4, 3, 2, 1] 이라면 ascending은 False, descending은 True일 것!   
* [1, 6, 2, 7, 3, 4, 8, 5] 이라면 ascending은 False, descending도 False일 것!   

``` python
if ascending:
  print('ascending')
elif descending:
  print('descending')
else:
  print('mixed')
```


<br> 

--- 

<br>


## <span style="background-color:#fff5b1;">총정리</span>
``` python
scale = list(map(int, input().split(' ')))

ascending = True
descending = False

for i in range(1, 8):
  if scale[i] > scale[i-1]:
    descending = False
  elif scale[i] < scale[i-1]:
    ascending = False

if ascending:
  print('ascending')
elif descending:
  print('descending')
else:
  print('mixed')
```

[음계]: https://www.acmicpc.net/problem/2920 