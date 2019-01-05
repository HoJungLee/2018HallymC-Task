1. 교재 639p : 문제 7번

```
[프로그램 소스]
#include <iostream>
#include <fstream>
#include <string>
#include <stack>

using namespace std;



int main(){
    // OS X 환경이라서 C::\\temp\\system.ini 파일도 없고 경로도 없어요
   // /Users/macroom/Desktop/Full2018Cpp/15주차/15주차/week15.ini
    const char* file="/Users/macroom/Desktop/Full2018Cpp/15주차/15주차/week15.ini";
    const char* txt="/Users/macroom/Desktop/Full2018Cpp/15주차/15주차/words.txt";
    
    ifstream fread;
    ofstream fwrite;
    
    // 파일을 반전시키는 방법으로 stack을 사용한다.
    stack<char> reverse;
    
    
    fread.open(file,ios::in|ios::binary);
    if(!fread){
        cout<<"파일 열기 오류";
        return 0;
    }
    
    fwrite.open(txt,ios::out|ios::binary);
    if(!fread){
        cout<<"txt 열기 오류";
        return 0;
    }
    
    char buf[1];
    
    // 한 바이트씩 읽어 스텍에 저장한다.
    while(!fread.eof()){
        fread.read(buf,1);
        reverse.push(buf[0]);
    }
    
    // 한바이트씩 스텍에서 꺼내 파일에 쓴다.
    while (!reverse.empty()) {
        buf[0]=reverse.top();
        fwrite.write(buf, 1);
        reverse.pop();
    }
    
    
    fread.close();
    fwrite.close();
    
    cout<<"복사 완료"<<endl;
    
    return 0;
}

```
<br>
2. 교재 641p : 문제 13번

```
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
using namespace std;

void fileRead(vector<string> &v, ifstream &fin) { // fin 스트림으로부터 벡터 v에 읽어들임
    string line;
    while(getline(fin, line)) { // fin 파일에서 한 라인 읽기
        v.push_back(line); // 읽은 라인을 벡터에 저장
    }
}

void search(vector<string> &v, string word) { // 벡터 v에서 word를 찾아 출력
    bool flag=true; // 단어를 찾지 못했을 경우를 표시 찾지 못하면 true 찾으면 false
    for(int i=0; i<v.size(); i++) {
        int index = v[i].find(word);
        if(index != -1){ // found
            cout << v[i] << endl;
            flag=false;
        }
    }
      // 단어를 못 찾았을 경우
    if(flag){
        cout<<"발견할 수 없음"<<endl;
    }
}

int main() {
    vector<string> wordVector;
    ifstream fin("words.txt");// 열기
    
    // 열기 오류
    if(!fin) {
        cout << "words.txt 파일을 열 수 없습니다." << endl;
        return 0;
    }
    fileRead(wordVector, fin); // fin 스트림으로부터 wordVector에 라인 별로 읽기
    fin.close();
    
    cout << "... words.txt 파일로딩 완료\n검색을 시작합니다. 단어를 입력해 주세요." << endl;
    while(true) {
        cout << "단어 >>";
        string word;
        getline(cin, word); // 키보드로부터 문자열 읽기
        if(word == "exit")
            break; // 프로그램 종료
    
    search(wordVector, word); // 문자열을 words.txt에서 검색하여 출력

    }
    cout << "프로그램을 종료합니다." << endl;

```
