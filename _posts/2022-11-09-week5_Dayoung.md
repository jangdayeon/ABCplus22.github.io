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
 ##### +=연산자 중복(c = a += b)  
 ->   c = a. += (b);      
 Power& operator+= (const Power& op2);

##### father = daughter; 
->   Person& operator= (const Person &rhs); 
    
    
#### 단항 연산자
피 연산자가 하나 뿐인 연산자
##### 단항 연산자 종류
1. 전위 연산자(prefix operator)
  - !op, ~op, ++op, --op
2. 후위 연산자(postfix operator)
  - op++, op--


##### 전위 ++ 연산자 중복 (++a)
1. a. ++ ( ); 
  - Power& operator++( );

2. ++(a); 
  - Power& operator++(Power& op);
##### 후위 ++ 연산자 중복(a++)
1. a. ++ (정수); 
  - Power operator++(int x);
2. ++(a, 0); 
  - Power operator++ (Power& op, int x);
  
  
#### 이동 대입 연산자
 
 ```c++
#include <iostream>
#include <utility> //swap()
using namespace std;
class Person {
  char *name;
  int id;
  public:
  Person& operator= (const Person &&person ) noexcept; //이동 대입 연산자
};
Person &Person::operator=(const Person &&person) noexcept {
  Person temp(person); 
  swap_person(*this, temp); 
  return *this;
}
void swap_person(Person &first, Person &second) noexcept {
  swap(first.id, second.id);
  swap(first.name, second.name);
}
  Person createObject() {
  return Person(10, "Hallym"); //rvalue(값) 반환
}
int main() {
  Person p1(1, "software");
  p1 = createObject(); //이동 대입 연산자 함수 호출
  p1.show();
  return 0;
}
  ```


  
### 학습 평가
 복사 대입 연산자를 구현해보고, 대입 연산자 구현 과정에서 복사 과정 중 예외가 발생하면 문제가 생기는 것에 대해 다시 코딩해 보았다. 대입 연산자 함수에서 받은 매개 변수를 참조로 받아 데이터를 복사하고 다시 리턴하게 되었을 때 발생하는 예외를 막기 위해 표준 라이브러리(<utility>) 에서 제공하는 유틸리티 swap() 함수를 사용하여 간단히 처리하였다.
##### 예외발생
 ```c++
class Person {
  ''''''''''''''''''
  Person& operator=(const Person &rhs); //대입(=)연산자 함수
};
Person& Person::operator= (const Person &rhs) {
  if (this == &rhs) //자기 자신을 대입
  return *this;
  
  delete name;
  name = nullptr;
  
  int len = strlen(rhs.name);
  name = new char[len + 1];
  //데이터 복사
  id = rhs.id;
  strcpy(name, rhs.name);
  return *this;
}//복사 과정 중 예외가 발생할 수 있다
  ```

##### swap() 함수 사용
 ```c++
class Person{
'''''''''''''''
Person &operator=(const Person &person);
//표준 라이브러리 알고리즘에서 활용할 수 있게 외부 함수로 swap_person() 추가
//단, 복사 과정에서 예외가 발생하지 않도록 한다. 
friend void swap_person(Person& first, Person& second) noexcept; 
};
  
Person &Person::operator=(const Person &person){
  '''''''''''''''''''
  Person temp(person); //임시 객체 생성
  swap_person(*this, temp); //현재 객체를 생성된 임시 복사본으로 교체
  return *this;
}
void swap_person(Person& first, Person& second) noexcept{
  swap(first.id, second.id);
  swap(first.name, second.name);
}
  ```
