---
title: 스택과 우선순위큐를 사용한 데이터처리 콘솔 응용 프로그램
date: 2014-03-31 13:00:00
category: development
thumbnail: './images/custom-range-bar/custom-range-bar.png'
draft: false
---

## 1. 기본 학생 데이터

학생의 정보를 저장하는 구조체 Student이다. 총 3개의 필드를 가지고 있다. 학생의 성적에 해당하는 실수 float형 Score, 학생의 학번의 정수 int형 Number, 학생의 성적의 문자열 string형 Name 변수이다. 

```C
typedef struct {
  float Score;
  int Number;
  string Name;
} Student;
```
학생의 수를 저장하는 정수형 전역 변수이다. 사용자의 키 입력을 통해 학생의 수를 변경할 수 있다. 다양한 반복문, 함수 등에서 사용되게 된다.

```C
int STUDENT_COUNT = 6;
```

* 처음 stack를 초기화 할 때 사용 → `(stack.Initialize(STUDENT_COUNT);)`
* 랜덤 함수 rand를 통해 학생들의 학번, 이름, 성적을 저장할 때 사용 → `for(int i=0; i<STUDENT_COUNT; i++) { //생략 }`

```C
string names[17]= {"유승현", //생략 };
```

학생의 이름들 17명을 미리 입력했다. 랜덤함수 rand를 통해 학생의 이름을 지정된다.

```C
srand(time(NULL));
for (int i = 0; i < STUDENT_COUNT; i++) {
  Student temp; // 임시 Student 구조체 temp
  temp.Number = ((rand() % 14 + 2001) * 100) + rand() % 100; // 학번
  temp.Name = names[rand() % 16]; // 이름
  temp.Score = (rand() % 10001) / 100.0; // 성적
  stack.Push(temp); // stack에 temp를 push
}
```

Main 함수에서 학생의 학번, 이름, 성적을 랜덤 함수 rand를 통해 저장한다. 학번(Number)은 임의의 양의 정수로 했고, 성명은 이미 지정해둔 names 배열의 인덱스를 무작위로 저장하고, 성적은 0에서 100 사이의 실수로 저장했다.

## 2. Class staack
```C
class Stack {
  public:
    int m_size; // Stack의 사이즈 지정
    int m_top; // Stack의 현재 높이
  
    // students Student 구조체의 Vector
    // 주로 students[m_top]를 사용
    vector < Student > students;
    void Initialize(int size = 6); // Stack 클래스의 초기화
    void RemoveAll(); // Stack 모든 내용 클리어, 과제에서는 사용 안함
    void Push(Student temp); // Stack의 Push에 해당하는 함수
    Student Pop(void); // Stack의 Pop에 해당하는 함수
};
```
자체적으로 만든 `Stack` 이라는 이름의 클래스이다.

* 멤버 변수는 2개이다. 스택의 사이즈를 나타내는 int형 변수 `m_size` , 스택의 현재 높이를 나타내는 int형 변수 `m_top` 이다.
* 멤버 함수는 4개이다. 스택의 클래스를 초기화하는 함수 `Initialize`, 현재 프로그램에서는 사용 안했지만 스택의 모든 내용을 지우는 함수 `RemoveAll`, 스택의 Push에 해당하는 함수 `Push`, 스택의 Pop에 해당하는 함수 `Pop`가 있다.

```C
void Stack::Initialize(int size) {
  m_size = size;
  m_top = -1;
  students.clear();
}
```
### 스택의 함수 1) Initialize
* 우선 매개변수 int형 변수를 입력 받아 스택의 사이즈를 지정한다.
* 스택의 현재 높이를 –1로 초기화하고, 벡터 Students의 데이터를 모두 지운다.
* 반환 값은 없다

```C
void Stack::RemoveAll() {
  m_top = -1;
  students.clear();
}
```
### 스택의 함수 2) RemoveAll
* 스택의 현재 높이(m_top)를 –1로 초기화하여 데이터가 아무것도 없음을 표현한다.
* 학생들의 구조체 벡터를 초기화한다. 이 때 벡터의 기본 함수 clear() 사용한다.
* 반환 값은 없다.

```C
void Stack::Push(Student temp) {
  ++m_top;
  students.push_back(temp);
}
```
### 스택의 함수 3) Push
* 매개 변수는 Student 구조체(temp)이고 반환 값은 없다.
* Push가 실행되면 우선 m_top의 높이를 하나 증가한다.
* temp를 벡터함수 push_back 사용하여 학생 벡터 students에 넣는다.

```C
Student Stack::Pop(void) {
  if (!(m_top < 0)) { // Pop이 실행이 되면 우선 m_top이 음수가 아닌지를 체크
    return students[m_top--]; // Pop 함수의 반환 값으로 Student 벡터를 이용해
    Student 구조체를 출력
  }
}
```
### 스택의 함수 4) Pop
* 매개 변수는 없고, 반환 값으로 구조체 Student를 반환한다.
* Pop이 실행되면 현재 스택의 높이(m_top)를 체크하고 현재 높이의 벡터의 구조체를 반환한다.

---

## 3. 다양한 함수
```C
void PrintStudent(Stack stack);
void SaveStudentTxt(Stack stack);
void LoadStudentTxt();
void PrintPriorityQueue();
```
class Stack에 있는 함수 외에도 다양한 함수들이 있다.
* `PrintStudent` - Stack에 저장된 학생들의 정보를 스크린에 출력해주는 함수
* `LoadStudentTxt` - Stack의 학생들의 정보를 텍스트 파일로 저장(data.txt)해주는 함수
* `LoadStudentTxt` - 텍스트 파일를 통해 학생의 정보를 불러와 pqueue에 push해주는 함수
* `PrintPriorityQueue` - 학생들의 정보가 정렬된 pqueue(priority_queue) 출력해주는 함수

```C
void PrintStudent(Stack stack) {
  // PrintStudent 함수가 잘 실행되었다는 출력문은 여기서 생략
  for (int i = stack.m_top; i >= 0; i--) {
    cout << "이름: \t" << stack.students[i].Name << "\t\t";
    cout << "학번: \t" << stack.students[i].Number << "\t\t";
    cout << "성적: \t" << stack.students[i].Score << endl;
  }
  cout << endl;
}
```

### 1) `PrintStudent` - 현재 Stack에 존재하는 학생들의 정보를 출력하는 함수
* stack의 m_top 변수의 크기를 하나씩 줄이면서 stack 안에 있는 벡터 students의 학생의 이름, 학번, 성적을 출력한다.

```C
void SaveStudentTxt(Stack stack) {
  ofstream fout;
  fout.open("data.txt");
  Student temp; // 임시 Student 구조체 temp 선언
  int count = 0; // 몇 명의 학생이 text 파일에 저장됬는지 카운트
  for (int i = stack.m_top; i >= 0; i--) {
    temp = stack.Pop(); // stack의 pop함수의 리턴값을 student 구조체 temp에 저장
    fout << temp.Score << endl; // 학생의 성적
    fout << temp.Number << endl; // 학생의 학번
    fout << temp.Name; // 학생의 이름
    if (i != 0) // 마지막 element는 공백라인 넣지 않음
      fout << endl; //공백라인
    count++; // 텍스트 파일에 저장될 때 마다 count 변수 1씩 증가
  }
  fout.close();
  // 몇 명의 데이터가 data.txt에 저장 되었는지 알리는 출력문은 생략
}
```

### 2) `SaveStudentTxt` - Stack에 존재하는 학생들의 정보를 텍스트 파일로 저장
* 스택의 데이터를 하나씩 pop하며 꺼내서 파일에 저장한다.
* 스택의 pop해서 나오는 값은 Student 구조체이다.
* ofstream 클래스로 객체(fout)를 선언한다.
* fout open() 메소드를 사용하여 출력하길 원하는 파일명(data.txt)를 지정한다.
* 스트림 객체를 사용하여 출력한다. fout << ... << endl;
* 오픈 파일을 닫는다. (fout.close())

---
문서 작성 중입니다.
