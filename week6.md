1. 교재 274p : 문제11번

```
#include <iostream>
#include <string>
using namespace std;

// 스트링 사용
class Book{
    string title;
    int price;
public:
    Book( string title, int price);
    ~Book();
    // 디폴트 복사 생성자 이용
    void set(string title , int price);
    void show(){ cout<< title << ' ' << price << "원" << endl;};
};

Book::Book( string title , int price){
    this->title=title;
    this->price=price;
}

Book::~Book(){
   
}

void Book::set(string title, int price){
   

    this->title=title;
    this->price=price;
}


int main(){
    Book cpp("명품c++",10000);
    Book java=cpp;// 복사 생성자 호출됨
    java.set("명품자바", 12000);
    cpp.show();
    java.show();
    
    return 0;
}

/////////////////////////////////////////////////////


#include <iostream>

using namespace std;

class Book{
    char *title;
    int price;
public:
    Book( const char *title, int price);
    ~Book();
    Book(Book &book);
    void set(char *title , int price);
    void show(){ cout<< title << ' ' << price << "원" << endl;};
};

Book::Book( const char *title , int price){
    int len=strlen(title);
    this->title= new char[len+1];
    strcpy(this->title,title);
    this->price=price;
}

Book::~Book(){
    delete [] title;
}

void Book::set(char *title, int price){
    if(this->title!=NULL){
        delete [] this->title;
    }
    
    int len=strlen(title);
    this->title= new char[len+1];
    strcpy(this->title,title);
    this->price=price;
}

// 깊은 복사 // 에러나지 않도록 만든 복사 생성자
Book::Book(Book& book){
    int len=strlen(book.title);
    this->title= new char[len+1];
    strcpy(this->title,book.title);
    this->price=book.price;
}


// 얕은 복사 /// 컴파일러가 자종으로 생성하는 복사생성자 
Book::Book(Book& book){
    this->title=book.title;
    this->price=book.price;
}

int main(){
    Book cpp("명품c++",10000);
    Book java=cpp;// 복사 생성자 호출됨
    java.set("명품자바", 12000);
    cpp.show();
    java.show();
    
    return 0;
}
```

<br>
2. 교재 275p : 문제12번

```
[프로그램 소스]

#include <iostream>
#include <string>
using namespace std;

class Dept{
    int size;
    int *scores;
public:
    Dept(int size){
        this->size=size;
        scores = new int[size];
    }
   // Dept(Dept& dept);
    ~Dept();
    int getSize(){ return  size;}
    void read();// size 만큼 키보드에서 정수를 읽어 scores 배얄에 저장.
    bool isOver60(int index); //index의 값이 60보다 클경우 true 반환
};

/*    복사 생성자 // 
Dept::Dept(Dept &dept){
    this->size=dept.size;
    this->scores=new int[size];
    for(int i = 0; i< size ; i++){
        this->scores[i]=dept.scores[i];
    }
}
*/

Dept::~Dept(){
    delete []scores;
}

void Dept::read(){
    cout<<this->size<<"정수 입력>>";
    for(int i = 0 ; i < this->size ; i++){
        cin>>scores[i];
    }
}

bool Dept::isOver60(int index){
    if(scores[index]>60){
        return true;
    }
    return false;
}


//복사 생성자 없으면 scores의  메모리가  반환된다.

int countPass(Dept &dept){ //  복사 생성자 없이 오류가 나지 않도록 매개변수를 참조로 넘겨준다
    int count = 0;
    for(int i=0; i<dept.getSize(); i++){
        if(dept.isOver60(i)) count++;
    }
    return count;
}

int main(){
    Dept com(10);
    com.read();
   int n = countPass(com); // 값을 전달 할 때 복사생성자가 실행된다. 
    cout<< "60점 이상은 " << n << "명"<< endl;
    return 0;
}

```
