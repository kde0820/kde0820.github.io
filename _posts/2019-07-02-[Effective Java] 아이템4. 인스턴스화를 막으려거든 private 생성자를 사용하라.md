---
layout: post
title: "[Effective Java] 아이템4. 인스턴스화를 막으려거든 private 생성자를 사용하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리  

단순히 정적 메서드와 정적 필드 만을 담은 클래스를 만들고 싶을 때가 있다.  
  
정적 멤버만을 담은 유틸리티 클래스는 인스턴스로 만들어 쓰려고 설계한 것이 아니다.  
하지만 생성자를 명시하지 않으면 컴파일러가 자동으로 기본 생성자를 만들어 주기 때문에 인스턴스화를 막으려면 **private 생성자**를 사용해야 한다.
  
```java
public class UtilityClass {
    private UtilityClass() {
        throw new AssertionError(); // 실수라도 생성자를 호출하지 않도록 해줌
    }
}
```