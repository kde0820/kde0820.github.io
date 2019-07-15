---
layout: post
title: "[Effective Java] 아이템13. clone 재정의는 주의해서 진행하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리  

Cloneable은 복제해도 되는 클래스임을 명시하는 용도의 믹스인 인터페이스이다.  
하지만 clone 메서드가 선언된 곳이 Object이고 protected이기 때문에 Cloneable을 구현하는 것 만으로는 외부 객체에서 clone 메서드를 호출할 수 없다.

## 믹스인 인터페이스
- 믹스인: 클래스가 자신의 '본래 타입'에 추가하여 구현할 수 있는 타입 --> 클래스가 구현할 수 있는 타입(클래스, 함수, 인터페이스 등)
- 자바에서는 다중 상속에 문제가 없는 인터페이스가 믹스인을 정의하는데 이상적이다.
```java
public class Person implements Comparable<Person> {
    String name;
    int age;
    
    public void printName() {
        System.out.println(String.format("My name is %s!", name));
    }
    
    @Override
    public int compareTo(Person o) {
        return 0;
    }
}
```
- 주된 기능(개인 정보 표시, printName)에 선택적 기능인 Comparable을 추가하였다.

# Cloneable 인터페이스
```java
public interface Cloneable {
}
```
- 아무런 기능이 없다.  
  
```java
protected native Object clone() throws CloneNotSupportedException;
```
- native: 자바가 아닌 언어(보통 C나 C++)로 구현한 후 자바에서 사용하려고 할 때 이용하는 키워드
- protected 메서드


***작성중***