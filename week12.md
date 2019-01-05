1. 교재 525p : 문제 2번

```
#include <iostream>

using namespace std;

// 문제2번
// 두개 배열을 비교하여 같으면 true 아니면 false를 반환하는 제너릭 함수를 작성하라
template <class T>
bool equalsArrays(const T *a,const T *b,const int length){
    bool re=true;
    for(int i=0;i<length;i++){
        if(a[i]!=b[i]){
            re=false;
            i=length;
        }
    }
    return re;
}


int  main(){
    int x[]={1,10,1-0,5,4};
    int y[]={1,10,100,5,4};
    
    if(equalsArrays(x, y, 5)){
        cout<<"같다\n";
    }else{
        cout<<"다르다\n";
    }
}

```
<br>
2. 교재 525p : 문제 3번

```
[프로그램 소스]
#include <iostream>

using namespace std;
// 문제 3번
// reverseArray작성

template <class T>
void reverseArray(T *a,int leng){
    
    T *b=new T[leng]; // 새로운 배열 생성
    
    for(int i=0;i<5;i++){ // 새로운 배열에 기존 값을 거꾸로 복사한다.
        b[--leng]=a[i];
    }
    
    for(int i=0;i<5;i++){ // 값을 원 배열에 전달한다.
        a[i]=b[i];
    }
    
}

int main(){
    int x[]={1,10,100,5,4};
    
    reverseArray(x, 5);
    
    for(int i=0;i<5;i++){
        cout<<x[i]<<" ";
    }
    cout<<endl;
    return 0;
}
```

<br>
3. 교재 525p : 문제 4번

```
#include <iostream>

using namespace std;
// 문제 4번
// 배열에서 원소를 찾는 search함수

template <class T>
int search(T a,T *b,int length){
    bool con=false;
    for(int i = 0 ; i < length ; i++){
        if(a==b[i]){
            con=true;
            i=length;
        }
    }
    return con;
}


int main(){
    int x[]={1,10,100,5,4};
    
    if(search(100,x,5)){
        cout<<"100이 배열에 포함되 있습니다.\n";
    }else{
        cout<<"100이 배열에 포함되 있지 않습니다.\n";
    }
    
    return 0;
}

```

4.교재 527p : 문제 8번

```
// 문제 8번
#include <iostream>
using namespace std;


class Comparable{
public:
    virtual bool operator>(Comparable& op)=0;
    virtual bool operator<(Comparable& op)=0;
    virtual bool operator==(Comparable& op)=0;
};


class Circle:public Comparable{
    int radius;
public:
    Circle(int radius=1){this->radius=radius;}
    int getRadius(){ return radius;}

    virtual bool operator>(Comparable& op){
        Circle *ci=dynamic_cast<Circle *>(&op);
        
        if(ci->getRadius() > this->getRadius() ){
            return false;
        }
        return true;
    };
    bool operator<(Comparable& op){
        Circle *ci=dynamic_cast<Circle *>(&op);
        
        if(ci->getRadius() > this->getRadius() ){
            return true;
        }
        return false;
    };
    bool operator==(Comparable& op){
        Circle *ci=dynamic_cast<Circle *>(&op);
        
        if(ci->getRadius() == this->getRadius() ){
            return true;
        }
        return false;
        
    };
};



template<class T>
T bigger(T a , T b){
    if(a > b){ return a;
    }else{ return b;
    }
}

int main(){
    int a=20,b=50,c;
    c=bigger(a, b);
    cout<<"20과 50중 큰 값은 "<< c << endl;
    Circle waffle(10),pizza(20),y;
    
    y=bigger(waffle, pizza);
    cout<<"waffle과 pizza중 큰 것의 반지름은 "<< y.getRadius() <<endl;
}

```

<br>
5. 교재 527p : 문제 9번

```
// 문제 9번
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> vec;
    int input=1;
    int i=0;
    double sum=0;
   
    
    while(true){
        cout<<"정수를 입력하세요(0을 입력하면 종료)>>";
        cin>>input;
        if(input!=0)
            vec.push_back(input);
        else
            break;
        
        sum=0;
        i++;
        for(int k=0;k<i;k++){
            sum+=vec.at(k);
            cout<<vec.at(k)<<" ";
        }
        cout<<"\n평균 ="<< sum/i<<endl;
    }

    return 0;
}

```
