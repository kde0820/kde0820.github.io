---
layout: post
title: "[Effective Java] 아이템5. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리 

클래스가 내부적으로 하나 이상의 자원에 의존하고, 그 자원이 클래스 동작에 영향을 준다면 싱글턴과 정적 유틸리티 클래스는 사용하지 않는 것이 좋다.  
클래스가 여러 자원 인스턴스를 지원해야 하며, 클라이언트가 원하는 자원을 사용해야 한다.  
이 조건을 만족한 방법은 **인스턴스를 생성할 때 생성자에 필요한 자원을 넘겨주는 것**이다.

# 의존 객체 주입
- 인스턴스를 생성할 때 생성자에 필요한 자원을 넘겨주는 방식
- 자원이 몇 개든 의존 관계가 어떻든 상관없이 잘 작동함
- 불변을 보장하여 여러 클라이언트가 의존 객체들을 안심하고 공유할 수 있음

## 팩터리 메서드 패턴을 사용하여 자원 팩터리 넘겨주기
- 팩터리: 호출할 때마다 특정 타입의 인스턴스를 반복해서 만들어주는 객체
- ex) 자바 8에서 소개한 `Supplier<T>`인터페이스
- `Supplier<T>`를 입력으로 받는 메서드는 일반적으로 한정적 와일드카드 타입을 사용해 팩터리의 타입 매개변수를 제한함
- 이 방식을 사용하면 클아이언트는 자신이 명시한 타입의 하위 타입이라면 무엇이든 생성할 수 있는 팩터리를 넘길 수 있음
```java
Mosaic create(Supplier<? extends Tile> tile Factory) { ... } 
```

## Supplier<T>
- 인자는 받지 않으며 리턴값만 존재하는 메서드를 갖고 있음  
- 이 메서드들을 실행하면 호출한 곳으로 데이터를 공급하는 역할을 함
- 참고: [Java 8 docs](https://docs.oracle.com/javase/8/docs/api/java/util/function/Supplier.html)
```java
Supplier<String> s = () -> "Hello, World!";
String result = s.get();
```