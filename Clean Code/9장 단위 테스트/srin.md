# 9장 단위 테스트

> 애자일과 TDD 덕택에 단위 테스트를 자동화하는 프로그래머들이 이미 많아졌으며 점점 더 늘어나는 추세다. 하지만 우리 분야에 테스트를 추가하려고 급하게 서두르는 와중에 많은 프로그래머들이 제대로 된 테스트 케이스를 작성해야한다는 좀 더 미묘한 (그리고 더욱 중요한) 사실을 놓쳐버렸다.
> 

## TDD 법칙 세 가지

- 첫째 법칙, 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
- 둘째 법칙, 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
- 셋째 법칙, 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

> 이렇게 일하면 매일 수십 개, 매달 수백 개, 매년 수천 개에 달하는 테스트 케이스가 나온다. 이렇게 일하면 실제 코드를 사실상 전부 테스트하는 테스트 케이스가 나온다. 하지만 실제 코드와 맞먹을 정도로 방대한 테스트 코드는 심각한 관리 문제를 유발하기도 한다.
> 

## 깨끗한 테스트 코드 유지하기

> 하지만 팀은 지저분한 테스트 코드를 내놓으나 테스트를 안 하나 오십보 백보라는, 아니 오히려 더 못하다는 사실을 깨닫지 못했다. 문제는 실제 코드가 진화하면 테스트 코드도 변해야 한다는 데 있다. 그런데 테스트 코드가 지저분할수록 변겨하기 어려워 진다.
> 

> 테스트 코드를 깨끗하게 짰다면 테스트에 쏟아 부은 노력은 허사로 돌아가지 않았을 터이다. 내가 이처럼 어느 정도 자신 있게 말하는 이유는 내가 참여하고 조언한 많은 팀이 깨끗한 단위 테스트 코드로 성공했기 때문이다.
> 

> **테스트 코드는 실제 코드 못지 않게 중요하다.**
> 

<br>

*테스트는 유연성, 유지보수성, 재사용성을 제공한다.*

> 테스트 코드를 깨끗하게 유지하지 않으면 결국은 읽어버린다. 그리고 테스트 케이스가 없으면 실제 코드를 유연하게 만드는 버팀목도 사라진다.
> 

> 코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목이 바로 **단위 테스트**다. 이뉴는 단순하다. 테스트 케이스가 있으면 변경이 두렵지 않으니까!
> 

## 깨끗한 테스트 코드

> 깨끗한 테스트 코드를 만들려면? 세 가지가 필요하다. 가독성, 가독성, 가독성. 어쩌면 가독성은 실제 코드보다 테스트 코드에 더더욱 중요하다.
> 

> 테스트 코드에서 가독성을 높이려면? 여느 코드와 마찬가지다. 명료성, 단순성, 풍부한 표현력이 필요하다. 테스트 코드는 최소의 표현으로 많은 것을 나타내야 한다.
> 

<br>

**[BUILD-OPERATE-CHECK 패턴](http://butunclebob.com/FitNesse.AcceptanceTestPatterns) :** 각 테스트는 명확히 세 부분으로 나눠진다. 첫 부분은 테스트 자료를 만든다.(given) 두 번째 부분은 테스트 자료를 조작하며,(when) 세 번째 부분은 조작한 결과가 올바른지 확인한다.(then)

> 테스트 코드는 본론에 돌입해 진짜 필요한 자료 유형과 함수만 사용한다. 그러므로 코드를 읽는 사람은 온갖 잡다하고 세세한 코드에 주눅들고 헷갈릴 필요 없이 코드가 수행하는 기능을 재빨리 이해한다.
> 

<br>

*[도메인에 특화된 테스트 언어](https://www.jetbrains.com/ko-kr/mps/concepts/domain-specific-languages/)*

> 숙련된 개발자라면 자기 코드를 좀 더 간결하고 표현력이 풍부한 코드로 리팩터링해야 마땅하다.
> 

<br>

*이중 표준*

> 테스트 API 코드에 적용하는 표준은 실제 코드에 적용하는 표준과 확실히 다르다. 단순하고, 간결하고, 표현력이 풍부해야 하지만, 실제 코드만큼 효율적일 필요는 없다.
> 

> 실제 환경에서는 절대로 안 되지만 테스트 환경에서는 전혀 문제없는 방식이 있다. 대개 메모리나 CPU 효율과 관련있는 경우다. 코드의 깨끗함과는 철저히 무관하다.
> 

## 테스트 당 assert 하나

> assert문이 단 하나인 함수는 결론이 하나라서 코드를 이해하기 쉽고 빠르다.
> 

> 불행하게도, 위에서 보듯이, 테스트를 분리하면 중복되는 코드가 많아진다. TEMPLATE METHOD 패턴을 사용하면 중복을 제거할 수 있다.
> 

**TEMPLATE METHOD 패턴 :** given/when 부분을 부모 클래스에 두고, then 부분을 자식 클래스에 두거나
완전히 독자적인 테스트 클래스를 만들어 @Before함수에 given/when 부분을 넣고 각각의 @Test함수에 then에 해당하는 코드를 작성해도 된다. 

> 하지만 때로는 주저 없이 함수 하나에 여러 assert문을 넣기도 한다. 단지 assert문 개수는 최대한 줄여야 좋다는 생각이다.
> 

## 테스트 당 개념 하나

> 새 개념을 한 함수로 몰아넣으면 독자가 각 절이 거기에 존재하는 이유와 각 절이 테스트하는 개념을 모두 이해해야한다.
> 

> 그러므로 가장 좋은 규칙은 “개념 당 assert 문 수를 최소로 줄여라”와 “테스트 함수 하나는 개념 하나만 테스트하라”라 하겠다.
> 

## F.I.R.S.T.

> 깨끗한 테스트는 다음 다섯가지 규칙을 따르는데 각 규칙에서 첫 글자를 따오면 FIRST가 된다.
> 

**Fast(빠르게)**

- 테스트는 빨리 돌아야 한다. 테스트가 느리면 자주 돌릴 엄두를 못낸다.

**Independent(독립적으로)**

- 각 테스트는 서로 의존하면 안된다. 한 테스트가 다음 테스트가 실행될 환경을 준비해서는 안된다.
- 테스트가 서로에게 의존하면 하나가 실패할때 나머지도 잇달아 실패하므로 원인을 진단하기 어려워지며 후반 테스트가 찾아내야 할 결함이 숨겨진다.

**Repeatable(반복가능하게)**

- 테스트는 어떤 환경에서도 반복 가능해야 한다.
- 테스트가 돌아가지 않는 환경이 하나라도 있다면 테스트가 실패한 이유를 둘러댈 변명이 생긴다. 게다가 환경이 지원되지 않기에 테스트를 수행하지 못하는 상황에 직면한다.

**Self-Validating(자가 검증하는)**

- 테스트는 bool값으로 결과를 내야 한다. 성공 아니면 실패다. 통과 여부를 알려고 로그 파일을 읽게 만들어서는 안된다.
- 테스트가 스스로 성공과 실패를 가늠하지 않는다면 판단은 주관적이 되며 지루한 수작업 평가가 필요하게 된다.

**Timely(적시에)**

- 테스트는 적시에 작성해야 한다. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다.

## 결론

> 테스트 코드는 실제 코드의 유연성, 유지보수성, 재사용성을 보존하고 강화하기 때문이다. 그러므로 테스트 코드는 지속적으로 깨끗하게 관리하자. 표현력을 높이고 간결하게 정리하자
> 

## 느낀점

 클린코드 읽기 스터디를 진행하며 가장 기대했던 주제인 단위 테스트에 대해 알아보았다. 회사에서 지금까지의 코드를 정리하며 밀려있던 단위 테스트를 개발하는 업무를 맡았는데, 이전까지 단위 테스트는 내가 짠 CRUD에 대한 작은 메서드 하나씩만을 테스트 하는 것이었지만 회사에서는 이미 개발되어있는 엄청 길고도 긴 메서드를 테스트하려니 어떤것이 좋은 테스트일지에 대해 많은 고민을 하고 있었기 때문이다. 

 이번 주제를 읽는 내내 엄청 찔림의 연속이었다. 특히나 지저분한 테스트 코드를 짜느니 안짜느니만 못하다는 말이 매우 충격으로 다가왔다. 그리고 반성의 시간이었다. 내가 안짜느니만 못한 테스트 코드를 짠건 아닐까? 나도 알아보지 못하는 테스트 코드를 누가 알아보고 수정할까 가독성에 대해 한번이라도 생각하고 테스트코드를 짰나 하는 식의 정말 많은 생각을 하게 되었던것 같다. 결론적으로는.. 지금까지 테스트 코드를 제대로 짜지 못했구나 라는 생각이 들었다. 

 물론 이 주제의 결론에서 말하듯 이것은 수박겉핥기와 같이 단위 테스트에 대해 겉만 훑었지만 **깨끗한 테스트코드**라는 것을 조금은 깨우칠 수 있었던 것 같다.
