1. 교재 466p : 문제 4번

```
	class LoopAdder{
    string name; // 루프의 이름
    int x,y,sum; // x에서y까지의 합 sum
    void read(); // x,y를 읽어 들이는 함수
    void write(); // sum을 출력하는 함수
protected:
    LoopAdder(string name=""){
        this->name=name;
    }
    int getX(){ return x;}
    int getY(){ return y;}
    virtual int calculate()=0; // 순수 가상 함수. 루프를 돌며 합을 구하는 함수
public:
    void run();// 연산을 진행하는 함수
    
};

void LoopAdder::read(){
    cout<<name<<":"<<endl;
    cout<<"처음 수에서 두번째 수까지 더합니다. 두 수를 입력하세요 >>";
    cin >> x >> y;
}

void LoopAdder::write(){
    cout<<x<<"에서 "<<y<<"까지의 합 =" << sum << "입니다." <<endl;
}

void LoopAdder::run(){
    read();
    sum = calculate();
    write();
}


class WhileLoopAdder:public LoopAdder{
public:
    WhileLoopAdder(string name="While Loop"):LoopAdder(name){
    }
    int calculate(){
        int x=getX();
        int y=getY();
        int sum=0;
        
        while(x<=y){
            sum+=x;
            x++;
        }
        return sum;
    }
};


class DoWhileLoopAdder:public LoopAdder{
public:
    DoWhileLoopAdder(string name="While Loop"):LoopAdder(name){
    }
    int calculate(){
        int x=getX();
        int y=getY();
        int sum=0;
        
        do{
            sum+=x;
            x++;
        }while(x<=y);
        return sum;
    }
};

int main() {
    WhileLoopAdder whileLoop=WhileLoopAdder("While Loop");
    DoWhileLoopAdder dowhileLoop("Do while Loop");
    
    whileLoop.run();
    dowhileLoop.run();
    
    return 0;
}

```
<br>
2.교재 467p : 문제 5번

```
// 문제 5번
#include <iostream>
#include <string>
using namespace std;

class AbstractGate{
protected:
    bool x,y;
public:
    void set(bool x,bool y){this-> x= x; this->y=y;}
    virtual bool operation()=0;
    
};

class ANDGate:public AbstractGate{
public:
    bool operation(){
        return x==y==true;
    }
};

class ORGate:public AbstractGate{
public:
    bool operation(){
        return x==true||y==true;
    }
};

class XORGate:public AbstractGate{
public:
    bool operation(){
        return x!=true||y!=true;
    }
};


int main(){
    ANDGate andGate;
    ORGate orGate;
    XORGate xorGate;
    
    andGate.set(true, false);
    orGate.set(true, false);
    xorGate.set(true, false);
    
    cout<< andGate.operation() << endl;
    cout<< orGate.operation() << endl;
    cout<< xorGate.operation() << endl;
    return 0;
}


#include <iostream>
#include <string>
using namespace std;

```

<br>
3. 교재 469p : 문제 7번

```
 // 문제 7번
#include <iostream>
#include <string>
using namespace std;

class Shape{
protected:
    string name;
    int width,hegiht;
public:
    Shape(string n="",int w=0,int h=0){
        this->name=n;
        this->width=w;
        this->hegiht=h;
    }
    virtual double getArea(){return 0;} // 더미 값을 리턴
    string getName(){return name;}
};

class Oval:public Shape{
public:
    Oval(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht*3.14;
    }
    
};


class Rect:public Shape{
public:
    Rect(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht;
    }
    
};

class Triangular:public Shape{
public:
    Triangular(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht*1/2;
    }
    
};

int main(){
    Shape *p[3];
    p[0]= new Oval("빈대떡",10,20);
    p[1]= new Rect("찰떡",30,40);
    p[2]= new Triangular("토스트",30,40);
    
    for(int i=0; i < 3 ; i++){
        cout<< p[i]->getName() << " 넓이는 " << p[i]->getArea() << endl;
    }
    
    for(int i=0; i < 3 ; i++){
        delete p[i];
    }
    return 0;
}

```

<br>
4. 교재 469p : 문제 8번

```
[프로그램 소스] 
// 문제 8번
#include <iostream>
#include <string>
using namespace std;

class Shape{
protected:
    string name;
    int width,hegiht;
public:
    Shape(string n="",int w=0,int h=0){
        this->name=n;
        this->width=w;
        this->hegiht=h;
    }
    virtual double getArea()=0;
    string getName(){return name;}
    virtual ~Shape(){}; // 소멸자 가상함수로 선언
};


class Oval:public Shape{
public:
    Oval(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht*3.14;
    }
    
};


class Rect:public Shape{
public:
    Rect(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht;
    }
    
};

class Triangular:public Shape{
public:
    Triangular(string name,int w, int h):Shape(name,w,h){
    }
    double getArea(){
        return width*hegiht*1/2;
    }
    
};

int main(){
    Shape *p[3];
    p[0]= new Oval("빈대떡",10,20);
    p[1]= new Rect("찰떡",30,40);
    p[2]= new Triangular("토스트",30,40);
    
    for(int i=0; i < 3 ; i++){
        cout<< p[i]->getName() << " 넓이는 " << p[i]->getArea() << endl;
    }
    
    for(int i=0; i < 3 ; i++){
        delete p[i];
    }
    return 0;
}

```

<br>
5. 교재 471p : 문제 9번

```
[프로그램 소스]
#include <iostream>
#include <string>
using namespace std;

//프린터는 모델명 제조사 인쇄매수 인쇄종이 잔량나타내는 정보와
//print(int pages)를 갖는다.
//print를 호출 할 때 마다 인쇄종이 잔량은 int pages 줄어든다.
class Printer{
protected:
    string model,manufacture;
    int printedCount,availableCount;
   
    Printer(string model,string manufacture,int availableCount){
        this->model=model;
        this->manufacture=manufacture;
        this->availableCount=availableCount;
    }
public:
    virtual void print(int pages)=0;
    virtual void show()=0;
    virtual ~Printer(){};
};

// 잉크젯 프린터는 잉크 잔량과 printInkJet(int pages) 함수를 추가로 가진다.

class InkPrinter:public Printer{
    int availableInk;
public:
    InkPrinter(string model="Officejet v40",string manufacture="HP",int availableCount=5,int availableInk=10):Printer(model,manufacture,availableCount){
        this->availableInk=availableInk;
    }
    
    void print(int pages){
        if(pages>availableInk){
            cout<<"잉크가 부족해서 출력할 수 없습니다."<<endl;
        }else if( pages > availableCount){
            cout<<"용지가 부족해서 출력할 수 없습니다."<<endl;
        }else{
            availableCount+=pages;
            availableInk-=pages;
            cout<<"프린트 하였습니다."<<endl;
        }
    }
    
    void show(){
        cout<<"잉크젯 :"<<model<<","<<manufacture<<", 남은 종이 "<<availableCount<<"장,남은 잉크:"<<availableInk<<endl;
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
    
    
    void print(int pages){
        
        if(pages>availableToner){
            cout<<"토너가 부족해서 출력할 수 없습니다."<<endl;
        }else if(pages > availableCount ){
            cout<<"용지가 부족해서 출력할 수 없습니다."<<endl;
        }else{
           
            
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
                availableCount+=pages;
                cout<<"프린트 하였습니다."<<endl;
            }
        }
    }
    
    void show(){
        cout<<"레이저 :"<<model<<","<<manufacture<<", 남은 종이 "<<availableCount<<"장,남은토너:"<<availableToner<<endl;
    }
};




int main(){
    Printer *p[2];
    p[0]=new InkPrinter;
    p[1]=new LaserPrinter;
    
    cout<<"현재 작동중인 2대의 프린터는 아래와 같다."<<endl;
    p[0]->show();
    p[1]->show();
    
    
    
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
                    p[0]->print(pages);
                    flag2=false;
                    break;
                case 2:
                    p[1]->print(pages);
                    flag2=false;
                    break;
                    
                default:
                    cout<<"잘 못 입력하셧습니다."<<endl;
                    break;
            }
        }
        
        
        cout<<endl;
        p[0]->show();
        p[1]->show();
        cout<<endl;
        
        // 잘못 입력했을 경우에도 위 과정을 다시 거치지 않기 위한 과정
        while(true){
            cout<<"계속 프린트 하시겠습니까?(y/n)"<<endl;
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
    for(int i=0; i < 2 ; i++){
        delete p[i];
    }

    return 0;
}
```
