1. 교재 528p : 문제 10번

```
[프로그램 소스]
// 10번 문제
#include <iostream>
#include <string>
#include <vector>
#include <ctime>

using namespace std;

// 나라이름과 수도를 저장하는 클래스
class Nation{
    string nation;
    string capital;
public:
    // 생성자
    Nation(string nation="Nation",string capital="Capital"){this->capital=capital;this->nation=nation;}
    
    
    // set
    void setNation(string nation,string capital){
        this->nation=nation;
        this->capital=capital;
    }
    
  // == 연산자 재정의를 통헤 class 정보 가 일치하는 지 확인
    bool operator == (const Nation &p){
        bool con=false;
        
        if(p.capital == this->capital || p.nation == this->nation){
            con=true;
        }
        
        return con;
    }
    
    // 나라 정보를 반환
    string getNation(){
        return this->nation;
    }
    
    // 수도 정보를 반환
    string getCapital(){
        return this->capital;
    }
};


// vector에 새로운 nation클래스를 저장한다.
void insert(vector<Nation> &v , Nation &temp){
  
    // vector에 일치하는 정보가 있는지 확인한다.
    bool con=true;
    for(int i=0; i<v.size(); i++){
        if( v[i].operator==(temp)){
            con=false;
            break;
        }
    }
    
    // 일치하는 객체가 없다면 저장
    if(con)
        v.push_back(temp);
    else
        cout<<"already exits !!\n";
    
}


int main() {
    // 나라의 수도 9개 입력
    vector<Nation> v={Nation("Korea","Seoul"),Nation("Japan","Tokyo"),Nation("UK","London"),Nation("France","Paris"),
        Nation("China","Beijing"),Nation("USA","Washinton"),Nation("Germany","Berlin"),
        Nation("Italy","Rome"),Nation("Spain","Madrid")};
   
    // 랜덤 넘버 설정
   srand( (unsigned int) time(0));
    
    
    int chioce=0;
    string nation;
    string capital;
    int random;
    
    
    // 반복문을 통하여 메뉴 실행
    // 3이 입력 될 경우 종료
    while(chioce!=3){
        cout<<v.size()<<"개의 나라가 입력되어 있습니다.\n";
        cout<<"정보 입력: 1, 퀴즈: 2, 종료: 3 >>";
        cin>>chioce;
        
        switch (chioce) {
            case 1:
                while(true){
                    cout<<v.size()+1<<">>";
                    cin>>nation>>capital;
                    if(nation=="no" && capital=="no")
                        break;
                
                    Nation temp(nation,capital);
                    insert(v, temp);
                   
                }
                break;
            case 2:
                while (true) {
                    random=rand()%v.size();
                    cout<<v.at(random).getNation()<<"의 수도는?";
                    cin>>capital;
                    
                    if(capital=="exit")
                        break;
                    
                    if(capital == v.at(random).getCapital()){
                        cout<<"Correct !!\n";
                    }else{
                        cout<<"No !!\n";
                    }
                    
                }
                break;
            
            default:
                break;
             
        }
      
    }
    
    return 0;
}

```

<br>
2. 교재 530p : 문제 14번

```
#include <iostream>
#include <string>
#include <map>
using namespace std;


//  삽입
void insert(map<string,string> &key){
    string name,pw;
    
    cout<<"이름 암호>>";
    cin>>name>>pw;
    
    
    if( key.find(name) == key.end() ){
        key[name]=pw;
    }else{
        cout<< " 키 값이 중복됩니다.\n";
    }

}

// 검사
void find( map<string,string> &key){
    string name,pw;
    
    while(1){
        cout<<"이름 ? ";
        cin>>name;
        if(  key.find(name) == key.end() ){
            cout<< " 키 값이 없습니다..\n";
            continue;
        }else{
            break;
        }
    }
    cin.clear();
    while(1){
        cout<<"암호 ? ";
        
        cin>>pw;
    
        if( key[name] == pw ){
            cout<< "통과!!\n";
            break;
        }else{
            cout<< " 실패~~\n";
            continue;
        }
    }
}


int main(){
    map<string,string> keyCode;
    int choice;
    // 무한 반복문을 통하여 메뉴 실행
    cout<< "****** 암호 관리 프로그램 WHO를 실행합니다 ******\n";
    while(1){
        cout<< "삽입: 1 ,검사 : 2 ,종료: 3>>";
        cin>>choice;
        
        switch (choice) {
            case 1:
                insert(keyCode);
                break;
            case 2:
                find(keyCode);
                break;
        }
        
        if(choice==3){
            cout<<"프로그램을 종료합니다... \n";
            break;
        }
        cin.clear();
        
    }
    
    
    return 0;
}

```
