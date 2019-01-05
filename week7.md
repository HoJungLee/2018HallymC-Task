1.교재 313p : 문제1번

```
[프로그램 소스]

// 과제 6장 1번

 
#include <iostream>
using namespace std;


 
// add() 함수를 중복 작성하고 프로그램을 완성하라.
/*
int add(int *arr, int length){
    int sum=0;
    for(int i =0 ; i < length ; i++){
        sum+=arr[i];
    }
    return sum;
}

int add(int *arr, int length , int *arr2){
    int sum=0;
    for(int i =0 ; i < length ; i++){
        sum+=arr[i]+arr2[i];
    }
    return sum;
}
 */

// 디폴트 매개 변수를 가진 하나의 add함수
int add(int *arr, int length , int *arr2=NULL){
    int sum=0;
    int sum2=0;
    
    for(int i =0 ; i < length ; i++){
        sum+=arr[i];
    }
    if(arr2!=NULL){
        sum2=add(arr2,length);
    }
    
    return sum+sum2;
}

int main(){
    
    int a[] = {1,2,3,4,5};
    int b[] = {6,7,8,9,10};
    int c = add(a,5);
    int d = add(a,5,b);
    
    cout<<c<<endl;
    cout<<d<<endl;

    
    return 0;
}
```

<br>
2.교재 313p : 문제2번

```
[프로그램 소스]

 //  6장 2번
#include <iostream>
#include <string>
using namespace std;

class Person{
    int id;
    double weight;
    string name;
public:
    //  중복 생성자
    // Person();
    // Person(int id, string name);
    // Person(int id, string name,double weight);
    
    Person(int id=1, string name="Grace",double weight=20.5); // 디폴트 매겨 변수를 가진 하나의 생성자 선언
    void show(){ cout<< id << ' '<< weight <<' '<< name << endl; }
};


//Person::Person():id(1),name("Grace"),weight(20.5){};
//Person::Person(int id, string name):id(id),name(name),weight(20.5){};
Person::Person(int id, string name,double weight):id(id),name(name),weight(weight){};


int main(){
    Person grace,ashley(2,"Ashley"),helen(3,"Helen",32.5);
    grace.show();
    ashley.show();
    helen.show();
}
```
<br>
3.교재 313p : 문제3번

```
// 6장 3번
#include <iostream>
using namespace std;

/* 
// 중복 함수로 처리

int big(int x, int y){
    if(x<y)
        x=y;
    
    if(x>100)
        x=100;
    
    return x;
}

int big(int x, int y , int z){
    if(x<y)
        x=y;
    if(x<z)
        x=z;
    return x;
}

*/
int big( int x , int y , int z=NULL){
    
    if(z==NULL){
        if(x<y)
            x=y;
        if(x>100)
            x=100;
    }else{
        if(x<y)
            x=y;
        if(x<z)
            x=z;
    }
 
    
    
    return x;
}
int main(){
    int x=big(3,5);
    int y=big(300, 60);
    int z=big(30, 60 , 50);
    cout<<x << ' '<<y <<' '<< z <<endl;
    
}

```

<br>
4. 교재 313p : 문제4번

```
[프로그램 소스]
#include <iostream>
using namespace std;

class MyVector{
    int *mem;
    int size;
public:
   // MyVector();
    //   MyVector(int n, int val);
    MyVector(int n=100, int val=0); // 선언시 기본값을 지정
    ~MyVector(){ delete [] mem;}
    void disp();
};

/*
 // 매개변수가 없는 생성자
MyVector::MyVector(){
    mem = new int[100];
    size = 100;
    for(int i = 0; i < size ; i++){ mem[i] = 0; }
    
}
*/

// 매개변수를 갖는 생성자
MyVector::MyVector(int n , int val){
    mem = new int [n];
    size = n;
    for( int i=0; i<size; i++){ mem[i] = val; }
}





void MyVector::disp(){
    cout<<"szie:"<<this->size<<" value:" <<this->mem[0] <<endl;
    
}

int main(){
    MyVector a,b(10,1);
    
    a.disp();
    b.disp();
    
    return 0;
}
```
