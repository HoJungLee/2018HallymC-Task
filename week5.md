1. 교재 212p : 문제5번

```
#include <iostream>
#include <string>
#include <ctime>

using namespace std;



int main() {
    
    srand( (unsigned int)time(0)); // 랜덤 시드 설정
    string str; // 문자열
    int n; // 랜덤한 정수를 저장할 변수
    
    // while 반복문을 통해 반복한다.
    while(true){
        cout<<"\n아래에 한 줄을 입력하세요.(exit를 입력하시면 종료됩니다.)\n >>";
        getline(cin,str);
        if(str=="exit"){ break;} // 입력받은 문자열이 exit일 경우 종료
        n= rand()%str.length(); // 입력받은 문자열 길이 중 랜덤한 위치를 찾는다.
        str[n]=(char)rand()%58+65; // 입력받은 랜점한 문자열 순서에 랜덤한 알파벳을 입력한다.
        cout<<str;
    }
    
    return 0;
    
}

```
<br>
2.교재 213p : 문제9번

```
#include <iostream>
#include <string>

using namespace std;

// 클래스 Person 선언
class Person{
    string name;
    string tel;
    
public:
    Person(){};
    string getName(){
        return name;
    }
    string getTel(){
        return tel;
    }
    
    void set(string nam, string te);
};

// set 구현
void Person::set(string nam, string te){
    name=nam;
    tel=te;
}


int main(){
    
   Person ary[3];
    
    string nam;
    string te;
    
    cout<<"이름과 전화번호를 입력해 주세요\n";
    
    for(int i=0;i<3;i++){
        cout<<"사람 "<<i+1<<">>";
        getline(cin, nam);
        getline(cin, te);
        ary[i].set(nam, te);
    }
    
    cout<<"\n모든 사람의 이름은";
    for(int i=0;i<3;i++){
        cout<<ary[i].getName()<<" ";
    }
    
    
    cout<<"\n전화번호 검색합니다. 이름을 입력하세요>>>";
    getline(cin,nam);
    
    
    for(int i=0;i<3;i++){
        if(ary[i].getName()==nam){
            cout<<"\n전화번호는 "<<ary[i].getTel()<<endl;
            break;
        }
    }
    
    
    
    return 0;
}

```

<br>
3.교재 216p : 문제12번

```
[프로그램 소스]
// 216페이지 12번
#include <iostream>
#include <string>

using namespace std;
// 원 클래스 선언
class Circle{
    int radius;
    string name;
public:
    void setCircle(string name, int radius);
    double getArea();
    string getName();
};

 // 원 클래스 함수 구현부
void Circle::setCircle(string name, int radius){
    this->name=name;
    this->radius=radius;
}

double Circle::getArea(){
    double area= (double) radius * 2 * 3.14;
    return area;
}

string Circle::getName(){
    return this->name;
}


// 원매너지 클래스 선언

class CircleManager{
    Circle *p;
    int size;
public:
    CircleManager(int size);
    ~CircleManager();
    void searchByName();
    void searchByArea();
};

 
 // 원클래스 매니저 구현
CircleManager::CircleManager(int size){
    this->size=size;
    Circle *op=new Circle[size]; // 사이즈 만큼 메모리 할당한다.
    string nam;
    int rad;
    for(int i =0; i<size ; i++){ // 메모리 할당 받은 서클의 갯수만큼 반복문을 통하여 초기화 한다.
        cout<<"원 "<<i+1<<"의 이름과 반지름 >>";
        cin.ignore();
        cin>>nam;
        cin>>rad;
        op[i].setCircle(nam, rad);
    }
    this->p=op; // 할당 받은 메모리 영역을 변수 p에 넣어준다.
}

void CircleManager::searchByName(){
    string nam;
    cin.ignore();
    printf("\n검색하고자 하는 원의 이름>>");

    getline(cin, nam);
    for(int i=0;i<this->size;i++){
        if( p[i].getName()==nam ){
            cout<<nam<<"의 면적은 "<<p[i].getArea()<<endl;
            break;
        }
    }
}



void CircleManager::searchByArea(){
    int are;
    cout<<"\n최소 면적을 정수로 입력하세요>>";
    cin>>are;
    cout<<are<<"보다 큰 원을 검색합니다. ";
    for(int i =0; i<this->size;i++){
        if(p[i].getArea()>are){
            cout<<p[i].getName()<<"의 면적은"<<p[i].getArea()<<", ";
        }
    }
    cout<<endl;
}

CircleManager::~CircleManager(){
    
}

int main(){
    int size;
    cout<<"원의 개수 >>";
    cin>>size;
    dec(cout);
    CircleManager CM = CircleManager(size);
    
    CM.searchByName();
    
    CM.searchByArea();
    
    
    
    return 0;
}
```

4. 교재 270p : 문제3번

```
#include <iostream>
#include <string>

using namespace std;

// &참조 연산자 사용하여 text1,2를 합치고 text3값 수정
void combine(string &text1, string &text2, string &text3 ){
    text1.append(" ");
    text1.append(text2);
    text3=text1;
    
}

int main(){
    string text1("i love you"),text2("very much");
    string text3;
    combine(text1, text2, text3);
    cout<<text3<<endl;
    
    
    return 0;
}
```

5.교재 270p : 문제4번

```
[프로그램 소스]
#include <iostream>


using namespace std;

bool bigger(int a, int b , int& big){
    
    if(a==b){
        return true;
    }else if(a>b){
        big=a;
        return false;
    }else{
        big=b;
        return false;
    }
}

int main(){
    int a,b;
    int big;
    cout<<"비교 할 수 a,b >>";
    cin>>a;
    cin>>b;

    if(bigger(a, b, big)){
        cout<<"두 수는 같습니다.\n";
    }else{
        cout<<a<<"와 "<<b<<"중 큰 수는 "<<big<<"입니다. \n";
    }
    
    return 0;
}
```
<br>
6.교재 271p : 문제6번

```
[프로그램 소스]
#include <iostream>
using namespace std;

char& find(char a[],char c,bool& success){
    for(int i=0; i< sizeof(*a)/sizeof(a[0]) ;i++){
        if(a[i]==c){
            success=true;
            return a[i];
        }
    }
    success=false;
    return c; // 형식을 맞추기 위한 반환
}


int main(){
    char s[]="Mike";
    bool b=false;
    char& loc = find(s,'M',b);
    
    if(b==false){
        cout<<"M을 발견할 수 없다."<<endl;
        return 0;
    }
    
    loc = 'm';
    cout<<s<<endl;
    return 0;
}

```
