---
layout: post
title: 1주차 실습코드_박다현
subtitle:
categories: Dahyun
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
#include <iomanip>
#include <memory>
#include <cstdlib>
#include <ctime>
using namespace std;

int main()
{
    srand((unsigned int)time(NULL));
    int size;
    double ran;

    cout << "배열(double) 크기를 입력하세요 >> ";
    cin >> size;
    auto num = make_unique<double[]>(size);

    for (int i = 0; i < size; i++)
    {
        ran = (double)((rand() % 99) + 1) / 100;
        num[i] = ran;
        cout << i + 1 << ")" << setprecision(2) << num[i] << endl;
    }
}
```
## 2번
```C++
#include <iostream>
#include <string>
#include <string_view>
#include <cstdlib>
#include <ctime>
using namespace std;

string changeExt(string text)
{
    srand((unsigned int)time(NULL));
    int size = text.length();
    int n = rand() % size;
    int ran = rand() % 25 + 95;
    text[n] = (char)ran;
    return text;
}
int main()
{
    string text;
    char str[100];
    cout << "string 문자열을 입력하세요 >> ";
    getline(cin, text);
    cout << "change: " << changeExt(text) << endl;
    cout << "cstring 문자열을 입력하세요 >> ";
    cin >> str;
    cout << "change: " << changeExt(str) << endl;
}
```
## 3번
```C++
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string text;
    char c;
    int cnt = 0;

    cout << "문자열 입력>> ";
    getline(cin, text);
    cout << "검색하고자 하는 문자 입력>> ";
    cin >> c;

    if (text.find(c))
    {
        for (int i = 0; i < text.length(); i++)
        {
            if (text[i] == c)
                cnt++;
        }
        cout << "문자 " << c << "는 " << cnt << "개 있습니다.";
    }
}
```
## 4번
```C++
#include <iostream>
#include <memory>
using namespace std;

int main()
{
    int size;
    string name, text;

    cout << "끝말 잇기 게임을 시작합니다" << endl;
    cout << "게임에 참가하는 인원은 몇명입니까? >> ";
    cin >> size;
    auto game = make_unique<string[]>(size);

    for (int i = 0; i < size; i++)
    {
        cout << "참가자의 이름을 입력하세요. 빈칸 없이 >> ";
        cin >> name;
        game[i] = name;
    }

    int i = 0;
    cout << "시작하는 단어는 tree입니다" << endl;
    char end = 'e';

    while (true)
    {
        cout << game[i] << " >> ";
        cin >> text;
        int length = text.size();
        if (end == text[0])
        {
            end = text[length - 1];
            i++;
            if (i >= size)
                i = 0;
        }
        else
        {
            cout << game[i] << "이 졌습니다.";
            break;
        }
    }
}
```
## 5번
```C++
#include <iostream>
#include <string>
#include <memory>
using namespace std;

class Employee
{
    int year;
    string name;
    string dept;

public:
    void setEmployee(string name, string dept, int year);
    int getYear();
    string getName();
    string getDept();
    void disPlay();
    ~Employee();
};

void Employee::setEmployee(string n, string d, int y)
{
    name = n;
    dept = d;
    year = y;
}

int Employee::getYear()
{
    return year;
}

string Employee::getName()
{
    return name;
}

string Employee::getDept()
{
    return dept;
}

void Employee::disPlay()
{
    cout << "name : " << name << " dept : " << dept << " year : " << year << endl;
}

Employee::~Employee()
{
    cout << name << "객체 소멸" << endl;
}

class Manager
{
    unique_ptr<Employee[]> p;
    int size;

public:
    Manager(int size);
    ~Manager();
    void searchByName();
    void searchByYear();
};

Manager::Manager(int s)
{
    size = s;
    p = make_unique<Employee[]>(size);
    for (int i = 0; i < size; i++)
    {
        string n;
        string d;
        int y;
        cout << "사원 " << i + 1 << "의 이름과 소속, 입사연도를 입력하세요 >> ";
        cin >> n >> d >> y;
        p[i].setEmployee(n, d, y);
    }
}
Manager::~Manager()
{
    cout << "객체 소멸" << endl;
}

void Manager::searchByName()
{
    string name;
    cout << "검색하고자 하는 사원의 이름 >> ";
    cin >> name;
    for (int i = 0; i < size; i++)
    {
        if (p[i].getName() == name)
        {
            p[i].disPlay();
        }
    }
}

void Manager::searchByYear()
{
    int year;
    int cnt = 0;
    cout << "입사 연도를 입력하세요 >> ";
    cin >> year;

    cout << year << " 년도 이후에 입사한 사원을 검색합니다." << endl;
    for (int i = 0; i < size; i++)
    {
        if (p[i].getYear() > year)
        {
            p[i].disPlay();
            cnt++;
        }
    }
    cout << year << "연도 이후에 입사한 사원은 " << cnt << "명 입니다." << endl;
}

int main()
{
    Manager *pManager;
    cout << "사원수를 입력하세요 >> ";
    int size;
    cin >> size;
    if (size <= 0)
    {
        cout << "양수를 입력하세요." << endl;
        return 0;
    }
    pManager = new Manager(size);
    pManager->searchByName();
    pManager->searchByYear();

    delete pManager;
    return 0;
}
```
