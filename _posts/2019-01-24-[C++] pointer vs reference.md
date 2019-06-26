---
layout: post
title: '[C++] pointer vs reference'
comments: true
categories: Study
---
pointer와 reference 비교  

## 공통점  
- 다른 변수를 간접적으로 참조한다.

## 차이점  
1. **포인터**는 NULL 값을 가질 수 있지만, **참조자**는 NULL 값을 가질 수 없다.  

```c
int *pNum = NULL; // 통과
int &rNum = NULL; // 에러

int num = 100;
int &rNum = num   // 통과 (참조자는 선언 시  반드시 초기화를 해야한다.)
```
  
- 참조자는 그 대상이 언제나 존재하기 때문에 유효성 검사를 할 필요가 없지만, 포인터는 그 대상이 존재하지 않을 수도 있기때문에 사용전에 언제나 유효성 검사를 해야 한다.
  
```c
string name("daeun");
string *ps = &name;
if(ps) cout << ps;  // 유효성 검사 : ps가 존재하는지 확인 후 사용해야 한다.
```
  
2. **참조자**는 변수를 입력받고, **포인터**는 변수의 주소값을 입력받는다.
  
```c
string name("daeun");
string *pName = &name;
string &rName = name;
```
  
3. **참조자**는 한번 지정한 대상을 변경할 수 없지만, **포인터**는 가능하다.
  
4. 클래스 멤버 접근 시, **참조자**는 '.'을 사용하고 **포인터**는 '->'을 사용한다.
  
```c
class Dog {
    void bark();
}

Dog maltese;

Dog &rDog = maltese;
rDog.bark();       // 참조자에서 bark()함수 호출

Dog *pDog = &maltese;
pDog->Attack();  // 포인터에서 bark()함수 호출

```
