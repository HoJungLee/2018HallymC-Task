1. 교재 211 페이지 4번

```
[프로그램 소스]
#include <iostream>
using namespace std;

class Sample{
    int *p;
    int size;
public:
    Sample(int n){
        size=n;
        p=new int[n];
    }
    void read(); // 동적 할당받은 정수 배열 p에 사용자로부터 정수를 입력 받음
    void write(); // 정수 배열을 화면에 출력
    int big(); // 정수 배열에서 가장 큰 수 리턴
    ~Sample(); // 소멸자
};


// for문을 이용하여 배열에 정수를 입력한다.
void Sample::read(){
    for(int i =0; i < size ; i++){
        cout<<i+1<<"번쨰 정수 >>";
        cin>>p[i];
    }
}


// for 문을 이용하여 배열을 출력한다.
void Sample::write(){
    for(int i =0; i < size ; i++){
        cout<<p[i]<<" ";
    }
    cout<<endl;
}


int Sample::big(){
    
    int big=p[0]; // return할 값을 저장하는 변수인 big에 p[0]를 저장한다.
    // 배열이 생성된다면 p[0]는 반드시 생성 된다.
    
    // 배열에 2번째 부터 비교한다.
    for(int i =1; i < size ; i++){
        if( p[i] > big){ // p[i]가 big보다 크다면 big에 p[i] 를 저장한다.
            big=p[i];
        }
    }
    
    return big;
}


// 소멸자 할당 받은 메모리를 반환한다.
Sample::~Sample(){
    delete[] p;
    
}


int main(){
    Sample s(10);// 10개의 정수 배열을 가진 Sample 객체 생성
    s.read(); // 키보드에서 정수 배열 읽기
    
    s.write(); // 정수 배열 출력
    
    cout<<"가장 큰 수는 "<<s.big() << endl; // 가장 큰 수 출력
    
    return 0;
}

```

<br>
2.객체 배열의 동적 생성 및 반환

```
#include <iostream>
using namespace std;
class Circle {
	int radius; 
public:
	Circle();
	Circle(int r);
       ~Circle();
	void setRadius(int r)  { radius = r; } 
	double getArea(); 
}; 
double Circle::getArea() {
	return 3.14*radius*radius;
}

Circle::Circle() {
	radius=1;
       cout<<”생성자 실행 radius = “<<radius<<endl;
}

Circle::Circle(int r) {
	radius=r;
       cout<<”생성자 실행 radius = “<<radius<<endl;
}

 Circle::~Circle() {
	radius=1;
       cout<<”소멸자 실행 radius = “<<radius<<두이;
}

int main() {
	Circle *circleArray = new Circle[3]; 	// Circle 객체 배열 동적 생성, default 생성자 호출

	circleArray[0].setRadius(10); 								circleArray[1].setRadius(20);
	circleArray[2].setRadius(30);

	for(int i=0; i<3; i++) // 배열의 각 원소 객체의 멤버 접근
		cout << "Circle " << i << "의 면적은 " << circleArray[i].getArea() << endl;

	Circle *p= circleArray;      // 포인터 p에 배열의 주소값 설정
		for(int i=0; i<3; i++) { 	// 객체 포인터로 배열 접근 
		cout << "Circle " << i << "의 면적은 " << p->getArea() << endl;
		p++; 		}
       delete[] circleArray;  //객체 배열 반환
}
```

<br>
3. 교재 213 페이지 8번 – 위의 예제로 제시된Circle 클래스를 사용할 것

```
int main() {
    int createCircle; // 만들 원의 갯수를 설정하는 변수
    int radius; //   반지름을 입력 받을 변수
    int count=0; // 넓이가 100보다 큰 원의 갯수를 세는 변수
    
    
    cout<<"원은 개수 >>";
    cin>>createCircle;
    
    
    Circle *circleArray = new Circle[createCircle];     // Circle 객체 배열 동적 생성, default 생성자 호출

    Circle *p= circleArray;      // 포인터 p에 배열의 주소값 설정
    

    for(int i=0; i<createCircle; i++) {     // 객체 포인터로 배열 접근
        cout<<"원"<<i+1<<"의 반지름>>";
        cin>>radius;
        p->setRadius(radius);
        if(p->getArea() > 100){
            count++;
        }
        p++; // 배열의 다음을 참조하기 위한 증가
    }
    
    cout<<"면적이 100보다 큰 원은 "<<count<<"입니다."<<endl;
    
    delete[] circleArray;  //객체 배열 반환
}

```
