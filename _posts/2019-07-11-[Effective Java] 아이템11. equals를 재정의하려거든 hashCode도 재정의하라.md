---
layout: post
title: "[Effective Java] 아이템11. equals를 재정의하려거든 hashCode도 재정의하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리  

**equals를 재정의한 클래스 모두에서 hashCode도 재정의 해야한다.**  
그렇지 않으면 해당 인스턴스를 HashMap이나 HashSet과 같은 컬렉션의 원소로 사용할 때 문제를 일으킬 것이다.

# hashCode 규약
- equals 비교에 사용되는 정보가 변경되지 않았다면, 애플리케이션이 실행되는 동안 그 객체의 hashCode 메서드는 몇 번을 호출해도 일관되게 항상 같은 값을 반환해야한다.   
(단, 애플리케이션을 다시 실행한다면 이 값이 달라져도 상관없음)
- equals가 두 객체를 같다고 판단했다면, 두 객체의 hashCode는 똑같은 값을 반환해야한다.
- equals가 두 객체를 다르다고 판단했더라도, 두 객체의 hashCode가 서로 다른 값을 반환할 필요는 없다.  
(단, 다른 객체에 대해서는 다른 값을 반환해야 해시테이블의 성능이 좋아진다.)

# hashCode를 재정의 하지 않은 경우
- 크게 문제가 되는 조항은 두 번째이다.

```java
Map<PhoneNumber, String> m = new HashMap<>();
m.put(new PhoneNumber(707, 867, 5309), "제니");
System.out.println(m.get(new PhoneNumber(707, 867, 5309))); // null
```
- 두번째 줄과 세번째 줄의 `new PhoneNumber(707, 867, 5309)`로 생성된 객체는 논리적으로 같은 객체이므로 같은 해시코드를 반환해야 하지만 hashCode를 재정의하지 않아서 올바른 결과를 얻어내지 못한다.

# 좋은 hashCode 작성
```java
   @Override
   public int hashCode() {
        // 1. int result를 선언한 후 해당 객체의 첫번째 핵심 필드의 해시코드로 초기화한다.
        int result = Short.hashCode(areaCode);

        // 2. 해당 객체의 나머지 핵심 필드 각각에 대해 해당 필드의 해시코드 c를 계산하고;
        // result = 31 * result + c 로 갱신한다.
        
        // 2.1 기본 타입 필드라면, Type.hashcode(f) 수행
        result = 31 * result + Short.hashCode(prefix);
        result = 31 * result + Short.hashCode(lineNum);

        // 2.2 참조 타입 필드라면, 해당 필드의 hashCode를 호출한다.
        // 값이 null이면 0을 사용한다.
        result = 31 * result + reference == null ? 0 : reference.hashCode();

        // 2.3 필드가 배열이라면, 핵심 원소 각각을 별도 필드처럼 다룬다.
        // 모든 원소가 핵심 원소라면 Arrays.hashCode를 사용한다.
        result = 31 * result + Arrays.hashCode(arr);

        // 3. 계산된 결과를 리턴한다.
        return result;
   }
```
- 해당 객체의 핵심 필드(equals 비교에 사용되는 필드)들을 사용하여 해시코드를 계산한다.
- 파생 필드(다른 필드로부터 계산해낼 수 있는 필드)는 제외해도 된다.
- equals 비교에 사용되지 않은 필드는 반드시 제외해야 한다.
- `31 * result`는 필드를 곱하는 순서에 따라 result 값이 달라지게 한다. 곱할 숫자를 31로 정한 이유는 홀수이면서 소수이기 때문이다.
