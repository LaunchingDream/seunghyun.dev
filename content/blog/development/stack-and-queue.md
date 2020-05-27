---
title: 스택”과 “우선순위큐를 사용한 데이터처리 콘솔 응용 프로그램
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

* 처음 stack를 초기화 할 때 사용 (stack.Initialize(STUDENT_COUNT);)
* 랜덤 함수 rand를 통해 학생들의 학번, 이름, 성적을 저장할 때 사용 `for(int i=0; i<STUDENT_COUNT; i++) { //생략 }`

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