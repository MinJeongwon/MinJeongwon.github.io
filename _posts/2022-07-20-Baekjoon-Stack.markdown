---
layout: post
title:  "백준 스택 문제풀이"
date:   2022-07-21 08:55:11 +0900
categories: coding_test baekjoon
---

문제 제목 : 1874번 [스택]  
문제 난이도 : 하   
문제 유형 : 스택, 그리디


<br>   

# ✏️ 문제

1부터 n까지의 수를 스택에 넣었다가 뽑아 늘어놓음으로써, 하나의 수열을 만들 수 있다.      
이때, 스택에 **push하는 순서는 반드시 오름차순**을 지키도록 한다고 하자.     

임의의 수열이 주어졌을 때 스택을 이용해 그 수열을 만들 수 있는지 없는지,      
있다면 어떤 순서로 push와 pop 연산을 수행해야 하는지를 알아낼 수 있다.      

이를 계산하는 프로그램을 작성하라.

- ## 입력   
  첫 줄에 n (1 ≤ n ≤ 100,000)이 주어진다.     
  둘째 줄부터 n개의 줄에는 수열을 이루는 1이상 n이하의 정수가 하나씩 순서대로 주어진다. 물론 같은 정수가 두 번 나오는 일은 없다.

- ## 출력
  입력된 수열을 만들기 위해 필요한 연산을 한 줄에 한 개씩 출력한다.     
  **push연산은 +로, pop 연산은 -로 표현**하도록 한다.    
  **불가능한 경우 NO를 출력**한다.


<br> 

--- 

<br>


## 🔔 아이디어 🔔
* 처음에 입력되는 숫자(n)에 해당되는 개수 만큼의 양의 정수가 차례대로 입력될 것     
  즉, n=5이면 이후에 입력되는 숫자들은 1~5라는 의미    
  ➜ n개 loop을 도는 for문을 두어야 함     
  ➜ 매 loop에서 input으로 숫자를 입력받아야 함        
* input으로 받을 숫자를 저장할 스택(리스트) 하나, 동시에 +나 -를 append할 리스트 하나    
  append 시에는 +, pop 시에는 -
* 스택을 push하는 순서는 반드시 오름차순          
  ➜ 스택에 들어온 마지막 숫자부터 입력으로 받는 숫자까지 오름차순으로 append      
  ➜ 스택의 마지막 숫자가 입력으로 받는 숫자와 같다면 pop
  ➜ 스택에 들어온 마지막 숫자가 input으로 받을 숫자보다 클 경우    
  NO를 반환하여야 함


<br>


## 입력받기
첫 입력으로는 총 입력될 숫자의 갯수 n이 입력됨        
``` python 
n = int(input())
```


<br>


## 스택, +/- 리스트 선언
``` python
stack = []
result = [] # 마지막 결과로 반환해주어야 하기 때문에 변수명을 result로 둠
```


<br>


## 스택에 대해 append, pop 수행하는 코드
* append : 스택에 들어갔던 마지막 수 이후부터 입력으로 받는 숫자까지 오름차순으로 붙이기 
* pop : 입력으로 받는 숫자와 스택의 마지막 숫자가 같은 경우 반환하기    
* <span style="color:red;">!!! 스택에 append한 마지막 숫자를 저장할 변수를 만들어야 함</span>    
   
  ``` python
  last = 1 # 스택에 마지막으로 붙여진 숫자를 저장

  for i in range(n):
    number = int(input()) # 숫자 차례로 입력으로 받기

    while last<=number: # 스택에 마지막으로 붙여진 숫자가 들어오는 숫자보다 같거나 작을 때
      stack.append(last) # 스택에 n까지의 숫자를 붙임
      result.append('+') # 붙이는 연산만큼 +도 추가
      last+=1 # 붙여지는 숫자에 1씩 증가시키기 (붙이는 연산을 한 횟수가 됨)

    if stack[-1] == number: # 스택의 가장 마지막 요소가 입력되는 숫자랑 같은 경우
      stack.pop() # 해당 숫자를 반환
      result.append('-') # 반환하는 연산을 했으니 -를 붙이기

    else:
      print('NO') # 위에 해당하지 않는 경우 (오름차순으로 붙일 수 없게되는 경우)
      exit(0) # 종료

  print('\n'.join(result)) # 한 줄에 한 연산씩 출력 # 한 줄에 한 연산씩 출력
  ``` 


<br>


--- 

<br>


## <span style="background-color:#fff5b1;">총정리</span>    
메모리 : 30840     
시간 : 104ms   
``` python
n = int(input())

stack = []
result = []
last = 1 

for i in range(n):
  number = int(input())

  while last<=number: 
    stack.append(last) 
    result.append('+') 
    last+=1 

  if stack[-1] == number:
    stack.pop() 
    result.append('-') 

  else:
    print('NO')
    exit(0)

print('\n'.join(result)) 
```

[스택]: https://www.acmicpc.net/problem/1874