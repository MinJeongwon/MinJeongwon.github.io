---
layout: post
title:  "백준 키로거 문제풀이"
date:   2022-07-25 10:46:13 +0900
categories: coding_test baekjoon
---

문제 제목 : 5397번 [키로거]  
문제 난이도 : 중   
문제 유형 : 스택, 구현, 그리디


<br>   

# ✏️ 문제

창영이는 강산이의 비밀번호를 훔치기 위해서 강산이가 사용하는 컴퓨터에 키로거를 설치했다.    
며칠을 기다린 끝에 창영이는 강산이가 비밀번호 창에 입력하는 글자를 얻어냈다.    
키로거는 사용자가 키보드를 누른 명령을 모두 기록한다.     
따라서, 강산이가 비밀번호를 입력할 때, 화살표나 백스페이스를 입력해도 정확한 비밀번호를 알아낼 수 있다. 

강산이가 비밀번호 창에서 입력한 키가 주어졌을 때, 강산이의 비밀번호를 알아내는 프로그램을 작성하시오.     
강산이는 키보드로 입력한 키는 알파벳 대문자, 소문자, 숫자, 백스페이스, 화살표이다.

- ## 입력   
  첫째 줄에 테스트 케이스의 개수가 주어진다.     
  각 테스트 케이스는 한줄로 이루어져 있고, 강산이가 입력한 순서대로 길이가 L인 문자열이 주어진다. (1 ≤ L ≤ 1,000,000)       
  강산이가 백스페이스를 입력했다면, '-'가 주어진다.     
  이때 커서의 바로 앞에 글자가 존재한다면, 그 글자를 지운다.     
  화살표의 입력은 '<'와 '>'로 주어진다.     
  이때는 커서의 위치를 움직일 수 있다면, 왼쪽 또는 오른쪽으로 1만큼 움직인다.    
  나머지 문자는 비밀번호의 일부이다.     
  물론, 나중에 백스페이스를 통해서 지울 수는 있다.    
  만약 커서의 위치가 줄의 마지막이 아니라면, 커서 및 커서 오른쪽에 있는 모든 문자는 오른쪽으로 한 칸 이동한다.

- ## 출력
  각 테스트 케이스에 대해서, 강산이의 비밀번호를 출력한다.     
  비밀번호의 길이는 항상 0보다 크다.    


<br> 

--- 

<br>


## 🔔 아이디어 🔔
* `커서`를 움직이면 시간초과가 될 수 있음        
  ➜ 커서를 가운데 두어, 커서 왼쪽의 문자를 left라는 배열에, 커서 오른쪽의 문자를 right라는 배열에 담기      
  ➜ 결과로는 left배열과 right배열 거꾸로를 합한 배열을 스트링형식으로 반환하여야 함


<br>


## 입력받기
첫 줄에는 테스트케이스 개수가 입력됨         
``` python 
test_case = int(input())
```


<br>


## for문을 통해 한 케이스별로 처리
## 케이스별 1) 입력을 받고 2) left 3) right 배열 만들기
``` python
for _ in range(test_case):
  password = input()
  left = []
  right = []
```


<br>


## 패스워드 한 레터씩 보기
-/</>/그 외의 경우를 각각 따로 처리하는 코드를 작성    
``` python
for pw in password: # 입력으로 받은 패스워드의 한 레터가
  if pw == "-": # - 이면
    if left: # left가 비어있지 않다면
      left.pop() # left의 가장 마지막 요소를 뱉어내라

  elif pw == "<": # < 이면
    if left: # left가 비어있지 않다면
      right.append(left.pop()) # right 맨 뒤에 left 맨 뒷 요소를 붙여라

  elif pw == ">": # > 이면
    if right: # right가 비어있지 않다면
      left.append(right.pop()) # left 맨 뒤에 right 맨 뒷 요소를 붙여라

  else: # 레터가 위 세 경우에 해당되지 않으면
    left.append(pw) # left에 해당 레터를 붙여라
```


<br>


--- 

<br>


## 결과 만들기
left 요소와 right의 요소를 거꾸로 만든 것을 합한 것       
``` python
left.extend(reversed(right))
print("".join(left))
```


<br>


--- 

<br>



## <span style="background-color:#fff5b1;">총정리</span>    
메모리 : 41392KB     
시간 : 1184ms   
``` python
test_case = int(input())

for _ in range(test_case):
    left = []
    right = []
    data = input()
    
    for i in data:
        if i == "-":
            if left:
                left.pop()
        elif i == ">":
            if right:
                left.append(right.pop())
        elif i == "<":
            if left:
                right.append(left.pop())
        else:
            left.append(i)
    left.extend(reversed(right))
    print("".join(left))
```

[키로거]: https://www.acmicpc.net/problem/5397