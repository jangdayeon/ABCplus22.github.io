---
layout: post
title: 4주차 활동일지_정다영
subtitle:
categories: Week_04
tags: #Dayoung
---
## 네 번째 활동 일지
**일시 :** 2022.11.02 16:00~18:30  
**작성자 :** 콘텐츠IT전공 20215238 정다영   
**학습 목표 :** 프렌드와 연산자 중복      

**주요학습내용**   
- 프렌드 함수   
- 프렌드 선언   
- 연산자 중복   
- 연산자 함수    

**오늘의 학습 계획**
1. Ch08_프렌드와 연산자 중복 수업자료 ppt 공부
2. 10주차 실습 문제 코딩  
3. 학습 평가
### 요약 정리

#### 프렌드 함수   
클래스의 멤버 함수가 아닌 외부함수

 - 프렌드 선언   
1. 전역 함수 : 클래스 외부에 선언된 전역 함수   
2. 다른 클래스의 멤버 함수   
3. 다른 클래스 전체(모든 멤버함수) - 프렌드 함수 개수에 제한x

#### 연산자 중복   
피 연산자에 따라 서로 다른 연산을 하도록 연산자를 중복 작성하는 것이다.  
자신이 정의한 클래스를 기본 타입처럼 다룰 수 있다.   

• C++에 본래 있는 연산자만 중복이 가능      
• 피 연산자 타입이 다른 새로운 연산을 정의한다.   
• 반드시 클래스와 관계를 가진다.   
• 피 연산자의 개수를 바꿀 수 없음.   
• 연산의 우선 순위 변경 안됨.   
• 모든 연산자가 중복 가능하지 않음.   
• 디폴트 매개변수 사용 불가.   
#### 연산자 함수   
1. 클래스의 멤버 함수로 구현하기
2. 외부 함수로 구현하고 클래스에 프렌드 함수로 선언

리턴타입 operator 연산자(매개변수리스트);
#### 연산자 구현

 - 이항연산자 + 중복(c = a + b)

```c++
//c = a. + (b); 
//a는 this->kick/this->punch에 들어감
//b가 매개변수 op2로 들어감
class Power {
  int kick;
  int punch;
public:
  Power operator+ (Power op2);
};
Power Power::operator+(Power op2) {
  Power tmp;
  tmp.kick = this->kick + op2.kick;
  tmp.punch = this->punch + op2.punch;
  return tmp;
}
  ```
 - == 연산자 중복(a == b)

```c++
//a. == (b)
//a는 this->kick/this->punch에 들어감
//b가 매개변수 op2로 들어감
class Power {
  int kick;
  int punch;
public:
  bool operator== (const Power& op2);
};
bool Power::operator==(const Power& op2) {
  if(kick==op2.kick && punch==op2.punch)
  return true;
  else
  return false;
}
  ```
  
### 학습 평가
프렌드 함수의 개념과 연산자 중복 개념을 통한 연산자 함수의 구현방법을 알아보고, 연산자를 작성해봄으로서 어떤식으로 함수 코드를 써야하는지에 대한 감을 익혀나갔다. 연산자 중복은 정수와 정수를 더하여 만들어질 수 있는 기본적인 +연산자를 정수 뿐만 아니라 문자열, 색, 배열 합치기 등으로 새로 만들어 구현할 수 있도록 해준다.
