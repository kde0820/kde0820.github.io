---
layout: post
title: [Effective Java] 2장 객체 생성과 파괴
comments: true
categories: Study
---
# 2장
- 객체를 만들어야 할 때와 만들지 말아야 할 때를 구분하는 법
- 올바른 객체 생성 방법과 불필요한 생성을 피하는 방법
- 제때 파괴됨을 보장하고 파괴 전에 수행해야 할 정리 작업을 관리하는 요령

# 아이템 1. 생성자 대신 정적 팩터리 메서드를 고려하라
- 정적 팩터리 메서드(static factory method): 그 클래스의 인스턴스를 반환하는 단순한 정적 메서드
```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
```
  
## 장점 1 - 이름을 가질 수 있다.
- 생성자에 넘기는 매개변수와 생성자 자체만으로는 반환될 객체의 특성을 제대로 설명하지 못함 but! 정적 팩터리는 이름만 잘 지으면 반환될 객체의 특성을 쉽게 묘사할 수 있음
    - ex) `BigInteager(int, int, Random)` vs `BigInteger.probablePrime`
- 하나의 시그니처로는 생성자를 하나만 만들 수 있음 but! 정적 팩터리는 이러한 제약이 없음

## 장점 2 - 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.