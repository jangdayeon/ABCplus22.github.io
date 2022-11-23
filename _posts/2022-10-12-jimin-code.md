---
layout: post
title: 지민
subtitle:
categories: jimin
tags: #Jimin
---

## 객체 포인터 배열
```C++
#include <iostream>
using namespace std;

class Person {
    string name, tel;
    public : 
        Person(string n, string t) : name(n), tel(t) {};
        ~Person() { cout << "객체 소멸" << endl; }
        void disPlay() const { cout << "name = " << name << ", tel = " << tel << endl; }
};

int main() {
    Person *per[3];
    string name, tel;

    int size = sizeof(per) / sizeof(per[0]); // 3개의 객체 주소를 저장할 수 있는 객체 포인터 배열
    for(int i = 0; i < size; i++) {
        cout << ">> name, tel : ";
        cin >> name;
        cin >> tel;
        per[i] = new Person(name, tel);
    }
    for(int i = 0; i < size; i++) {
        per[i] -> disPlay(); // == (*(per + i)) -> disPlay();
    }
    for(int i = 0; i < size; i++) {
        delete per[i]; // n번 객체 생성, n번 객체 소멸
    }
}
```
