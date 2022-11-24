---
layout: post
title: 6주차 활동일지_정다영
subtitle:
categories: Week_06
tags: #Dayoung
---
## 여섯 번째 활동 일지
**일시 :** 2022.11.16 16:00~18:30  
**작성자 :** 콘텐츠IT전공 20215238 정다영   
**학습 목표 :** 상속    

**주요학습내용**
- 상속 개념
- 클래스상속과 객체
- 접근 지정자
- 상속과 생성자, 소멸자
- 상속의 종류
- 다중 상속

**오늘의 학습 계획**
1. Ch08_상속 수업자료 ppt 공부
2. 12주차 실습 문제 코딩  
3. 학습 평가
### 요약 정리

#### 상속이란?
객체가 생성될 때 자신의 멤버 뿐 아니라 부모 클래스의 멤버를 포함할 것을 지시하여 기본 클래스의 속성과 기능을 파생 클래스에 물려주는 것     

 - 기본 클래스(base class, superclass) : 상속 해 주는 클래스. 부모 클래스    
 - 파생 클래스(derived class, subclass) : 상속 받는 클래스. 자식 클래스   

• 여러 개의 클래스를 동시에 상속 받는 다중 상속 허용   

##### 상속의 선언   

 ```c++
class Student : public Person { // Person을 상속받는 Student 선언
// Person 클래스의 멤버를 물려 받음
//기본 클래스명 : Person
//파생 클래스명: Student
//상속 접근 지정 – private, protected 도 가능
.....
};
class StudentWorker : public Student {// Student를 상속받는 StudentWorker 선언
// Student가 물려받은 Person의 멤버도 함께 물려받음
.....
};
  ```
  
#### 업 캐스팅(up-casting) : 기본 클래스의 포인터 = 파생 클래스의 포인터;     
#### 다운 캐스팅(down-casting) : 파생 클래스의 포인터 = 기본 클래스의 포인터;

#### 접근 지정자    
1. private 멤버
• 선언된 클래스 내에서만 접근 가능   
• 파생 클래스에서도 기본 클래스의 private 멤버에는 직접 접근 불가   

2. public 멤버
• 선언된 클래스나 외부 어떤 클래스, 모든 외부 함수에 접근 허용   
• 파생 클래스에서 기본 클래스의 public 멤버 접근 가능   

3. protected 멤버   
• 선언된 클래스에서 접근 가능   
• 파생 클래스에서만 접근 허용   
• 파생 클래스가 아닌 다른 클래스나 외부 함수에서는 protected 멤버를 접근할 수 없다.   



#### 상속과 생성자, 소멸자
##### 생성자 실행 순서
 - 파생 클래스의 객체가 생성될 때 파생 클래스의 생성자와 기본 클래스의 생성자 모두 실행됨.   
 - 생성자는 기본 클래스의 생성자가 먼저 실행된 후 파생 클래스의 생성자가 실행됨.   

##### 소멸자 실행 순서
 - 파생 클래스의 객체가 소멸될 때 파생 클래스의 소멸자가 먼저 실행되고, 기본 클래스의 소멸자가 나중에 실행 됨.   

#### 상속의 종류
 - public으로 선언 : 기본 클래스의 protected, public 멤버 속성을 그대로 계승   
 - protected으로 선언 : 기본 클래스의 protected, public 멤버를 protected로 계승   
 - private으로 선언 : 기본 클래스의 protected, public 멤버를 private으로 계승   

#### 다중 상속
##### 다중 상속 선언 및 활용
 ```c++
class MP3 {
public:
  void play();
  void stop();
};
class MobilePhone {
public:
  bool sendCall();
  bool receiveCall();
  bool sendSMS();
  bool receiveSMS();
};
// 다중 상속 선언
class MusicPhone : public MP3, public MobilePhone { 
public:
  void dial();
};

void MusicPhone::dial() {
  play(); //MP3::play() 호출
  sendCall(); //MobilePhone::sendCall() 호출
}

int main() {
  MusicPhone hanPhone;
  hanPhone.play(); //MP3의 멤버 play() 호출
  hanPhone.sendSMS(); //MobilePhone의 멤버 sendSMS() 호출
}
  ```

### 학습 평가
C++ 상속의 개념을 배우고, 상속을 통해 간결한 클래스를 작성해보면서 객체 지향적 설계를 하기 위한 기반을 다졌다.
상속을 사용해보니 클래스를 분류하고 관리하기 용이하여 클래스들의 구조적 관계 파악이 잘 될 것 같다고 생각했다.
상속은 다중 상속이 가능한데, 여기서 다중 상속으로 인해 기본 클래스의 멤버와 파생 클래스의 멤버가 이중으로 객체에 삽입되는 문제점을 발견했다.
이를 해결하는 방법은 가상 상속을 통해 기본 클래스 멤버의 중복 상속을 해결할 수 있다.

 - 가상 상속 구현 방법
• 파생 클래스의 선언문에서 기본 클래스 앞에 virtual로 선언한다   
• 파생 클래스의 객체가 생성될 때 기본 클래스의 멤버는 오직 한 번만 생성   
 ```c++
class In : virtual public BaseIO {
//In 클래스는 BaseIO 클래스를 가상 상속함
... 
};
class Out : virtual public BaseIO {
// Out 클래스는 BaseIO 클래스를 가상 상속함
... 
}; 
  ```
