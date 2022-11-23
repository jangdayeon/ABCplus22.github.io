---
layout: post
title: 2주차 실습코드_박다현
subtitle:
categories: Week_02
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
using namespace std;

char &find2replace(char fstr[], char re, bool &success)
{
    int i = 0;
    while (fstr[i])
    {
        if (fstr[i] == re)
        {
            success = true; //발견함. 함수 성공
            return fstr[i];
        }
        i++;
    }
    return fstr[0]; //발견하지 못함, return 값 의미 없음
}

int main()
{
    char str[] = "C++ programming";
    char has = '+';
    char replace = 'p';
    bool result = false;

    cout << "변경 전 문자열 = " << str << endl;

    find2replace(str, has, result) = replace; //'+' 위치에  'p' 저장

    if (result == true)
        cout << "변경 후 문자열 = " << str << endl;
    else
        cout << str << "에서 " << has << "를 발견하지 못함." << endl;
    return 0;
}
```
## 2번
```C++
#include <iostream>
using namespace std;

void find2replace(string &s, string &h, string &r, bool &re)
{
    int i = 0;
    while (s[i])
    {
        if (s.at(i) == h.at(0))
        {
            re = true;
            s.replace(i, 1, r);
        }
        i++;
    }
}

int main()
{
    std::string str = "C++ programming";
    std::string has = "+";
    string replace = "p";
    bool result = false;

    cout << "변경 전 문자열 = " << str << endl;

    find2replace(str, has, replace, result);

    if (result == true)
        cout << "변경 후 문자열 = " << str << endl;
    else
        cout << str << "에서 " << has << "를 발견하지 못함." << endl;
    return 0;
}
```
## 3번
```C++
#include <iostream>
using namespace std;

class Accumulator
{
    int value;

public:
    Accumulator(int val) : value{val} {};
    Accumulator &add(int n); //this
    int get() { return value; }
};

Accumulator &Accumulator::add(int n)
{
    value += n;
    return *this;
}

int main()
{
    Accumulator acc(10);
    cout << acc.get() << endl;

    acc.add(1).add(2).add(3);
    cout << acc.get() << endl;
}
```
## 4번
```C++
#include <iostream>
using namespace std;

class Fraction
{
    int numer;
    int denom;

public:
    Fraction(int num, int den);
    Fraction(){};
    ~Fraction(){};

    int getNumer() const { return numer; };
    int getDenom() const { return denom; };

    void setNumer(int num) { numer = num; };
    void setDenom(int den) { denom = den; };
    void print() const { cout << numer << "/" << denom << endl; };

private:
    void normalize();
    int gcd(int n, int m);
};

Fraction::Fraction(int num, int den)
{
    numer = num;
    denom = den;
    normalize();
}

void Fraction::normalize()
{
    int g = gcd(numer, denom);
    numer /= g;
    denom /= g;
}

int Fraction::gcd(int n, int m)
{
    int g;
    for (int i = 1; i <= n && i <= m; i++)
    {
        if (n % i == 0 && m % i == 0)
        {
            g = i;
        }
    }
    return g;
}

Fraction &larger(Fraction &a, Fraction &b)
{
    if (a.getNumer() * b.getDenom() > b.getNumer() * a.getDenom())
    {
        return a;
    }
    return b;
}

Fraction &largest(Fraction &a, Fraction &b, Fraction &c)
{
    return larger(larger(a, b), c);
}

Fraction *mul(Fraction &a, Fraction &b)
{
    Fraction *f = new Fraction((a.getNumer() * b.getNumer()), (a.getDenom() * b.getDenom()));
    return f;
}

Fraction *add(Fraction &a, Fraction &b)
{
    Fraction *f = new Fraction(((a.getNumer() * b.getDenom()) + (a.getDenom() * b.getNumer())), (a.getDenom() * b.getDenom()));
    return f;
}

int main()
{
    cout << "다음과 같은 분수에서 가장 큰 분수를 찾습니다" << endl;

    Fraction fract1(12, 15);
    cout << "fract1: ";
    fract1.print();

    Fraction fract2(6, 9);
    cout << "fract2: ";
    fract2.print();

    Fraction fract3(4, 11);
    cout << "fract3: ";
    fract3.print();

    cout << "가장 큰 분수: ";
    largest(fract1, fract2, fract3).print();

    cout << "다음과 같은 분수에 대하여 곱셈과 덧셈 연산을 합니다" << endl;

    Fraction fract4(2, 12);
    cout << "fract4: ";
    fract4.print();
    Fraction fract5(15, 25);
    cout << "fract5: ";
    fract5.print();

    Fraction *p;

    cout << "The result of multiplying is: ";
    p = mul(fract4, fract5);
    p->print();
    delete p;

    cout << "The result of adding is: ";
    p = add(fract4, fract5);
    p->print();
    delete p;

    Fraction product;
}
```
## 5번
```C++
#include <iostream>
using namespace std;

class Coffee
{
    string name;
    int price;

public:
    Coffee() = default;
    ~Coffee();
    void setName(string n);
    string getName();
    void setPrice(int p);
    int getPrice();
};

Coffee::~Coffee()
{
    cout << "소멸자 실행되었습니다." << endl;
}

void Coffee::setName(string n)
{
    name = n;
}

string Coffee::getName()
{
    return name;
}

void Coffee::setPrice(int p)
{
    price = p;
}

int Coffee::getPrice()
{
    return price;
}

int write(Coffee *b, int size)
{
    int total = 0;
    for (int i = 0; i < size; i++)
    {
        cout << " " << (b + i)->getName() << "," << (b + i)->getPrice() << endl;
        total += (b + i)->getPrice();
    }
    return total;
}

class CoffeeMachine
{
    Coffee *orderlist;
    int count;

public:
    CoffeeMachine()
    {
        string name[5] = {"moca", "latte", "americano", "espresso", "sugarcoffee"};
        int price[5] = {2000, 3000, 2000, 2500, 1500};
        cout << "=== 메뉴 ===" << endl;
        for (int i = 0; i < 5; i++)
        {
            cout << " " << i << ")" << name[i] << "," << price[i] << endl;
        }
        cout << endl
             << "몇 잔을 주문하시겠습니까?";
        cin >> count;
        orderlist = new Coffee[count];
        for (int i = 0; i < count; i++)
        {
            int index = -1;
            while (index < 0 || index > 4)
            {
                cout << "구매하실 메뉴 번호를 입력하세요 : ";
                cin >> index;
            }
            orderlist[i].setName(name[index]);
            orderlist[i].setPrice(price[index]);
        }
    }
    ~CoffeeMachine()
    {
        delete[] orderlist;
    }

    void result()
    {
        cout << endl
             << "주문하신 메뉴는" << endl;
        int total = write(orderlist, count);
        cout << "합계 금액은" << total << "원 입니다.";
        cout << endl
             << endl;
    }
};

int main()
{
    CoffeeMachine cm;
    cm.result();
    return 0;
}
```
