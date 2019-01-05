1. 교재 418p : 문제 1번

```
#include <iostream>
#include <string>
using namespace std;

class Circle{
    int radius;
public:
    Circle(int radiu=0){ this->radius=radius;}
    int getRadius(){ return this->radius;}
    void setRadius(int radius){ this->radius=radius;}
    double getArea(){ return this->radius*3.14; }
};

// 써클 클래스를 상속 받은 NameCircle
class NameCircle:public Circle{ // public을 통하여 circle 접근 지정자를 유지한다.
    string name;
public:
    // circle의 함수를 이용 값을 지정하는 생성자
    NameCircle(int radius,string name){
        this->setRadius(radius);
        this->name=name;
    }
    
    // circle의 함수를 이용 값을 가지고 와 출력한다.
    void show(){
        cout<<"반지름이 "<<this->Circle::getRadius()<<"인 "<<this->name<<endl;
    }
    
    // 객체 값을 지정하는 함수
    void setNameCircle(int radius,string name){
        this->name=name;
        this->setRadius(radius);
    }
    
    // 이름값을 반환하는 함수
    string getName(){
        return this->name;
    }
    
};

int main(){
     NameCircle waffle(3,”waffle”);
waffle.show();
    return 0;
}

```
<br>
2. 교재 418p : 문제 2번

```
#include <iostream>
#include <string>
using namespace std;

class Circle{
    int radius;
public:
    Circle(int radiu=0){ this->radius=radius;}
    int getRadius(){ return this->radius;}
    void setRadius(int radius){ this->radius=radius;}
    double getArea(){ return this->radius*3.14; }
};

// 써클 클래스를 상속 받은 NameCircle
class NameCircle:public Circle{ // public을 통하여 circle 접근 지정자를 유지한다.
    string name;
public:
    // 배열 생성을 위한 기본 생성자
    NameCircle(){};
    // circle의 함수를 이용 값을 지정하는 생성자
    NameCircle(int radius,string name){
        this->setRadius(radius);
        this->name=name;
    }
    
    // circle의 함수를 이용 값을 가지고 와 출력한다.
    void show(){
        cout<<"반지름이 "<<this->Circle::getRadius()<<"인 "<<this->name<<endl;
    }
    
    // 객체 값을 지정하는 함수
    void setNameCircle(int radius,string name){
        this->name=name;
        this->setRadius(radius);
    }
    
    // 이름값을 반환하는 함수
    string getName(){
        return this->name;
    }
    
};

int main(){
    NameCircle pizza[5];
    NameCircle max;
    cout<<"5 개의 정수 반지름과 원의 이름을 입력하세요"<<endl;
    for(int i = 0; i < 5 ; i++ ){
        int radius;
        string name;
        cout<<i+1<<">>";
        cin>>radius;
        cin>>name;
        
        pizza[i].setNameCircle(radius, name);
        
        // 전 피자의 크기와 크기를 비교한다.
        if(i>0 && pizza[i].getArea() > pizza[i-1].getArea() ){// 첫번째 피자는 비교할 대상이 없으므로 제외
            max=pizza[i];
        }
        
    }

    cout<<"가장 면적이 큰 피자는 "<< max.getName() <<"입니다."<<endl;
    
    
    
    return 0;
}

```
<br>
3. 교재 419p : 문제 3번

```
#include <iostream>
#include <string>
using namespace std;

class Point{
    int x,y;
public:
    Point(int x, int y){ this->x=x; this->y=y;};
    int getX(){return this->x;}
    int getY(){return this->y;}
    
protected:
    void move(int x, int y){
        this->x=x; this->y=y;
    }
};

class ColorPoint:public Point{
    string color;
public:
    
    // 상속받은 생성자를 호출
    ColorPoint(int x, int y,string color="MANGGO"):Point(x,y){
        this->color=color;
    };
    
    
    void setPoint(int x, int y){
        move(x,y);
    };
    
    void setColor(string color){
        this->color=color;
    }
    void show(){
        cout<<this->color<<"색으로 ("<<getX()<<","<<getY()<<")에 위치한 점입니다."<<endl;
    }
    
};
int main(){
   
ColorPoint cp(5,5,"RED");
    ColorPoint cp(5,5);
    cp.setPoint(10, 20);
    cp.setColor("BLUE");
    cp.show();
};

```
<br>
4. 교재 419p : 문제 4번

```
#include <iostream>
#include <string>
using namespace std;

class Point{
    int x,y;
public:
    Point(int x, int y){ this->x=x; this->y=y;};
    int getX(){return this->x;}
    int getY(){return this->y;}
    
protected:
    void move(int x, int y){
        this->x=x; this->y=y;
    }
};

class ColorPoint:public Point{
    string color;
public:
    
    // 상속받은 생성자를 호출
    ColorPoint(int x, int y,string color="MANGGO"):Point(x,y){
        this->color=color;
    };
    // 포인트를 0으로 생성하는 기본 생성자
    ColorPoint():Point(0,0){
        this->color="BLACK";
    };
    
    void setPoint(int x, int y){
        move(x,y);
    };
    
    void setColor(string color){
        this->color=color;
    }
    void show(){
        cout<<this->color<<"색으로 ("<<getX()<<","<<getY()<<")에 위치한 점입니다."<<endl;
    }
    
};
int main(){
    ColorPoint zeroPoint;
    zeroPoint.show();
    
    //ColorPoint cp(5,5,"RED");
    ColorPoint cp(5,5);
    cp.setPoint(10, 20);
    cp.setColor("BLUE");
    cp.show();
};

```
<br>
5. 교재 420p : 문제 6번

```
[프로그램 소스]
 // 문제 6번
#include <iostream>
#include <string>
using namespace std;

class BaseArray{
    int capacity;
    int *mem;
protected:
    BaseArray(int capacity=100){
        this->capacity=capacity;
        this->mem=new int[capacity];
    }
    
    ~BaseArray(){
        delete [] mem;
    }
    
    void put(int index,int val){
        mem[index]=val;
    }
    
    int get(int index){
        return mem[index];
    }
    
    int getCapacity(){
        return capacity;
    }
};

class MyStack:public BaseArray{
    int index;
public:
    MyStack(int capacity=100):BaseArray(capacity){
        this->index=0;
    }
    int length(){
        return index;
    }
    
    // 값을 저장하고 인덱스 증가시킨다.
    void push(int val){
        put(index,val);
        index++;
    }
    
    // index 가 음수가 되지 않도록 한다.
    int pop(){
        if(index!=0){
            return get(--index);
        }else{
            return get(0);
        }
    }
    int Capacity(){
        return getCapacity();
    }
    
};


int main(){
    MyStack mStack(100);
    int n;
    cout<<"스택에 삽입할 5개의 정수를 입력하라 >>"<<endl;
    for(int i=0; i< 5 ; i++){
        cin>> n;
        mStack.push(n);
    }
    
    cout<<"스택용량:"<<mStack.Capacity()<<", 스택크기:" <<mStack.length() <<endl;
    cout<< "스택의 모든 원소를 팝하여 출력한다.>>";
    
    while (mStack.length() != 0) {
        cout<< mStack.pop() << ' ';
    }
    
    cout<< endl << "스택의 현재 크기 : " << mStack.length() <<endl;
    
    return 0;
}
```
<br>
6. 교재 422p : 문제 8번

```
[프로그램 소스]
/*
 프린터는 모델명 제조사 인쇄매수 인쇄종이 잔량나타내는 정보와
  print(int pages)를 갖는다.
 print를 호출 할 때 마다 인쇄종이 잔량은 int pages 줄어든다.
 
 잉크젯 프린터는 잉크 잔량과 printInkJet(int pages) 함수를 추가로 가진다.
 레이저 프린터는 토너 잔량과 printLaser(int pages) 함수를 추가로 가진다.
 
 각각 클래스의 함수 생성자 소멸자를 작성
 
 번호를 입력받아 어떤 프린터에서 몇페이지를 출력할지 결정하며
 
 메인 초기에는 프린터들의 정보를 출력하고
 
 프린트를 시도하고 물품이 부족할 경우 출력을 하지 않는다.
 
 이후 게속 프린트를 할 지를 문는다.
 
 */

#include <iostream>
#include <string>
using namespace std;

//프린터는 모델명 제조사 인쇄매수 인쇄종이 잔량나타내는 정보와
//print(int pages)를 갖는다.
//print를 호출 할 때 마다 인쇄종이 잔량은 int pages 줄어든다.
class Printer{
    string model,manufacture;
    int printedCount,availableCount;
    // printedCount는 사용되지 않는다.
public:
    Printer(string model,string manufacture,int availableCount){
        this->model=model;
        this->manufacture=manufacture;
        this->availableCount=availableCount;
    }
    
    void print(int pages){
            availableCount-=pages;
            cout<<"프린트 하였습니다."<<endl;

    }
    
    int getAvailableCount(){
        return availableCount;
    }
    
    void show(){
        cout<<model<<","<<manufacture<<", 남은 종이 "<<availableCount<<"장";
    }
};

// 잉크젯 프린터는 잉크 잔량과 printInkJet(int pages) 함수를 추가로 가진다.

class InkPrinter:public Printer{
    int availableInk;
public:
    InkPrinter(string model="Officejet v40",string manufacture="HP",int availableCount=5,int availableInk=10):Printer(model,manufacture,availableCount){
        this->availableInk=availableInk;
    }
    
    void printInkJet(int pages){
        if(pages>availableInk){
            cout<<"잉크가 부족해서 출력할 수 없습니다."<<endl;
        }else if(pages > getAvailableCount()){
            cout<<"용지가 부족해서 출력할 수 없습니다."<<endl;
        }else{
            print(pages);
            availableInk-=pages;
        }
    }
    void disp(){
        cout<<"잉크젯 :";
        show();
        cout<<",남은 잉크:"<<availableInk<<endl;
    }
};
// 레이저 프린터는 2장 1토너를 사용한다.
class LaserPrinter:public Printer{
    int availableToner;
    bool next=false;// 0.5 토너 사용을 표현하기 위한 변수
public:
    LaserPrinter(string model="SCX=6x45",string manufacture="삼성전자",int availableCount=3,int availableToner=20):Printer(model,manufacture,availableCount){
        this->availableToner=availableToner;
    }
    
    
    void printLaser(int pages){
        
        if(pages>availableToner){
            cout<<"토너가 부족해서 출력할 수 없습니다."<<endl;
        }else if(pages > getAvailableCount()){
            cout<<"용지가 부족해서 출력할 수 없습니다."<<endl;
        }else{
            print(pages);
            
            // 토너 사용량은 정수로 표시되며
            // 토너는 두장당 1이 사용된다.
            // 그래서
            // 이미 반을 사용하였고 이번에도 반을 사용하여야 하는 상황이라면
            // 토너 사용가능량에서 1을 더 빼준다.
            if(next && pages%2!=0){
                availableToner-=(pages/2+1);
                next=false;
            }else{
                availableToner-=(pages/2);
            }
        }
    }
    
    void disp(){
        cout<<"레이저 :";
        show();
        cout<<",남은토너:"<<availableToner<<endl;
    }
};


int main(){
    InkPrinter hp;
    LaserPrinter samsung;
    
    cout<<"현재 작동중인 2대의 프린터는 아래와 같다."<<endl;
    hp.disp();
    samsung.disp();
    bool flag=true,flag2=true;; // 무한 반복문 탈출을 위한 불린 변수
    int printer,pages;// 메뉴 선택을 위한 변수
    
    while(flag){
        flag2=true;
        
        cout<<endl;
        while (flag2) {
            
            cout<<"프린터(1: 잉크젯, 2:레이저)와 매수 입력>>";
            cin>>printer;
            cin>>pages;
            
            switch (printer) {
                case 1:
                    hp.printInkJet(pages);
                    flag2=false;
                    break;
                case 2:
                    samsung.printLaser(pages);
                    flag2=false;
                    break;
                    
                    
                default:
                    cout<<"잘 못 입력하셧습니다."<<endl;
                    break;
            }
        }
     
        
        cout<<endl;
        hp.disp();
        samsung.disp();
        cout<<endl;
        
        // 잘못 입력했을 경우에도 위 과정을 다시 거치지 않기 위한 과정
        while(true){
            cout<<"계속 프린트 하시겠습니까?(n/y)"<<endl;
            char choose;
            cin>>choose;
            if(choose=='y'||choose=='Y'){
                break;
            }else if(choose=='n'||choose=='N'){
                flag=false;
                break;
            }else{
                cout<<"잘 못 입력하셧습니다."<<endl;
            }
            cin.ignore();
        }

    }
    
    return 0;
}

```

