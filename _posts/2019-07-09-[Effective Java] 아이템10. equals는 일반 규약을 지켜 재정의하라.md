---
layout: post
title: "[Effective Java] 아이템10. equals는 일반 규약을 지켜 재정의하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리  

#3장 - 모든 객체의 공통 메서드
- final이 아닌 Object 메서드들을 언제 어떻게 재정의해야 하는지를 다룸
- equals, hashCode, toString, clone, finalize(아이템 8)

# equals를 재정의하지 않는 것이 좋은 경우
- 각 인스턴스가 본질적으로 고유한 경우 - 동작하는 개체를 표현하는 클래스
- 인스턴스의 '논리적 동치성'을 검사할 일이 없는 경우
- 상위 클래스에서 재정의한 equals가 하위 클래스에도 딱 들어 맞는 경우
- 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없는 경우

# equals 메서드를 재정의할 때의 규약


***작성중***