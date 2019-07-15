---
layout: post
title: "[Effective Java] 아이템12. toString을 항상 재정의하라"
comments: true
categories: Study
---
Effective Java 3판을 공부하며 배운 내용 정리  

- toString을 재정의하지 않으면 단순히 `클래스 이름@해시코드`를 반환

- toString은 **간결하면서 사람이 읽기 쉬운 형태의 유익한 정보**를 반환해야 한다.

- 모든 하위 클래스에서 toString 메서드를 재정의 해야 한다.

- toString을 잘 구현하면 디버깅하기 쉽다.

- toString은 그 객체가 가진 주요 정보 모두를 반환하는 게 좋다.

- toString을 구현할 때면 반환값의 포맷을 문서화할지 정해야 한다.
    - 포맷을 명시하면 그 객체는 표준적이고, 명확하고, 사람이 읽을 수 있게 된다.
    - 단점: 포맷을 한번 명시하면 평생 그 포맷에 얽매이게 된다.

- 포맷을 명시하든 아니든 개발자의 의도는 명확히 밝혀야 한다.

- toString이 반환한 값에 포함된 정보를 얻어올 수 있는 API를 제공해야 한다.
    - toString이 반환한 값들에 접근을 하지 못한다면, 해당 값들을 사용하기 위해서 toString을 파싱할 수 밖에 없다.