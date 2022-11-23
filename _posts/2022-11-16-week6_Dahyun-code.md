---
layout: post
title: 6주차 실습코드_박다현
subtitle:
categories: Dahyun
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
#include <string>
using namespace std;

class Calculator
{
protected:
    int a, b;

public:
    Calculator(int a, int b) : a(a), b(b) {}
    virtual int calc() = 0;
    virtual void write()
    {
        cout << "a:" << a << "\tb:" << b << " =>";
    }
};
class Adder : public Calculator
{
public:
    Adder(int a, int b) : Calculator(a, b) {}
    int sum()
    {
        int sum = 0;
        for (int i = a; i <= b; i++)
            sum += i;

        return sum;
    }
    int calc()
    {
        return a + b;
    }
};
class Mul : public Calculator
{
public:
    Mul(int a, int b) : Calculator(a, b) {}
    int calc()
    {
        return a * b;
    }
};

class Manage
{
public:
    static void run()
    {
        int num, n1, n2;
        while (true)
        {
            cout << "선택하세요" << endl;
            cout << "1:add 2:multiply 3.finish >> ";
            cin >> num;
            if (num == 3)
                break;
            cout << "정수 2개를 입력하세요 >> ";
            cin >> n1 >> n2;
            if (num == 1)
            {
                Adder add(n1, n2);
                Calculator *cal = &add;
                cal->write();
                cout << cal->calc() << endl;
                cout << "sum : " << add.sum() << endl;
            }
            else if (num == 2)
            {
                Mul mul(n1, n2);
                Calculator *cal = &mul;
                cal->write();
                cout << cal->calc() << endl;
            }
        }
    }
};

int main()
{
    Manage::run();
}
```
## 2번
```C++
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

class AbstractGate
{
	bool x, y;

public:
	virtual bool operation(bool x, bool y) = 0;
};

class ANDGate : public AbstractGate
{
public:
	virtual bool operation(bool x, bool y)
	{
		if (x == false || y == false)
			return false;
		else
			return true;
	}
};
class ORGate : public AbstractGate
{
public:
	virtual bool operation(bool x, bool y)
	{
		if (x == true || y == true)
			return true;
		else
			return false;
	}
};
class XORGate : public AbstractGate
{
public:
	virtual bool operation(bool x, bool y)
	{
		if (x != y)
			return true;
		else
			return false;
	}
};
class Manage
{
public:
	static void go()
	{
		int num, n1, n2;
		while (true)
		{
			cout << "연산 종류를 선택하세요 1.and 2.or 3.xor 4.stop >> ";
			cin >> num;
			if (num == 4)
				break;
			cout << "게이트 입력 값 >> ";
			cin >> n1 >> n2;
			if (num == 1)
			{
				ANDGate andgate;
				AbstractGate *ab = &andgate;
				cout << "AND : " << boolalpha << n1 << "," << n2 << "=>" << ab->operation(n1, n2) << endl;
			}
			else if (num == 2)
			{
				ORGate orgate;
				AbstractGate *ab = &orgate;
				cout << "OR : " << boolalpha << n1 << "," << n2 << "=>" << ab->operation(n1, n2) << endl;
			}
			else if (num == 3)
			{
				XORGate xorgate;
				AbstractGate *ab = &xorgate;
				cout << "XOR : " << boolalpha << n1 << "," << n2 << "=>" << ab->operation(n1, n2) << endl;
			}
		}
	}
};
int main()
{
	Manage::go();
}
```
## 3번
```C++
#include <iostream>
#include <string>
using namespace std;

class Shape
{
protected:
    string name;       // 도형의 이름
    int width, height; // 도형이 내접하는 사각형
public:
    Shape(string n = "", int w = 0, int h = 0)
    {
        name = n;
        width = w;
        height = h;
    }
    virtual double getArea()
    {
        return 0;
    }
    string getName() { return name; } // 이름 리턴
};

class Oval : public Shape
{
public:
    Oval(string n, int w, int h) : Shape(n, w, h) {}
    double getArea()
    {
        return width * height * 3.14;
    }
    string getName()
    {
        return name;
    }
};

class Rect : public Shape
{
public:
    Rect(string n, int w, int h) : Shape(n, w, h) {}
    double getArea()
    {
        return width * height;
    }
    string getName()
    {
        return name;
    }
};

class Triangular : public Shape
{
public:
    Triangular(string n, int w, int h) : Shape(n, w, h) {}
    double getArea()
    {
        return (width * height) / 2;
    }
    string getName()
    {
        return name;
    }
};

int main()
{
    Shape *p[3];
    p[0] = new Oval("빈대떡", 10, 20);
    p[1] = new Rect("찰떡", 30, 40);
    p[2] = new Triangular("토스트", 30, 40);
    for (int i = 0; i < 3; i++)
        cout << p[i]->getName() << " 넓이는 " << p[i]->getArea() << endl;

    for (int i = 0; i < 3; i++)
        delete p[i];
}
```
## 4번
```C++
#include <iostream>
#include <string>
using namespace std;

class Converter
{
protected:
    double ratio;
    virtual double convert(double src) = 0; // src를 다른 단위로 변환한다.
    virtual string getSourceString() = 0;   // 소스 단위 명칭
    virtual string getDestString() = 0;     // dest 단위 명칭
public:
    Converter(double ratio) { this->ratio = ratio; }
    void run()
    {
        double src;
        cout << getSourceString() << "을 " << getDestString() << "로 바꿉니다. ";
        cout << getSourceString() << "을 입력하세요>> ";
        cin >> src;
        cout << "변환 결과 : " << convert(src) << getDestString() << endl;
    }
};
class KmToMile : public Converter
{
public:
    KmToMile(double ratio) : Converter(ratio) {}
    double convert(double src)
    {
        return src / ratio;
    }
    string getSourceString()
    {
        return "Km";
    }
    string getDestString()
    {
        return "Mile";
    }
};

class WonToDollar : public Converter
{
public:
    WonToDollar(int ratio) : Converter(ratio) {}
    double convert(double src)
    {
        return src / ratio;
    }
    string getSourceString()
    {
        return "원";
    }
    string getDestString()
    {
        return "달러";
    }
};

int main()
{
    KmToMile toMile(1.609344); // 1mile은 1.609344 Km
    WonToDollar wd(1010);      // 1 달러에 1010원
    Converter *cp = &toMile;
    cp->run();
    cp = &wd;
    cp->run();
}
```
## 5번
```C++
#include <iostream>
#include <string>
using namespace std;

class Tool
{
    string type;

public:
    Tool() = default;
    Tool(string type) : type(type) {}
    string getType()
    {
        return type;
    }
    virtual void write()
    {
        cout << "type >> " << type << endl;
    }

    virtual void cut() = 0; //자르다
    virtual void dry() = 0; //말리다
};

class Hair : public Tool
{
    string style;

public:
    Hair(string type, string style) : Tool(type)
    {
        this->style = style;
    }
    void tint(string color)
    {
        getType() = color;
        cout << "Hair(을)를 " << color << " 색으로 염색하다" << endl;
    }
    void cut()
    {
        cout << "Hair (을)를 자르다" << endl;
    }
    void dry()
    {
        cout << "Hair (을)를 말리다" << endl;
    }
    void write()
    {
        Tool::write();
        cout << "style >> " << style << endl;
    }
};

class Paper : public Tool
{
    string size;

public:
    Paper(string type, string size) : Tool(type)
    {
        this->size = size;
    }
    void draw()
    {
        cout << "크기가 " << size << " 인 종이에 그림을 그립니다" << endl;
    }
    void cut()
    {
        cout << "Paper (을)를 정해진 규격으로 자르다" << endl;
    }
    void dry()
    {
        cout << "Paper (을)를 건조한다" << endl;
    }
    void write()
    {
        Tool::write();
        cout << "size >> " << size << endl;
    }
};

void show(Tool *tool)
{
    tool->write();
    tool->cut();
    tool->dry();
}

int main()
{
    Hair h("Hair", "wave");
    Paper p("Paper", "A3");
    cout << "=== Hair 클래스 ===" << endl;
    show(&h);
    h.tint("red");
    cout << "=== Paper 클래스 ===" << endl;
    show(&p);
    p.draw();
    return 0;
}
```
