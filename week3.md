1. 교재 151p 문제 5번, 6번, 7번 - 클래스 선언부와 구현부를 파일로 분리하고 main() 함수부분을 main.cpp로 분리하여 프로그램을 완성하시오

```
// 5번 main
 

#include <iostream>
#include <cstdlib>
#include <ctime>
#include "Random.h"

using namespace std;

int main(){
    srand( (unsigned int)time(0));
    
    Random r;
    cout<<"--0에서"<<RAND_MAX<<"까지의 랜덤 정수 10개--"<< endl;
    
    for(int i=0;i<10;i++){
        int n=r.next();
        cout << n << ' ';
    }
    
    cout << endl << endl <<"--2에서 "<<"4 까지의 랜덤 정수 10개--"<<endl;
    for(int i=0;i<10;i++){
        int n=r.nextInRange(2, 4);
        cout << n << ' ';
    }
    cout << endl;
    return 0;
}

// 5번 header

#ifndef Ramdom_h
#define Ramdom_h


#endif /* Ramdom_h */
class Random{
public:
    Random(); // 기본 생성자
    int next();
    int nextInRange(int min,int max);
};

// 5번 Random.cpp


#include <iostream>
#include "Random.h"
using namespace std;


Random::Random(){};// 기본 생성자

int Random::next(){ // 0부터 RAND_MAX가 까지의 난수를 반환하는 함수
    return rand()%RAND_MAX;
}

int Random::nextInRange(int min,int max){ // min부터 max까지의 난수를 반환하는 함수
    
    // max에서 min까지 이니 0부터 max-min+1까지 의 난수에 min을 더해 반환한다.
    
    return rand()%(max-min+1)+min;
    
}
// 150페이지 6번 main
 
#include <iostream>
#include <cstdlib>
#include <ctime>
#include "EvenRandom.h"

using namespace std;

int main(){
    srand( (unsigned int)time(0));
    
    EvenRandom r;
    cout<<"--0에서"<<RAND_MAX<<"까지의 랜덤 짝수 10개--"<< endl;
    
    for(int i=0;i<10;i++){
        int n=r.next();
        cout << n << ' ';
    }
    
    cout << endl << endl <<"--2에서 "<<"10 까지의 랜덤 짝수 10개--"<<endl;
    for(int i=0;i<10;i++){
        int n=r.nextInRange(2, 10);
        cout << n << ' ';
    }
    cout << endl;
    return 0;
}

// 150페이지 6번 EvenRandom.h


#ifndef EvenRamdom_h
#define EvenRamdom_h

class EvenRandom{
public:
    EvenRandom();
    int next();
    int nextInRange(int min,int max);
};
#endif /* EvenRamdom_h */


// 150페이지 6번 EvenRandom.cpp


#include <iostream>
#include "EvenRandom.h"
using namespace std;

EvenRandom::EvenRandom(){};

int EvenRandom::next(){
    // 0부터 RAND_MAX가 까지의 난수를 반환하는 함수
    int r=rand()%RAND_MAX;
    if(r%2==0){
        return r;
    }else{
        return r+1;
    }
}

int EvenRandom::nextInRange(int min,int max){ // min부터 max까지의 난수를 반환하는 함수
    
    // max에서 min까지 이니 0부터 max-min+1까지 의 난수에 min을 더해 반환한다.
    int r=rand()%(max-min+1)+min;
    if(r%2==0){
        return r;
    }else{
        return r+1;
    }
    
}



// 150페이지 7번 main


#include <iostream>
#include <cstdlib>
#include <ctime>
#include "SelectableRandom.h"

using namespace std;

int main(){
    srand( (unsigned int)time(0));
    
    SelectableRandom r(false); // 짝수를 반환하는 클래스 생성
    cout<<"--0에서"<<RAND_MAX<<"까지의 짝수 랜덤 정수 10개--"<< endl;
    
    for(int i=0;i<10;i++){
        int n=r.next();
        cout << n << ' ';
    }
    
    
    SelectableRandom rj(true); // 홀수를 반환하는 클래스 생성
    
    cout << endl << endl <<"--2에서 "<<"9 까지의 홀수 랜점 정수 10개--"<<endl;
    for(int i=0;i<10;i++){
        int n=rj.nextInRange(2, 9);
        cout << n << ' ';
    }
    cout << endl;
    return 0;
}

// 150페이지 7번 SelectableRandom.h


#ifndef SelectableRamdom_h
#define SelectableRamdom_h

class SelectableRandom{
    int hol=0;
    int jak=0;
public:
    SelectableRandom(bool select);
    
    int next();
    int nextInRange(int min,int max);
};

#endif /* SelectableRamdom_h */

// 150페이지 7번 SelectableRandom.cpp


#include <iostream>
#include "SelectableRandom.h"
using namespace std;

SelectableRandom::SelectableRandom(bool select){// true일 경우 홀수 flase일 경우 짝수
    if(select){
        hol=1;
    }else{
        jak=1;
    } // 홀수 생성자
}

int SelectableRandom::next(){ // 0부터 RAND_MAX가 까지의 난수를 반환하는 함수
    int r=rand()%RAND_MAX;
    if(r%2==0){
        return r+hol; // 홀수 생성일 때 hol은 1 짝수일 경우 hol=0
    }else{
        return r+jak;// 짝수 생성일 때 jak은 1 홀수 일 경우 jak=0
    }
}
int SelectableRandom::nextInRange(int min,int max){ // min부터 max까지의 난수를 반환하는 함수
    
    // (max-min) 을 포함하지 않는 난수를 반환하고 거기에 min을 더해 min부터 max까지 출력한다.
    
    int r=rand()%(max-min)+min;
    
    if(r%2==0){
        return r+hol;
    }else{
        return r+jak;
    }
    
}


```


<br>
2.교재 151p 문제 11번

```
// 11번 Box.h
#ifndef Box_h
#define Box_h
class Box{
    int width,height;
    char fill;
public:
    Box(int w, int h);
    void setFill(char f);
    void setSize(int w,int h);
    void draw();
};


#endif /* Box_h */



//150페이지 11번 Box.cpp 

#include <iostream>
using namespace std;
#include "Box.h"


// 박스를 생성한다.
Box::Box(int w,int h){
    width =w;
    height = h;
    fill='*';
}


// fill에 값을 채운다.
void Box::setFill(char f){
    fill=f;
}


// 박스 설정하기
void Box::setSize(int w, int h){
    width = w;
    height = h;
}


// 박스 그리기
void Box::draw(){
    for(int i=0;i<height;i++){// 넓이 출력을 높이만큼 반복한다.
        for(int j=0;j<width;j++){// 넓이 만큼 fill을 출력한다.
            cout<<fill;
        }
        cout<<endl;// 넓이 출력이 끝나면 다음 줄로 출력하기 위해 넘긴다.
    }
}
```
<br>
3.교재 210p 문제 1번

```
// 실습과제 210페이지 1번 완료

// color 클래스 구현
// 색상은 red,green,blue 세가지를 int형으로 갖는다.
// 생성자는 기본 생성자
// 색을 설정하는 set과 출력 하는 show
class Color{
    int red,green,blue;
public:
    Color() { red=green=blue=0; }
    Color( int r , int g ,int b){ red=r;green=g; blue=b;}
    void setColor(int r , int g ,int b){ red=r;green=g; blue=b; }
    void show(){ cout<<red<<' '<<green<<' '<<blue<<endl; }
    
};

int main(){
    Color screenColor(255,0,0);// 빨간색의 screenColor 객체 생성
    Color *p;//Color의 타입의 포인터 변수 p선언
    p=&screenColor;//(1) p가 screenColor의 주소를 가지도록 코드 작성
    (*p).show();//(2) p와 show를 이용하여 screenColor 색 출력
    Color colors[3];//(3) Color의 일차원 배열 colors 선언, 원소는 3개
    p=colors;
    
    //(5) p와 setColor를 이용하여 colors[0],colors[1],colors[2]가
    // 각각 빨강,초록,파랑색을 가지도록 코드 작성
    p[0].setColor(255, 0, 0);
    p[1].setColor(0, 255, 0);
    p[2].setColor(0, 0, 255);
    //(6) p와 show()를 이용하여 colors 배열의 모든 객첵의 색 출력, for 문 이용
    for( int i =0 ; i<3 ; i++){
        p[i].show();
    }
    
    
    
    
    
    return 0;
    
}

```
