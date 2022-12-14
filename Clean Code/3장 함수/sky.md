# 03. 함수
<br/>

### 작게 만들어라

> 지금까지 경험을 바탕으로 그리고 오랜 시행착오를 바탕으로 나는 작은 함수가 좋다고 확신한다. (생략) 이 말은 중첩 구조가 생길만큼 함수가 커져서는 안 된다는 뜻이다. 그러므로 함수에서 들여쓰기 수준은 1단이나 2단을 넘어서면 안 된다. 당연한 말이지만, 그래야 함수는 읽고 이해하기 쉬워진다.
> 

<br/>

### 한 가지만 해라!

함수가 ‘한 가지’만 하는지 판단하는 방법

- 지정된 함수 이름 아래에서 추상화 수준이 하나인 단계만 수행하는지 확인한다.
- 단순히 다른 표현이 아닌 의미 있는 이름으로 다른 함수를 추출할 수 있는지 확인한다.

> 한 함수 내에 추상화 수준을 섞으면 코드를 읽는 사람이 헷갈린다. 특정 표현이 근본 개념인지 아니면 세부사항인지 구분하기 어려운 탓이다.

**내려가기 규칙 ;** 위에서 아래로 프로그램을 읽으면 함수 추상화 수준이 한번에 한 단계씩 낮아지는 것
>

<br/>

### 서술적인 이름을 사용하라!

> 좋은 이름이 주는 가치는 아무리 강조해도 지나치지 않다. (생략) 한 가지만 하는 작은 함수에 좋은 이름을 붙인다면 이런 원칙을 달성함에 있어 이미 절반은 성공했다.
> 

우리는 변수, 함수, 클래스의 이름이 길어질수록 무서워한다. 하지만 필자는 길고 서술적인 이름이 짧고 어려운 이름 / 길고 서술적인 주석보다 좋다고 언급하였다. 

> 이름을 붙일 때는 일관성이 있어야 한다. 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용한다.
> 

예시 → `includeSetupAndTeardownPages`, `incloudSetupPages`

<br/>

### 함수 인수

> 함수에서 이상적인 인수 개수는 0개(무항)다. 다음은 1개(단항)고, 다음은 2개(이항)다. 3개(삼항)은 가능한 피하는 편이 좋다.
> 

**많이 쓰는 단항 형식**

- 인수에 질문을 던지는 경우 : boolean fileExists(”MyFile”)
- 인수를 뭔가로 변환해 결과를 반환하는 경우
- 이벤트 ; 함수 호출을 이벤트로 해석해 입력 인수로 시스템 상태를 바꾸는 경우

**플래그 인수**

> 플래그 인수는 추하다. 함수로 부울 값을 넘기는 관례는 정말로 끔찍하다.
> 

`render(boolean isSuite)`보다는 `renderForSuite(), renderForSingleTest()`로 구분지어 사용하자.

**이항 함수**

> 인수가 2개인 함수는 인수가 1개인 함수보다 이해하기 어렵다.
> 

인수가 2개인 함수와 1개인 함수를 비교했을 때, 두 함수 모두 의미가 명백할 수는 있어도 일부 함수의 경우 인수가 2개일 때 첫번째 인수를 무시해야 하는 경우가 생긴다. (outputStream을 그 예로 들 수 있다.) 그러나 어떤 코드든 무시한다면 그 코드에 오류가 숨어든다.

**삼항 함수**

> 인수가 3개인 함수는 인수가 2개인 함수보다 훨씬 더 이해하기 어렵다.
> 

순서, 주춤, 무시로 야기되는 문제가 두 배 이상 늘어나므로 삼항 함수를 만들 때에는 신중히 고려해야 한다.

**인수 객체**

> 인수가 2-3개 필요하다면 일부를 독자적인 클래스로 선언할 가능성을 짚어 본다.
> 

그 예시로 `x,y,radius`라는 3개의 인수를 Point객체를 사용하여 `point, radius`로 표현할 수 있다.

**인수 목록**

> 때로는 인수 개수가 가변적인 함수도 필요하다.
> 

`String.format` 메서드처럼 가변 인수 전부를 동등하게 취급하면 List형 인수 하나로 취급할 수 있게 된다.

**동사와 키워드**

> 단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야 한다.
> 

함수 이름에 키워드(인수 이름)를 추가함으로써 인수 순서를 기억할 필요가 없도록 구성할 수 있다. → `assertExpectedEqualsActual(expected, actual)`

<br/>

### 부수 효과를 일으키지 마라!

> 함수에서 한 가지를 하겠다고 약속하고선 남몰래 다른 짓도 하니까. 때로는 예상치 못하게 클래스 변수를 수정한다. 때로는 함수로 넘어온 인수나 시스템 전역 변수를 수정한다. 어느 쪽이든 교활하고 해로운 거짓말이다. 많은 경우 시간적인 결합이나 순서 종속성을 초래한다.
> 

필자는 `checkPassword` 라는 함수 내에서 `Session.initialize()` 를 호출하는 경우를 예시로 들고 있다. 이름만 봐서는 세션을 초기화한다는 것을 알 수 없기에 이러한 경우 시간적인 결합을 초래한다고 언급한다. 

<br/>

**출력 인수**

> 일반적으로 출력 인수는 피해야 한다. 함수에서 상태를 변경해야 한다면 함수가 속한 객체 상태를 변경하는 방식을 택한다.
> 

<br/>

**명령과 조회를 분리하라!**

함수는 객체 상태를 변경하거나 객체 정보를 반환하는 것 두 중 하나만 기능해야한다.

`if(set(”username”.”unclebob”) …`

<br/>

**오류 코드보다 예외를 사용하라!**

명령 함수에서 오류 코드를 반환할 경우 if문에서 명령을 표현식으로 사용하게 될 수 있다. 오류 코드 대신 예외를 사용하면 오류 처리 코드가 원래 코드에서 분리되므로 코드가 깔끔해진다.

<br/>

**오류 처리도 한 가지 작업이다**

- 함수는 ‘한 가지’ 작업만 해야 한다.

> 오류 처리도 ‘한 가지’작업에 속한다. 그러므로 오류를 처리하는 함수는 오류만 처리해야 마땅하다.
> 

<br/>

**반복하지 마라!**

> 어쩌면 중복은 소프트웨어에서 모든 악의 근원이다. 많은 원칙과 기법이 중복을 없에거나 제어할 목적으로 나왔다.
> 

<br/>

**구조적 프로그래밍**

> 구조적 프로그래밍의 목표와 규율은 공감하지만 함수가 작다면 위 규칙은 별 이익을 제공하지 못한다. 함수가 아주 클 때만 상당한 이익을 제공한다.
> 

`에츠허르 데이크스트라`의 구조적 프로그래밍은 루프 안에서 `break`나 `continue`를 사용해서는 안 되며 goto는 절대로 허용하지 않는다는 원칙이 있다. 하지만 작은 함수의 경우 간혹 위의 제어문을 사용해도 괜찮다.

<br/>

**함수를 어떻게 짜죠?**

> 내가 함수를 짤 때도 마찬가지다. 처음에는 길고 복잡하다. 들여쓰기 단계도 많고 중복된 루프도 많다. (생략) 하지만 나는 그 서투른 코드를 빠짐없이 테스트하는 단위 테스트 케이스도 만든다. 그런 다음 나는 코드를 다듬고, 함수를 만들고, 이름을 바꾸고, 중복을 제거한다.



### 느낀점
> 대가 프로그래머는 시스템을 (구현할)프로그램이 아니라 (풀어갈)이야기로 여긴다.

프로그램을 하나의 풀어나갈 이야기처럼 다루는 것이 새로웠다. 나의 프로그램은 항상 특정 기능을 구현해내기 위해 존재했고, 책에서 강조하고 있는 '오류 처리', '명령과 조회의 분리', '부수 효과'에 대해서는 깊이 고려해본 적이 없었다. 하나의 이야기를 쓰듯이 프로그램도 처음에는 내용이 길고 복잡해도 요약하고 다시 써보면서 `읽기 쉽고 고치기 쉬운`코드로 만들어나가는 과정이 가장 어렵고, 중요한 점인 것 같다.

