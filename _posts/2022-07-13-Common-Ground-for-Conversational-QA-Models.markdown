---
layout: post
title:  "Common Ground for Conversational QA Models (ACL Workshop 2022)"
date:   2022-07-13 23:33:12 +0900
categories: NLP dialog
---
**Proceedings of the 4th Workshop on NLP for Conversational AI, ACL 2022** [[paper]] ⭐️⭐️⭐️   
**Authors** : Marco Del Tredici, Xiaoyu Shen, Gianni Barlacchi, Bill Byrne, Adrià de Gispert (Amazon Alexa AI)   

<br>   

## ✏️ **요약** 

* Question Rewriting 태스크를 수행하는 모델들의 한계는    
**<u>현재 턴(turns, utterances)을 처리할 때**    
**이전의 여러 턴으로부터 관련 있는 정보를 적절하게 가져오지 못한다</u>** 는 점이었음     
* 본 연구에서는 <span style="background-color:#fff5b1;">**Common Ground**</span>(CG, 대화가 진행됨에 따라 정보를 축적해나가는 접근법)라는   
  컨셉을 도입하여, 이전 턴으로부터 각 턴과 관련된 적절한 정보를 선택할 수 있도록 함     
* **CG**를 이용한 접근법은 이전의 접근법들에 비해   
  더 효율적(more effective)이고, 인간이 정보를 처리하는 접근법과 비슷한(human-like) 방식임     

<br>

---

<br>

# 1. Introduction 
대화에 참여하는 화자들은 대화의 목적을 달성하기 위해    
1) 새로운 정보를 연속적으로 공유하고    
2) 이 공유된 정보를 축적하는데,    
위와 같은 과정은 "effortless"함   

conversational QA task에서 대화를 처리하는 데 있어 핵심이 되는 부분은   
**이전 턴(들)에 등장한 정보에 기반하여 현재 턴을 처리하는 것** 인데,    
이러한 인간의 정보 처리 과정을 모델링하기 위해 다양한 접근법이 제안됨        
여러 방법 중 하나가 <span style="background-color:#fff5b1;">**Question Rewriting**</span>!!  

#### <span style="background-color:#fff5b1;">**Question Rewriting**</span>   
"rewriting the question in a **self-contained form** based on the previous conversational information"   
질문을 **대화 히스토리 없이 이해할 수 있는 self-contained한 형태로 다시 작성**해주는 태스크   

```
은지 : 미팅해본 적 있어?   
미미 : 아니, 나 미팅은 안 해봤어.    
영지 : 언니는 해봤어? 
```    

위 대화에서 맨 마지막 영지의 말인 ```언니는 해봤어?``` 를 따로 떼어 보면   
무엇을 해 보았냐는 말인지 알 수 없음     
즉, ```언니는 해봤어?``` 는 **대화의 문맥이 필요한 발화(context-dependent utterance)**인 것!   
QR는 context-dependent utterance를 **self-contained utterance**로 다시 작성해주는 태스크를 말함   

<div align="center"> 영지 : 언니는 해봤어? ➜ 언니는 <b><u>미팅</u></b> 해봤어? </div>  

하지만 대화가 진행될수록(길어질수록) 축적되는 정보의 양이 커지기 때문에, QR이 더욱 어려워짐      
➜ 이 연구에서는 QR 태스크를 수행하는 데 있어서, Clark(1996)에 착안하여 명제(propositions)의 집합을 **Common Ground**라고 두어 대화 내 정보 표현을 활용함    

<br>   

# 2. Data Construction for CG

CG를 대화 속 정보를 요약하는 명제의 집합으로 정의하였음
CG 정보가 라벨링된 데이터셋이 존재하지 않기 때문에, QR 데이터셋인 QReCC (Anantha et al., 2020)에 CG 정보를 어노테이션 하기로 함    

**STEP 1**



[paper]: https://aclanthology.org/2022.nlp4convai-1.7.pdf