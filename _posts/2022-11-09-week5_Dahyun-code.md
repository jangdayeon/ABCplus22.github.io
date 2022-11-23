---
layout: post
title: 5주차 실습코드_박다현
subtitle:
categories: Week_05
tags: #Dahyun
---
## 1번
```C++
#include <iostream>
#include <string>
using namespace std;

class Rect
{
    int width, height;

public:
    Rect(int width = 0, int height = 0) : width(width), height(height){};
    void show(string name)
    {
        cout << "object " << name << "] "
             << "width = " << width << ", height = " << height << endl;
    };
    friend Rect &operator++(Rect &op)
    {
        op.height++;
        op.width++;
        return op;
    };
    friend Rect operator++(Rect &op, int x)
    {
        Rect temp = op;
        op.height++;
        op.width++;
        return temp;
    };
    friend Rect operator+(int x, Rect &op)
    {
        Rect temp;
        temp.height = op.height + x;
        temp.width = op.width + x;
        return temp;
    }
};

int main()
{
    Rect a(5, 12), b(4, 5);
    cout << " ==== 증가 전 객체 멤버 변수 ==== " << endl;
    a.show("a");
    b.show("b");

    cout << " ==== 증가 후 객체 멤버변수 ==== " << endl;
    ++a;     // width와 height를 1 증가
    b = a++; // width와 height를 1 증가
    a.show("a");
    b.show("b");

    cout << " ==== 3 + a 연산 후 객체 멤버변수  ==== " << endl;
    b = 3 + a; // b의 width와 height 값을 a에 3을 더한 것으로 변경
    a.show("a");
    b.show("b");
}
```
## 2번
```C++
#include <iostream>
#include <string>
using namespace std;

class Point
{
    int x, y;

public:
    Point(int x, int y)
    {
        this->x = x;
        this->y = y;
    }
    int getX() { return x; }
    int getY() { return y; }

protected:
    void move_up(int x, int y)
    {
        this->x += x;
        this->y += y;
    }
    void move_down(int x, int y)
    {
        this->x -= x;
        this->y -= y;
    }
};

class ColorPoint : public Point
{
    string color;

public:
    ColorPoint() : Point(0, 0)
    {
        color = "BLACK";
        show();
    }

    ColorPoint(int x, int y, string color = "BLUE") : Point(x, y)
    {
        this->color = color;
    }

    void setPoint(int x, int y, char c)
    {
        if (c == '+')
        {
            move_up(x, y);
            show();
        }
        else
        {
            move_down(x, y);
            show();
        }
    }

    void setColor(string color)
    {
        this->color = color;
    }

    void show()
    {
        cout << color << "색으로 " << '(' << getX() << ',' << getY() << ')' << "에 위치한 점입니다." << endl;
    }
};

int main()
{
    cout << "zeroPoint 객체 출력" << endl;
    ColorPoint zeroPoint; // BLACK에 (0, 0) 위치의 점

    ColorPoint blue(5, 5);
    cout << endl
         << "blue 객체 출력" << endl;
    cout << "현재 위치에서 x:+10, y:+20 위치로 이동합니다" << endl;
    blue.setPoint(10, 20, '+');

    cout << endl
         << "red 객체 출력" << endl;
    ColorPoint red(50, 40, "RED");
    red.show();
    cout << "현재 위치에서 x:-10, y:-20 위치로 이동합니다" << endl;
    red.setPoint(10, 20, '-');
}
```
## 3번
```C++
#include <iostream>
#include <string>
using namespace std;

class Circle
{
    int radius;

public:
    Circle(int radius = 0) { this->radius = radius; }
    int getRadius() { return radius; }
    void setRadius(int radius) { this->radius = radius; }
    double getArea() { return 3.14 * radius * radius; };
};

class NamedCircle : public Circle
{
    string name;

public:
    NamedCircle(int radius = 0, string name = "");
    void show();
    void setName(string name)
    {
        this->name = name;
    }
    string getName()
    {
        return name;
    }
};

NamedCircle::NamedCircle(int radius, string name) : Circle(radius)
{
    this->name = name;
}
void NamedCircle::show()
{
    cout << "반지름이 " << getRadius() << "인 " << name << endl;
}

int main()
{
    NamedCircle c[5];
    int r;
    string n;

    cout << "5 개의 정수 반지름과 원의 이름을 입력하세요" << endl;
    for (int i = 0; i < 5; i++)
    {
        cout << i + 1 << ">> ";
        cin >> r >> n;
        c[i].setRadius(r);
        c[i].setName(n);
    }

    int max = 0;
    for (int i = 0; i < 5; i++)
    {
        if (c[i].getArea() > c[max].getArea())
            max = i;
    }
    cout << "가장 면적이 큰 피자는 " << c[max].getName() << "입니다" << endl;
}
```
## 4번
```C++
#include <iostream>
#include <string>
using namespace std;

class printer
{
    string model;        //모델
    string manufacturer; //제조사
    int printedCount;    //총 인쇄 매수
    int availableCount;  //인쇄 종이 잔량
public:
    printer(string m, string ma, int p, int a) : model(m), manufacturer(ma), printedCount(p), availableCount(a) {}
    string getModel() { return model; }
    string getManufacturer() { return manufacturer; }
    int getPrintedCount() { return printedCount; }
    int getAvailableCount() { return availableCount; }
    void setPrintedCount(int pages) { printedCount += pages; }
    void setAvailableCount(int pages) { availableCount += pages; }
    void minAvailableCount(int pages) { availableCount -= pages; }
};

class InkJetPrinter : public printer
{
    int availableInk; //잉크 잔량
public:
    InkJetPrinter(string m = "", string ma = "", int p = 0, int a = 0, int l = 0) : printer(m, ma, p, a)
    {
        this->availableInk = l;
    }
    int getAvailableInk() { return availableInk; }
    void printInkJet(int pages = 1)
    {
        setPrintedCount(pages);
        minAvailableCount(pages);
        availableInk -= pages;
    } //pages 수만큼 용지 사용, 잉크잔량은 pages 수만큼 감소
    void addAvailableCount(int pages)
    {
        setAvailableCount(pages);
    }
    void showStateInkJet()
    {
        cout << getModel() << " ," << getManufacturer() << " ,"
             << "인쇄 매수 " << getPrintedCount() << "장 ,"
             << "남은 종이 " << getAvailableCount() << "장 ,"
             << "남은 잉크 " << availableInk << endl;
    } //현재 상태 출력
};

class LaserPrinter : public printer
{
    int availableToner; //토너 잔량
public:
    LaserPrinter(string m = "", string ma = "", int p = 0, int a = 0, int t = 0) : printer(m, ma, p, a)
    {
        this->availableToner = t;
    }
    void printLaser(int pages = 1)
    {
        setPrintedCount(pages);
        minAvailableCount(pages);
        availableToner -= 1;
    } //pages 수만큼 용지 사용, 토너 잔량은 -1 감소
    void addAvailableCount(int pages)
    {
        setAvailableCount(pages);
    }
    void showStateLaser()
    {
        cout << getModel() << " ," << getManufacturer() << " ,"
             << "인쇄 매수 " << getPrintedCount() << "장 ,"
             << "남은 종이 " << getAvailableCount() << "장 ,"
             << "남은 토너 " << availableToner << endl;
    } //현재 상태 출력
};

class PrinterManager : public InkJetPrinter, LaserPrinter
{
    InkJetPrinter *Ink;
    LaserPrinter *Laser;

public:
    PrinterManager()
    {
        cout << "현재 작동중인 2대의 프린터는 아래와 같다" << endl;
        Ink = new InkJetPrinter("officejet V40", "HP", 0, 5, 10);
        Laser = new LaserPrinter("SCX-6x45", "삼성전자", 0, 6, 10);
        cout << "잉크젯 : ";
        Ink->showStateInkJet();
        cout << "레이저 : ";
        Laser->showStateLaser();
    }
    void operater()
    {
        char c = 'y';
        while (c == 'y')
        {
            int num, pages, add;
            cout << endl
                 << "프린터(1:잉크젯, 2:레이저)와 매수 입력 >> ";
            cin >> num >> pages;

            if (num == 1)
            {
                if (Ink->getAvailableCount() < pages)
                {
                    cout << "용지가 부족하여 프린트할 수 없습니다." << endl;
                    cout << "용지를 추가해 주세요 ";
                    cin >> add;
                    Ink->addAvailableCount(add);
                    cout << "용지를 " << add << " 추가 합니다" << endl;
                }
                Ink->printInkJet(pages);
                cout << "프린트하였습니다." << endl;
                Ink->showStateInkJet();
            }
            else if (num == 2)
            {
                if (Laser->getAvailableCount() < pages)
                {
                    cout << "용지가 부족하여 프린트할 수 없습니다." << endl;
                    cout << "용지를 추가해 주세요 ";
                    cin >> add;
                    Laser->addAvailableCount(add);
                    cout << "용지를 " << add << " 추가 합니다" << endl;
                }

                Laser->printLaser(pages);
                cout << "프린트하였습니다." << endl;
                Laser->showStateLaser();
            }
            while (true)
            {
                cout << "계속 프린트 하시겠습니까(y/n)>> ";
                cin >> c;
                if (!(c == 'y' || c == 'n'))
                {
                    cout << "다시 입력해주세요." << endl;
                    continue;
                }
                break;
            }
        }
    }
};
```
