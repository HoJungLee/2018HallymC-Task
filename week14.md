1. 교재 581p : 문제 4번

```
#include <iostream>

using namespace std;

int main() {
	char word3[50];
	char word2[50];
	char word[50];

	while(1){
		//반복할 때를 대비해 버퍼를 지운다.
		cin.clear();
		// 원문장을 입력
		cin.get(word, 50);

		// 원문장을 거꾸로 버퍼의 입력
		for (int i = 0; i < strlen(word); i++) {
			cin.putback(word[i]);
		}
		//ignore를 이용해 ; 앞 문장을 삭제한다.
		cin.ignore(50, ';');

		// ;뒤가 제거된 거꾸로된 문장이 만들어진다.
		cin.get(word2, 50);

		cin.clear();
		// 거꾸로 된 문장을 다시 반대로 버퍼의 입력해준다.
		for (int i = 0; i < strlen(word2); i++) {
			cin.putback(word2[i]);
		}
		// 버퍼에서 문장을 입력받는다.
		cin.get(word3, 50);
		// 출력한다.
		cout << word3;

		cin.clear();

		// 종료를 위함
		if (cin.get() == EOF) {
			break;
		}
	}
}
```

<br>
2. 교재 583p : 문제 7번

```
[프로그램 소스]
//7번 문제

#include <iostream>
#include <iomanip>
#include <cctype>
using namespace std;

int main() {
    cout << showbase;
    
    // 타이틀을 출력한다.
    for(int i=0;i<4;i++){
        cout << left<< setw(8) << "dec";
        cout << left<<setw(8) << "hexa";
        cout << left<<setw(8) << "char" ;
    }
    cout <<endl;
    
    // 타이틀 밑에 선을 출력한다.
    for(int i=0;i<4;i++){
        cout << left<< setw(8) << "___";
        cout << left<< setw(8) << "____";
        cout << left<< setw(8) << "____" ;
    }
    cout <<endl;

    // 이중 반복문을 통하여 출력한다
    // 행의 정보를 갖는다.
    for(int i=0; i<=60; i+=4) {
        for(int j=0; j<4; j++){ //3가지열이 4번 반복된다.
            cout << setw(8) << setfill(' ') << dec << i+j; // 10진수
            cout.unsetf(cout.showbase);
            cout << setw(8) << setfill(' ') << hex << i+j; // 16진수
            if(isprint(i+j)){ // 문자열로 바꿀 수 있는지 여부를 확인
                cout << setw(8) << setfill(' ')<< char(i+j); // 문자
            }else{
                cout << setw(8) << setfill(' ')<< '.'; // . 출력
            }
        }
         cout<<endl; // 줄바꿈
    }
}

```

<br>
3. 교재 584p : 문제 9번

```
[프로그램 소스]
 #include <iostream>
#include <string>
using namespace std;

class Phone {
    string name;
    string telnum;
    string address;
public:
    Phone(string name="",string telnum="",string address=""){
        this->name=name;
        this->telnum=telnum;
        this->address=address;
    }
    friend istream& operator >> (istream& ins, Phone &a); // friend 선언
    friend ostream& operator << (ostream& stream, Phone &a); // friend 선언
};

istream& operator >> (istream& ins, Phone &a) { // >> 연산자 함수
    cout << "이름:";
    ins >> a.name;
    cout << "전화번호:";
    ins >> a.telnum;
    cout << "주소:";
    ins >> a.address;
    return ins;
}

ostream& operator << (ostream& stream, Phone &a) { // << 연산자 함수
    stream << "(" <<a.name <<","<<a.telnum<<","<<a.address<<")\n";
    return stream;
}

int main() {
    Phone girl,boy;
    cin >> girl >> boy;  // >> 연산자를 호출하여 x 좌표와 y 좌표를 키보드로 읽어 객체 p 완성
    cout << girl << boy;  // << 연산자를 호출하여 객체 p 출력
}

```

<br>
4. 교재 586p : 문제 12번

```
[프로그램 소스]
Main.cpp


#include <iostream>
#include <string>
#include "coffee.hpp"


#define size 5 // 커피가 몇가지 재료로 구성되는지를 나타낸다.
using namespace std;


int main(){
    string name[size]={"Coffee","Sugar","CREAM","Water","Cup"};
    int many[size]={3,3,3,3,3};
    int Brecipe[size]={1,0,0,1,1};
    int Drecipe[size]={1,1,0,1,1};
    int Urecipe[size]={1,0,1,1,1};
    coffee cafe(name,many); // 커피를 조절할 전체량
    coffee black(name,Brecipe,"블랙"); // 블랙 커피
    coffee dalcom(name,Drecipe,"설탕"); // 설탕 커피
    coffee Botong(name,Urecipe,"보통"); // 보통 커피
    
    int choice;
    bool run=true;
    cout<<"-----명품 커피 자판기입니다.-----"<<endl;
    
    while(run){
        cafe.show();
        cout<<endl<<endl;
        cout<<"보통 커피:0, 설탕 커피:1, 블랙커피:2, 채우기:3,종료:4>>";
        cin>>choice;
        switch (choice) {
            case 0:
                cafe-Botong;
                break;
            case 1:
                cafe-dalcom;
                break;
            case 2:
                cafe-black;
                break;
            case 3:
                cafe.full();
                break;
            case 4:
                run=false;
                break;
            default:
                break;
        }
    }

    
    return 0;
}

Ingredients.hpp

#ifndef ingredients_hpp
#define ingredients_hpp

#include <stdio.h>
#include <string>

using namespace std;

class ingredients{
    string name; // 재료이름
    int many; // 재료 량
public:
    // 선언문
    ingredients(string name="",int many=0);
    // 재료의 이름 같다면 재료의 량을 빼준다.
    void operator-(ingredients op);
    
    // 재료의 량을 비교하여 매개변수 보다 큰 값을 가지면 true를 반환한다.
    // coffee클래스에서 재료의 량을 비교하여 커피를 만들수 있는지 확인할 때 사용한다.
    bool compare(ingredients op);
    
    // 재료 량의 정보를 변경한다.
    void insert(int many);
    // 재료명 반환
    string getName();
    // 재료의 량을 *으로 표시된 문자열로 반환한다.
    string getMany();
    
};


#endif /* ingredients_hpp */

Ingredients.cpp

#include "ingredients.hpp"
#include <string>

using namespace std;

ingredients::ingredients(string name,int many){
        this->name=name;
        this->many=many;
    }
    
    // 재료의 이름 같다면 재료의 량을 빼준다.
void ingredients::operator-(ingredients op){
        this->many-=op.many;
    }
    
    // 재료의 량을 비교하여 매개변수 보다 큰 값을 가지면 true를 반환한다.
    // coffee클래스에서 재료의 량을 비교하여 커피를 만들수 있는지 확인할 때 사용한다.
bool ingredients::compare(ingredients op){
        bool result=true;
        if(op.many > this->many){
            result=false;
        }
        return result;
    }
    
    // 재료 량의 정보를 변경한다.
void ingredients::insert(int many){
        this->many=many;
    }
    // 재료명 반환
string ingredients::getName(){
        return this->name;
    }
    // 재료의 량을 *으로 표시된 문자열로 반환한다.
string ingredients::getMany(){
        string temp;
        for(int i=0;i<this->many;i++){
            temp+="*";
        }
        return temp;
    }


Coffee.hpp

#ifndef coffee_hpp
#define coffee_hpp

#include <iostream>
#include <string>
#include "ingredients.hpp"
#define size 5 // 커피가 몇가지 재료로 구성되는지를 나타낸다.
using namespace std;

class coffee{
    ingredients list[size];
    string CN;
public:
    coffee(string *name,int *many,string CN="");
    // 모든 재료의 량을 변경한다.
    void full(int many=3);
    
    // 커피를 만들수 있는지를 확인한 뒤 커피를 만든다.
    void operator-(coffee op);
    
    // 커피명 반환
    string getCN();
    
    // 커피클래스가 갖고 있는 재료 정보를 출력한다.
    void show();
    
};


#endif /* coffee_hpp */


Coffee.cpp
#include "coffee.hpp"
#include <string>
using namespace std;


coffee::coffee(string *name,int *many,string CN){
    for(int i=0;i<size;i++){
        list[i]=ingredients(name[i],many[i]);
    }
    this->CN=CN;
}
// 모든 재료의 량을 변경한다.
void coffee::full(int many){
    cout<<"모든 통을 채웁니다.~~"<<endl;
    for(int i=0;i<size;i++){
        list[i].insert(many);
    }
}

// 커피를 만들수 있는지를 확인한 뒤 커피를 만든다.
void coffee::operator-(coffee op){
    bool confirm=true;
    for(int i=0;i<size;i++){
        confirm = this->list[i].compare(op.list[i]);
        if(confirm==false){
            cout<<"----재료 부족----"<<endl;
            break;
        }
    }
    if(confirm){
        cout<<"맛있는 "<<op.getCN()<<" 커피 나왔습니다~~"<<endl;
        for(int i=0;i<size;i++){
            this->list[i]-op.list[i];
        }
    }
}
// 커피명 반환
string coffee::getCN(){
    return CN;
}

// 커피클래스가 갖고 있는 재료 정보를 출력한다.
void coffee::show(){
    for(int i=0;i<size;i++){
        cout.width(10);
        cout.fill(' ');
        cout<<this->list[i].getName();
        cout.width(10);
        cout.fill(' ');
        cout<<this->list[i].getMany()<<endl;
    }
}

```

