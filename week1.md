연습문제 1
<br>두 정수를 매개변수로 전달받아 두 번째 정수가 첫 번째 정수의 배수이면 true, 아니면 false를 리턴하는 함수 isMultiple() 함수를 작성하고자 한다.
<br>    (1) 함수의 원형을 선언하라.<br>
    (2) 함수를 작성하라.
<br>    (3) 다음과 같이 두 수를 키보드로부터 입력받아 isMultiple() 함수를 호출하는 main() 함수를 작성하고 전체 프로그램을 완성하라

```
#include <iostream>

bool isMultiple(int x, int y); // 함수 원형 선언 

int main(int argc, const char * argv[]) {
    // insert code here...
    int numOne, numTwo;
    
    std::cout << "두 정수 입력"<< std::endl;
    std::cin >> numOne ;
    
    std::cin >> numTwo ;
  
    if( isMultiple( numOne, numTwo ) ){
        std::cout<< "Yes"<< std::endl;
    }else{
        std::cout<< "No"<< std::endl;
    }

    return 0;
}

// 함수 구현
bool isMultiple(int x, int y ){
 
    if(x==0 || y==0)
        return false;
    
    if( y%x==0 ){
        return true;
    }else{
        return false;
    }
}
```

<br>
연습문제2
<br>swapArray() 함수는 매개 변수로 두 개의 배열과 배열의 크기를 전달받고, 두 배열 의 원소를 바꿔치기하며, printArray() 함수는 매개 변수로 전달받은 배열을 화면에 출력한다.
<br>main() 함수에 다음 두 정수형 배열을 선언-보편적 초기화 사용
<br>swapArray() 함수를 호출하여 배열 a와 b의 데이터를 교환하고 다음 출력과 같이 실행되게 하라.

```
#include <iostream>

void swapArray(int *a , int *b , int size);
void printArray(int *a , int size);

int main(int argc, const char * argv[]) {
  
    int a[]={1,2,3,4,5};
    int b[]={9,8,7,6,5};
    int size = sizeof(a)/sizeof(a[0]);
    
    
    std::cout<<"배열 a= ";
    printArray(a, size);
    std::cout<< std::endl <<"배열 b= ";
    printArray(b, size);
    std::cout<< std::endl <<"swapArray 실행";
    swapArray(a, b, size);
    std::cout<< std::endl << "배열 a= ";
    printArray(a, size);
    std::cout<< std::endl <<"배열 b= ";
    printArray(b, size);
    std::cout<< std::endl;
    
    
    return 0;
    
}

void swapArray(int *a , int *b , int size){

    int temp;
    int i;
    
    for(i=0;i<size;i++){
        temp=a[i];
        a[i]=b[i];
        b[i]=temp;
    }
    
}

void printArray(int *p , int size){
    int i;
    for( i=0; i<size ; i++){
        std::cout<<p[i]<<" ";
    }
}
```
