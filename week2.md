1. 93p 13번

₩₩₩
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
₩₩₩
