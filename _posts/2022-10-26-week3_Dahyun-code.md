---
layout: post
title: 3주차 실습코드_박다현
subtitle:
categories: Dahyun
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
#include <cstring>
#include <vector>
using namespace std;

class Book
{
	char *title;
	int price;

public:
	Book(const char *title, int price);
	Book(const Book &b);
	~Book();
	Book(Book &&b) noexcept;
	void set(const char *title, int price);
	void show() { cout << title << ' ' << price << "원" << endl; }
};

Book::Book(const char *title, int price)
{
	int len = strlen(title);
	this->title = new char[len + 1];
	strcpy(this->title, title);
	this->price = price;
}

Book::Book(const Book &b)
{ //(3)
	int len = strlen(b.title);
	title = new char[len + 1];
	strcpy(title, b.title);
	price = b.price;
}

Book::~Book()
{
	if (title)
		delete[] title;
}

/*
Book::Book(Book& b) { //(2)
	title = b.title;
	price = b.price;
}
*/

Book::Book(Book &&b) noexcept //(4)
{
	title = b.title;
	price = b.price;
	b.title = nullptr;
	b.price = 0;
}

void Book::set(const char *title, int price)
{ //(1)
	if (this->title)
		delete[] this->title;
	int len = strlen(title);
	this->title = new char[len + 1];
	strcpy(this->title, title);
	this->price = price;
}

int main()
{
	Book cpp("명품C++", 10000);
	Book java = cpp; //book java(cpp)
	java.set("명품자바", 12000);
	cpp.show();
	java.show();

	vector<Book> b;
	b.push_back(Book("명품파이썬", 300));
	b.at(0).show();
	Book book(Book{"명품스크립트", 34000});
	book.show();
}
```
## 2번
```C++
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

class MyClass
{
    int size;
    int *element;

public:
    MyClass(int size);
    MyClass(const MyClass &my);
    MyClass(MyClass &&my) noexcept;
    ~MyClass();
    void change(int index, int value);
    void write(string &&message);
};

MyClass::MyClass(int size) : size(size), element(new int[size])
{
    for (auto i = 0; i < size; i++)
    {
        element[i] = 0;
    }
}

MyClass::MyClass(const MyClass &my)
{
    size = my.size;
    element = new int[size];
    for (auto i = 0; i < size; i++)
    {
        element[i] = my.element[i];
    }
}

MyClass::MyClass(MyClass &&my) noexcept
{
    size = my.size;
    element = my.element;
    my.size = 0;
    my.element = nullptr;
}

MyClass::~MyClass()
{
    if (!element)
        delete[] element;
}

void MyClass::change(int index, int value)
{
    element[index] = value;
}

void print(MyClass &&my, string &&message)
{
    move(my).write(move(message));
}

void MyClass::write(string &&message)
{
    cout << "==== " << message << " ====" << endl;
    for (int i = 0; i < size; i++)
    {
        cout << "  " << element[i];
    }
    cout << endl;
}

int main()
{
    MyClass my{5};
    my.write("original(my)");
    my.change(2, 30);
    my.change(4, 15);
    my.write("change(my)");
    MyClass copy(my);
    copy.write("copy after");
    my.write("original(my)");
    copy.change(1, 23);
    copy.change(4, 61);
    print(move(copy), "change(copy)");
}
```
## 3번
```C++
#include <iostream>
#include <string>
using namespace std;

class Dept
{
    int size;
    int *scores;

public:
    Dept(int size);
    Dept(const Dept &dept);
    ~Dept();
    int getSize();
    void read();
    bool isOver60(int index);
};

Dept::Dept(int size) : size(size), scores(new int[size])
{
    for (auto i = 0; i < size; i++)
    {
        scores[i] = 0;
    }
}

Dept::Dept(const Dept &dept)
{
    size = dept.size;
    scores = new int[size];
    for (auto i = 0; i < size; i++)
    {
        scores[i] = dept.scores[i];
    }
}

Dept::~Dept()
{
    if (scores)
        delete[] scores;
}

int Dept::getSize()
{
    return size;
}

void Dept::read()
{
    cout << size << "개 점수 입력 >> " << endl;
    for (auto i = 0; i < size; i++)
    {
        cout << i + 1 << ") ";
        cin >> scores[i];
    }
}

bool Dept::isOver60(int index)
{
    if (scores[index] > 60)
    {
        return true;
    }
    return false;
}

int countPass(Dept com)
{
    int count = 0;
    for (auto i = 0; i < com.getSize(); i++)
    {
        if (com.isOver60(i))
            count++;
    }
    return count;
}
int main()
{
    Dept *com;
    int cnt;
    cout << "학생 수를 입력하세요 >> ";
    cin >> cnt;
    com = new Dept(cnt);
    com->read();
    int n = countPass(*com);
    cout << "60점 이상은 " << n << "명" << endl;
    delete com;
}
```
## 4번
```C++
#include <iostream>
#include <string>
using namespace std;

class MyIntStack
{
    char *p;
    int size;
    int tos;

public:
    MyIntStack();
    MyIntStack(int size);
    MyIntStack(const MyIntStack &s);
    ~MyIntStack();

    bool push(char n);
    bool pop(char &n);
    void show();
};

MyIntStack::MyIntStack(int size) : size(size), p(new char[size]), tos(-1)
{
    for (auto i = 0; i < size; i++)
    {
        p[i] = 0;
    }
}

MyIntStack::MyIntStack(const MyIntStack &s)
{
    size = s.size;
    p = new char[size];
    for (auto i = 0; i < size; i++)
    {
        p[i] = s.p[i];
    }
}

MyIntStack::~MyIntStack()
{
    if (p)
        delete[] p;
}

bool MyIntStack::push(char n)
{
    if (tos == size - 1)
        return false;
    p[++tos] = n;
    return true;
}

bool MyIntStack::pop(char &n)
{
    if (tos == -1)
        return false;
    n = p[tos--];
    return true;
}

void MyIntStack::show()
{
    for (auto i = 0; i < size; i++)
    {
        if (p[i] == 0)
            break;
        cout << p[i] << " ";
    }
    cout << endl;
}

int main()
{
    MyIntStack a(20);
    a.push('a');
    a.push('f');
    a.push('k');

    cout << "== 스택(a) ==" << endl;
    a.show();

    MyIntStack b = a;
    cout << endl
         << "== 스택(b) ==" << endl;
    b.push('q');
    b.show();

    char n;
    a.pop(n);
    cout << endl
         << "스택 a에서 팝한 값 " << n << endl;
    b.pop(n);
    cout << "스택 b에서 팝한 값 " << n << endl
         << endl;
}
```
