# 10. 클래스

### 클래스 체계

프로그램은 추상화 단계가 순차적으로 내려간다.

변수 목록(정적 공개 상수, 정적 비공개 변수, 비공개 인스턴스 변수, 공개 변수) → 공개 함수    
→ 비공개 함수(자신을 호출하는 공개함수 직후에 위치) 

**캡슐화**
변수와 유틸리티 함수는 최대한 비공개 상태를 유지하는 것이 좋다. 캡슐화를 풀어주는 결정은 언제나 최후의 수단이다.


<br/>

### 클래스는 작아야 한다!

> 단지 클래스를 설계할 때도, 함수와 마찬가지로, ‘작게’가 기본 규칙이라는 의미다.
> 

클래스는 물리적인 행 수로 크기를 측정했던 함수와는 다르게 클래스가 가지는 책임을 센다.

- 클래스 이름은 해당 클래스 책임을 기술해야 한다.
    - 작명은 클래스 크기를 줄이는 첫 번째 관문이다.
    - 클래스 이름이 모호함 = 클래스의 책임이 너무 많음
- 클래스 설명은 if, and, or, but을 사용하지 않고 25단어 내외로 가능해야 한다.
    - 설명에 if, and, or, but가 붙음 = 클래스의 책임이 너무 많음

<br/>

**단일 책임 원칙(SRP)**

* *SRP : 클래스를 변경하는 이유가 단 하나뿐이어야 한다는 원칙*

우리 개발자들은 프로그램이 돌아가면 일이 끝났다고 여긴다. ‘깨끗하고 체계적인 소프트웨어’라는 다음 관심사로 전환하지 않는다. 

> 프로그램으로 되돌아가 **만능 클래스**를 **단일 책임 클래스 여럿으로 분리**하는 대신 다음 문제로 넘어가버린다.
> 

> 큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다. 작은 클래스는 각자 맡은 책임이 하나며, 변경할 이유가 하나며,,,(생략)
> 

<br/>

**응집도** 

메서드가 변수를 많이 사용한다 → 클래스와 메서드는 **응집도**가 높다 → 클래스에 속한 메서드와 변수가 논리적인 단위로 묶인다

> 일반적으로 이처럼 응집도가 가장 높은 클래스는 가능하지도 바람직하지도 않다. 그렇지만 우리는 응집도가 높은 클래스를 선호한다.
> 

<br/>

**응집도를 유지하면 작은 클래스 여럿이 나온다**

큰 함수를 작은 함수 여럿으로 쪼개다 보면 종종 작은 클래스 여럿으로 쪼갤 기회가 생긴다.
(일부 함수가 일부의 변수만을 사용한다 = 클래스의 응집력을 잃는다 → 쪼개라!)

<br/>

**변경하기 쉬운 클래스**

> 깨끗한 시스템은 클래스를 체계적으로 정리해 변경에 수반하는 위험을 낮춘다.
> 

***클래스가 서로 분리되면*** 일부를 수정했다고 해서 위험이 발생하지 않고, 테스트 관점에서도 논리증명이 쉬워진다. 또한 함수(기능) 추가를 할 때에도 기존 클래스를 변경할 필요가 없을 가능성도 크다.

* *OCP(Open-Closed Principle) : 클래스는 확장에 개방적이고 수정에 폐쇠적이어야 한다는 원칙*

**변경으로부터 격리**

객체 지향 프로그램에는 구체적인 클래스와 추상 클래스가 존재한다. 
상세한 구현에 의존하는 클래스는 요구사항이 바뀌면 위험하다. 따라서 우리는 인터페이스와 추상 클래스를 사용함으로써 구현(요구사항)이 바뀌었을 때 미치는 영향을 격리한다.

_* **결합도가 낮다** : 각 시스템 요소가 다른 요소/변경으로부터 잘 격리되어 있다_

결합도를 최소로 줄이면 또 다른 클래스 설계 원칙인 DIP를 따르는 클래스가 나온다.

* *DIP : 클래스가 상세한 구현이 아니라 추상화에 의존해야 한다는 원칙*

<br/>

**참고(SOLID)**

> SOLID란? 로버트 마틴이 명명한 객체 지향 프로그래밍 및 설계의 다섯 가지 기본 원칙

|약자|원칙명|설명|
|---|---|---|
|SRP|**단일 책임 원칙 (Single responsibility principle)** | 한 클래스는 하나의 책임만 가져야 한다.|
|OCP|**개방-폐쇄 원칙 (Open/closed principle)**| 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다. |
|LSP|**리스코프 치환 원칙 (Liskov substitution principle)**| 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다. |
|ISP|**인터페이스 분리 원칙 (Interface segregation principle)**| 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다. |
|DIP|**의존관계 역전 원칙 (Dependency inversion principle)**| 프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다. |
