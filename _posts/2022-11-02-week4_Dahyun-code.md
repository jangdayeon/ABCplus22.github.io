---
layout: post
title: 4주차 실습코드_박다현
subtitle:
categories: Week_04
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
#include <string>
using namespace std;

class Book
{
    string title;
    int price, pages;

public:
    Book(string title = "", int price = 0, int pages = 0)
    {
        this->title = title;
        this->price = price;
        this->pages = pages;
    }
    void show() { cout << title << ' ' << price << "원 " << pages << "페이지" << endl; }
    string getTitle() { return title; } //title 반환
    Book &operator+=(int price);
    Book &operator-=(int price);
    bool operator==(int price);
    bool operator==(string title);
    bool operator==(const Book &b);
};

Book &Book::operator+=(int price)
{
    this->price += price;
    return *this;
}

Book &Book::operator-=(int price)
{
    this->price -= price;
    return *this;
}

bool Book::operator==(int price)
{
    if (this->price == price)
        return true;
    else
        return false;
}

bool Book::operator==(string title)
{
    if (this->title == title)
        return true;
    else
        return false;
}

bool Book::operator==(const Book &b)
{
    if (title == b.title && price == b.price && pages == b.pages)
        return true;
    else
        return false;
}

int main()
{
    Book a("청춘", 20000, 300), b("미래", 30000, 500);
    a += 500; // 책 a의 가격 500원 증가
    b -= 500; // 책 b의 가격 500원 감소
    a.show();
    b.show();

    Book b1("명품 C++", 30000, 500), b2("고품 C++", 30000, 500);
    if (b1 == 30000)
        cout << "정가 30000원" << endl; // price 비교
    if (b1 == "명품 C++")
        cout << "명품 C++ 입니다." << endl; // 책 title 비교
    if (b1 == b2)
        cout << "두 책이 같은 책입니다." << endl; // title, price, pages 모두 비교
}
```
## 2번
```C++
#include <iostream>
#include <string>
using namespace std;

class Matrix
{
    int ar[4];

public:
    Matrix(int a1 = 0, int a2 = 0, int b1 = 0, int b2 = 0)
    {
        ar[0] = a1;
        ar[1] = a2;
        ar[2] = b1;
        ar[3] = b2;
    }
    void show(string matrix)
    {
        cout << "=====" << matrix << "=====" << endl;
        for (int i = 0; i < 4; i++)
            cout << ar[i] << ' ';
        cout << endl;
    }
    Matrix operator+(const Matrix &m);
    Matrix &operator+=(const Matrix &m);
    Matrix &operator<<(int *ar);
    Matrix &operator>>(int *ar);
};

Matrix Matrix::operator+(const Matrix &m)
{
    Matrix tmp;
    for (int i = 0; i < 4; i++)
        tmp.ar[i] = ar[i] + m.ar[i];
    return tmp;
}

Matrix &Matrix::operator+=(const Matrix &m)
{
    for (int i = 0; i < 4; i++)
        ar[i] += m.ar[i];
    return *this;
}

Matrix &Matrix::operator>>(int *ar)
{
    for (int i = 0; i < 4; i++)
        this->ar[i] = ar[i];
    return *this;
}

Matrix &Matrix::operator<<(int *ar)
{
    for (int i = 0; i < 4; i++)
        this->ar[i] = ar[i];
    return *this;
}

int main()
{
    Matrix a(1, 2, 3, 4), b(2, 3, 4, 5), c;
    c = a + b;
    a += b;
    a.show("matrix a");
    b.show("matrix b");
    c.show("matrix c");

    int x[4], y[4] = {5, 6, 7, 8};
    a >> x; // a의 각 원소를 배열 x에 복사. x[]는 {4,3,2,1}
    b << y; // 배열 y의 원소 값을 b의 각 원소에 설정

    cout << ">> 배열 x의 원소 출력 << " << endl;
    for (int i = 0; i < 4; i++)
        cout << x[i] << ' '; // x[] 출력
    cout << endl;
    cout << ">> 배열 y값을 객체(b)에 복사 << " << endl;
    b.show("matrix b");
}
```
## 3번
```
#include <iostream>
#include <string>
using namespace std;

class Circle
{
    int radius;

public:
    Circle(int radius = 0)
    {
        this->radius = radius;
    };
    void show()
    {
        cout << "radius = " << radius << endl;
    };
    Circle &operator++();
    Circle operator++(int x);
    Circle operator+(int y);
};

Circle &Circle::operator++()
{
    radius++;
    return *this;
}

Circle Circle::operator++(int x)
{
    Circle tmp = *this;
    radius++;
    return tmp;
}

Circle Circle::operator+(int y)
{
    Circle tmp;
    tmp.radius = radius + y;
    return tmp;
}
int main()
{
    Circle a(5), b(4);
    cout << "Circle 객체 : a" << endl;
    a.show();
    cout << "Circle 객체 : b" << endl;
    b.show();
    ++a; // 반지름을 1 증가 시킨다.
    cout << "Circle 객체 : ++a" << endl;
    a.show();

    cout << "Circle 객체 : b=a++" << endl;
    b = a++; // 반지름을 1 증가 시킨다.
    cout << "Circle 객체 : a" << endl;
    a.show();
    cout << "Circle 객체 : b" << endl;
    b.show();

    b = a + 3; // b의 반지름을 a의 반지름에 1을 더한 것으로 변경
    cout << "Circle 객체 : b = a + 3" << endl;
    b.show();
}
 ```
## 4번
```C++
#include <iostream>
#include <string>
#include <utility>
using namespace std;

class Array
{
private:
    double *ptr;
    int size;

public:
    Array(int size)
    {
        ptr = new double[size];
    }; //size크기를 갖는 배열 동적 생성
    ~Array()
    {
        if (ptr)
            delete[] ptr;
    };
    void show()
    {
        for (int i = 0; i < size; i++)
        {
            cout << ptr[i] << "  ";
        }
    };
    auto &operator[](int index)
    {
        return ptr[index];
    }
    Array &operator=(const Array &op2)
    {
        Array tmp(op2);
        swap_array(*this, tmp);
        return *this;
    }
    void swap_array(Array &f, Array &s) noexcept
    {
        swap(f.ptr, s.ptr);
    }
};

int main()
{
    Array arr(5), brr(5);

    for (int i = 0; i < 5; i++)
    {
        cout << i + 1 << ") input>> ";
        cin >> arr[i];
    }

    cout << "==== Value of arr====" << endl;
    arr.show();

    brr = arr;
    brr[2] = 34.5;
    brr[4] = 56.3;
    cout << "==== Value of brr====" << endl;
    brr.show();

    cout << "==== Value of arr====" << endl;
    arr.show();

    return 0;
}
```
## 5번
```C++
#include <iostream>
#include <string>
using namespace std;

class SortedArray
{
    int size;    // 현재 배열의 크기
    int *p;      // 정수 배열에 대한 포인터
    void sort(); // 정수 배열을 오름차순으로 정렬
public:
    SortedArray();                  // p는 NULL로 size는 0으로 초기화
    SortedArray(SortedArray &src);  // 복사 생성자
    SortedArray(int p[], int size); // 생성자. 정수 배열과 크기를 전달받음
    ~SortedArray();                 // 소멸자
    SortedArray operator+(SortedArray &op2);
    SortedArray &operator=(const SortedArray &op2); // 현재 배열에 op2 배열을 복사
    void show();                                    // 배열의 원소 출력
};

void SortedArray::sort()
{
    int tmp;
    for (int i = 0; i < size; i++)
    {
        for (int j = 0; j < size - 1; j++)
        {
            if (p[j] > p[j + 1])
            {
                tmp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = tmp;
            }
        }
    }
}

SortedArray::SortedArray()
{
    p = NULL;
    size = 0;
}

SortedArray::SortedArray(SortedArray &src)
{
    size = src.size;
    p = new int[size];
    for (int i = 0; i < size; i++)
        p[i] = src.p[i];
}

SortedArray::SortedArray(int p[], int size)
{
    this->size = size;
    this->p = new int[size];
    for (int i = 0; i < size; i++)
        this->p[i] = p[i];
    sort();
}

SortedArray::~SortedArray()
{
    if (p)
        delete[] p;
}

SortedArray SortedArray::operator+(SortedArray &op2)
{
    SortedArray tmp;
    tmp.p = new int[size + op2.size];
    tmp.size = size + op2.size;
    int i;
    for (i = 0; i < size; i++)
    {
        tmp.p[i] = p[i];
    }
    int index = i;
    for (i = 0; i < op2.size; i++)
    {
        tmp.p[index] = op2.p[i];
        index++;
    }
    tmp.sort();
    return tmp;
}

SortedArray &SortedArray::operator=(const SortedArray &op2)
{
    size = op2.size;
    p = new int[size];
    for (int i = 0; i < size; i++)
        p[i] = op2.p[i];
    return *this;
}

void SortedArray::show()
{
    cout << "배열 출력 : ";
    for (int i = 0; i < size; i++)
        cout << p[i] << " ";
    cout << endl;
}

int main()
{
    int n[] = {2, 20, 6};
    int m[] = {10, 7, 8, 30};
    SortedArray a(n, 3), b(m, 4), c;

    c = a + b;
    a.show();
    b.show();
    c.show();
}
```
  
