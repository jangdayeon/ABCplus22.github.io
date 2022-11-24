---
layout: post
title: 5주차 활동일지_정다영
subtitle:
categories: Week_05
tags: #Dayoung
---
## 다섯 번째 활동 일지
**일시 :** 2022.11.02 16:00~18:30  
**작성자 :** 콘텐츠IT전공 20215238 정다영   
**학습 목표 :** 프렌드와 연산자 중복    

**주요학습내용**    
- 복사 대입 연산자2   
- 이동 대입 연산자   
- 프렌드를 이용한 연산자 중복
**오늘의 학습 계획**
1. Ch08_프렌드와 연산자 중복 수업자료 ppt 공부
2. 11주차 실습 문제 코딩  
3. 학습 평가   
### 요약 정리

#### 연산자 구현
 - +=연산자 중복(c = a += b)
 
 ```c++
//c = a. += (b)
//a는 this->kick/this->punch에 들어감
//b가 매개변수 op2로 들어감
class Power {
  int kick;
  int punch;
public:
  Power& operator+=(const Power& op2);
};
Power& Power::operator+=(const Power& op2) {
  kick = kick + op2.kick;
  punch = punch + op2.punch;
  return *this; //자신의 참조 리턴
}
  ```
#### 이동 대입 연산자


  
### 학습 평가
 복사 대입 연산자를 구현해보고, 대입 연산자에서 
