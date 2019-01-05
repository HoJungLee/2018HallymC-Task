1. 93p 13번

```
#include <iostream>
#include <string>
using namespace std;


int main() {
    
    cout<<"***** 승리장에 오신 것을 환영합니다. *****\n";
    
    int i=0;
    string name;
    int order;
    
    while(i<1){
        
        cout<<"짬뽕:1 , 짜장:2 , 군만두:3, 종료:4 \n";
        cin>>order;
        switch (order) {
            case 1:
                name="짬뽕";
                break;
            case 2:
                name="짜장";
                break;
            case 3:
                name="군만두";
                break;
            case 4:
                i=2;
                continue;
            default:
                cout<<"다시 주문하세요!\n";
                continue;
        }
        cout<<"몇인분? \n";
        cin>>order;
        cout<<name<<" "<<order<<"인분 나왔습니다.\n";
        continue;
        
    }
}
```

<br>
2.교재 92p 문제 14번

```
#include <iostream>
#include <string>
using namespace std;


int main() {
    
    string name;
    int price = 0;
    int jan;
    int sum;
    int i;
    string coffee[3]={"에스프레소","아메리카노","카푸치노"};

    
    for(i=0;i<3;i++){
        cout<<"에스프레소 2000원, 아메리카노 2300원 카푸치노 2500원\n주문>>";
        getline(cin,name);
       
        cin>>jan;
    
        if( name.compare(coffee[0]) ){
            price=2000;
        }
        if( name.compare(coffee[1]) ){
            price=2000;
        }
        if( name.compare(coffee[2]) ){
            price=2000;
        }
    
        price*=jan;
        sum+=price;
        cout<<price<<"입니다. 맛있게 드세요\n";
         cin.ignore();// 버퍼 비우기
    }
    
       cout<<"오늘 "<<sum<<"원을 판매하여 문을 닫습니다. 내일뵈요~~~\n";
        
}
```

<br>
3. 교재 150p 문제 3번

```
#include <iostream>
#include <string>
using namespace std;

class Account{
public:
    string owner;
    int id;
    int save;
    Account(string name,int x,int y);
    void deposit(int x);
    string getOwner();
    int withdraw(int money);
    int inquiry();
};


// 생성자
Account::Account(string nam , int x , int y){
    owner=nam;
    id=x;
    save=y;
}

// 잔액을 함수에 입력된 매개변수의 값만큼 증가 시킨다.
void Account::deposit(int x){
    save+=x;
}

// 계좌주인의 이름을 반환한다.
string Account::getOwner(){
    return owner;
}

// 출금 함수
// 출금 금액이 잔액과 비교후 많거나 같으면 출금후 잔액을 차감
// 출금 금액이 잔액보다 많을 경우 잔액 전부 출금 후 잔액을 0으로 변경
int Account::withdraw(int money){
    if(save>=money){
        save-=money;
        return money;
    }else{
        money=save;
        save=0;
        return money;
    }
}

// 잔액을 반환한다.
int Account::inquiry(){
    return save;
}

int main(){
    Account a("Kitae",1,5000);// 이름이 kitae이고 id가 1번이며 잔액이 5000원인 Account 객채를 생성한다.
    a.deposit(50000); // 50000원을 저금한다.
    cout<< a.getOwner() <<"의 잔액은 "<<  a.inquiry() <<"원 입니다.\n";
    int money=a.withdraw(20000);
    cout<< a.getOwner() <<"의 잔액은 "<<  a.inquiry() <<"원 입니다.\n";
    
}

```

<br>
4.교재 153p 문제 9번

```
#include <iostream>
using std::cin;
using namespace std;

class Oval{
    public:
        int width;
        int height;
    
        int getWidth();
        int getHeight();
        void set(int w , int h);
        void show();
    
        Oval();
        Oval(int w,int h);
        ~Oval();
};
// 생성자
Oval::Oval(){
    width=1;
    height=1;
}
Oval::Oval(int w,int h){
    set(w,h);
}

// 소멸자
Oval::~Oval(){
    cout<<"Oval 소멸 : ";
    show();
}

// get함수들
int Oval::getWidth(){
    return width;
}
int Oval::getHeight(){
    return height;
}
// 현재의 너비와 높이를 출력하는 함수
void Oval::show(){
    cout<<"width ="<<width<<" height ="<<height<<"\n";
}

// 너비와 높이를 설정하는 함수
void Oval::set(int w, int h){
    width=w;
    height=h;
}

int main(){
    Oval a,b(3,4);
    a.set(10, 20);
    a.show();
    cout<<b.getWidth()<<", "<<b.getHeight()<<"\n";
    cout<<1<<2<<'a'<<"hello"<<'\n';
    
}
```
