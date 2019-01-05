1.교재 316p : 문제6번

```
// 배열을 합치기 위한 함수

static int* concat(int s1[], int s2[], int size){
    int *s3=new int[size*2];
    
    // s1 배열을 먼저
    for(int i = 0; i<size ; i++){
        s3[i]=s1[i];
    }
    
    // s2 배열을 뒤에 저장한다.
    for(int i=0; i< size ; i++){
        s3[i+size]=s2[i];
    }
    
    return s3;
}


// s1에서 s2에 있는 숫자를 모두 삭제한 새로운 배열을 동적 생성하여 리턴, 리턴하는 배열의크기는
// retsize에 전달
 
static int* remove(int s1[] , int s2[] , int size , int& retSize){
    
    retSize=0; // s1과 s2에 원소가 같은 것이 얼마나 있는지 저장한다.
    
    
    // 이중 반복문을 통하여 s1과 s2에 중복을 확인한다.
    
    for(int i =0; i< size; i++){
        for(int k=0; k < size ; k++){
            if(s1[i]==s2[k]){
                s1[i]=NULL; // 중복되어 있다면 값을 null로 변경한다.
                retSize++;
                break;
            }
        }
    }

    retSize=size-retSize; // 전체에서 겹친 부분 만큼의 갯수를 빼준 값을 저장한다.
    int* s3=new int[retSize]; // 겹치지 않은 수 만큼의 배열을 생성한다.

    
    int k=0; // s3의 배열 인덱스
    for(int i =0; i < size ; i++){
        if( s1[i]!=NULL){ // s1이 null이 아니라면 s3에 값을 저장한다.
            s3[k]=s1[i];
            k++;// s3 에 값이 저장된다면 인덱스를 증가시킨다.
        }
    }
    
    return s3;
}



// 배열 입력을 위한 함수
void input(int* s,int size,char ch){
    cout<< "정수를 "<<size<<" 개 입력하라. 배열 "<<ch<<"에 삽입한다.";
    for(int i = 0; i< size ; i++){
        cin>>s[i];
    }
    cin.ignore();
}

// 배열을 출력하기 위한 함수
void show(int *s,int size){
    for(int i =0; i<size;i++){
        cout<<s[i]<<" ";
    }
    cout<<endl;
}

int main(){
    int size=5;
    int *s1=new int[size];
    int *s2=new int[size];
    int retSize=0;
    
    input(s1, size, 'x');
    input(s2, size, 'y');
    
    show(s2,size);
    cout<<"합친 정수 배열을 출력한다."<<endl;
    int *s3=concat(s1, s2, size);
    show(s3, size*2 );
    
    s1=remove(s1, s2, size , retSize);
    cout<<"배열 x[]에서 y[]를 뺀 결과를 출력한다. 개수는"<<retSize<<endl;
    show(s1,retSize);
    
}

```

<br>
2. 교재 318p : 문제9번

```
[프로그램 소스]
// 316페이지 9번 문제
 
#include <iostream>
#include <string>
using namespace std;

class Board{
public:
    static string str;
    static int index;
    static void add(string st);
    static void print();
};

string Board::str="**********게시판입니다***********\n";
int Board::index=0;

void Board::print(){
    cout<<str<<endl;
}

void Board::add(string st){
    string a= to_string(index)+": " ;// index: 으로 표시하기 위한 문자열
    str+=a; // 문자열을 기존 게시판글에 합한다.
    str+=st; // 새로운 문자열을 게시판글에 합한다.
    str+="\n"; // 한 줄 넘겨준다.
    index++;// 다음을 위하여 index를 증가시켜 준다.
}


int main(){
    Board::add("중간고사는 감독 없는 장율 시험입니다.");
    Board::add("코딩 라운지 많이 이용해 주세요.");
    Board::print();
    Board::add("진소리 학생이 경진대회 입상하였습니다. 축하해주세요");
    Board::print();
    
    
    
    return 0;
}

```

3.교재 366p : 문제1~4번

```
[프로그램 소스] -1번

class Book{
    string title;
    int price,pages;
public:
    Book(string title="",int price=0, int pages=0){
        this->title=title;
        this->price=price;
        this->pages=pages;
    }
    void show(){
        cout<< title <<' '<< price << "원 "<<pages << " 페이지"<< endl;
    }
    string getTitle(){
        return title;
    }
   //Book operator+=(Book,int);
   //Book operator-=(Book,int);
    friend Book operator+=(Book &a, int pri);
   friend Book operator-=(Book &a, int pri);
};
/*
// += 맴버 함수로 구현
Book Book::operator+=(int pri){
    this->price+=pri;
    return *this;
}

Book Book::operator-=(int pri){
    this->price-=pri;
    return *this;
}
*/
 // 외부 함수 구현
Book operator+=(Book &a,int pri){
    a.price+=pri;
    return a;
}

Book operator-=(Book &a,int pri){
    a.price-=pri;
    return a;
}

int main(){
    Book a("청춘",20000,300),b("미래",30000,500);
    a+=500;
b-=500;
a.show();
b.show();

    return 0;
}

```

```
[프로그램 소스] -2번
class Book{
    string title;
    int price,pages;
public:
    Book(string title="",int price=0, int pages=0){
        this->title=title;
        this->price=price;
        this->pages=pages;
    }
    void show(){
        cout<< title <<' '<< price << "원 "<<pages << " 페이지"<< endl;
    }
    string getTitle(){
        return title;
    }
bool operator==(Book);
     bool operator==(string);
     bool operator==(int);

 };

// 맴버 함수 구현
bool Book::operator==(Book a){
    bool con=true;
    
    if(this->pages!=a.pages)
        con=false;
    if(this->price!=a.price)
        con=false;
    if(this->title!=a.title)
        con=false;
    
    return con;
}

bool Book::operator==(int a){
    bool con=true;
    
    if(this->price!=a)
        con=false;
    
    return con;
}
bool Book::operator==(string a){
    bool con=true;
    
    if(this->title!=a)
        con=false;
    
    return con;
}

*/

//  전체 비교
bool operator==(Book a,Book b){
    bool con=true;
    
    if(b.pages!=a.pages)
        con=false;
    if(b.price!=a.price)
        con=false;
    if(b.title!=a.title)
        con=false;
    
    
    return con;
}
//  가격 비교
bool operator==(Book a,int b){
    bool con=true;
    
    if(a.price!=b)
        con=false;
    
    return con;
}

// 스트링 비교
bool operator==(Book a,string b){
    bool con=true;
    
    if(a.title!=b)
        con=false;
    
    return con;
}


int main(){
    Book a("명품 c++",30000,500),b("고품 c++",30000,500);
    
    if(a==30000) cout<<"정가 30000원입니다."<<endl;
    if(a=="명품 c++") cout<<"명품 c++입니다."<<endl;
    if(a==b) cout<< "두 책이 같은 책입니다. "<<endl;
    
  return 0;
}
```

```
[프로그램 소스] -3번
#include <iostream>
#include <string>
using namespace std;

/*
  문제 1~4까지 사용될 Book 클래스는 다음과 같다.
 */
class Book{
    string title;
    int price,pages;
public:
    Book(string title="",int price=0, int pages=0){
        this->title=title;
        this->price=price;
        this->pages=pages;
    }
    void show(){
        cout<< title <<' '<< price << "원 "<<pages << " 페이지"<< endl;
    }
    string getTitle(){
        return title;
    }    
    bool operator!();
    
};
bool Book::operator!(){
    bool con=true;
    if(this->price!=0)
        con=false;
    
    return con;
}
int main(){
    Book book("벼룩시장",0,50);
    if(!book) cout<<"공짜다"<<endl;
    return 0;
}
```

```
[프로그램 소스] -4번
#include <iostream>
#include <string>
using namespace std;

/*
  문제 1~4까지 사용될 Book 클래스는 다음과 같다.
 */
class Book{
    string title;
    int price,pages;
public:
    Book(string title="",int price=0, int pages=0){
        this->title=title;
        this->price=price;
        this->pages=pages;
    }
    void show(){
        cout<< title <<' '<< price << "원 "<<pages << " 페이지"<< endl;
    }
    string getTitle(){
        return title;
    }
};

bool operator<(string a,Book b){
    bool con=true;
    
    if(a>=b.getTitle()){
        con=false;
    }
    
    return con;
}

int main(){
    Book a("청춘",20000,300);
    string b;
    cout<<"책 이름을 입력하세요.>>";
    getline(cin, b);
    if(b < a)
        cout<< a.getTitle() <<"이 "<< b << "보다 뒤에 있구나!"<<endl;
    return 0;
}

```

<br>
4. 교재 369p : 문제7번

```
[프로그램 소스]
// 프랜드 함수로 구현
#include <iostream>
#include <string>
using namespace std;

class Matrix{
    int v[4];
public:
    Matrix(int f=0,int s=0, int t=0,int fo=0){
        v[0]=f;
        v[1]=s;
        v[2]=t;
        v[3]=fo;
    }
   
    void show(){
        cout<<"Matrix =";
        for(int i=0; i<4;i++){
            cout<<v[i]<<" ";
        }
        cout<<endl;
    }
    friend void operator >> (Matrix&,int *);
    friend void operator << (Matrix&,int *);
};

void operator >> (Matrix &a,int *b){
    for(int i=0; i<4;i++){
        b[i]=a.v[i];
    }
}
void operator << (Matrix &a,int *b){
    for(int i=0; i<4;i++){
        a.v[i]=b[i];
    }
}


int main(){
    Matrix a(4,3,2,1),b;
    int x[4],y[4]={1,2,3,4};
    
    a >> x;
    b << y;
    for(int i=0; i<4;i++) cout<<x[i]<<' ';
    cout<<endl;
    b.show();
    return 0;
}

// 맴버 함수로 구현

#include <iostream>
#include <string>
using namespace std;

class Matrix{
    int v[4];
public:
    Matrix(int f=0,int s=0, int t=0,int fo=0){
        v[0]=f;
        v[1]=s;
        v[2]=t;
        v[3]=fo;
    }
    void operator >>(int *a){
        for(int i=0; i<4;i++){
            a[i]=v[i];
        }
    }
    void operator <<(int *a){
        for(int i=0; i<4;i++){
            v[i]=a[i];
        }
    }
    void show(){
        cout<<"Matrix =";
        for(int i=0; i<4;i++){
            cout<<v[i]<<" ";
        }
        cout<<endl;
    }
};

int main(){
    Matrix a(4,3,2,1),b;
    int x[4],y[4]={1,2,3,4};
    
    a >> x;
    b << y;
    for(int i=0; i<4;i++) cout<<x[i]<<' ';
    cout<<endl;
    b.show();
    return 0;
}

```

