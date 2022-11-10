# 3. 함수

### 작게 만들어라

1. 블록과 들여쓰기
    - if / else / while 문 등에 들어가는 블록은 한 줄이어야 한다.
    - 바깥을 감싸는 함수가 작아질 뿐 아니라 블록 안에서 함수 이름을 적절히 지으면 코드를 이해하기도 쉽다.

### 한 가지만 해라

> 함수는 한 가지를 해야 한다. 그 한 가지를 잘 해야 한다. 그 한 가지만을 해야 한다.
> 

```java
public static String renderPageWithSetupAndTeardowns(
	PageData pagedata, boolean isSuite) throws Exception {
		if (isTestPage(pageData))
			includeSetupAndTeardownPages(pageData, isSuite);
		return pageData.getHtml();
}
```

- 위 함수는 한 가지만 하는가?
    1. 페이지가 테스트 페이지인지 판단한다.
    2. 그렇다면 설정 페이지와 해제 페이지를 넣는다.
    3. 페이지를 HTML로 렌더링한다.
- 위에서 언급하는 세 단계는 지정된 함수 이름 아래에서 추상화 수준이 하나다.
- 지정된 함수 이름 아래에서 추상화 수준이 하나인 단계만 수행한다면 그 함수는 한 가지 작업만 한다.
- 우리가 함수를 만드는 이유는 큰 개념(함수 이름)을 다음 추상화 수준에서 여러 단계로 나눠 수행하기 위해서다.
- 단순히 다른 표현이 아니라 의미 있는 이름으로 다른 함수를 추출할 수 있다면 그 함수는 여러 작업을 하는 셈이다.

### 함수 당 추상화 수준은 하나로

- 한 함수 내에 추상화 수준을 섞으면 코드를 읽는 사람이 헷갈린다. 특정 표현이 근본 개념인지 세부사항인지 구분하기 어려운 탓이다.
- 내려가기 규칙 - 위에서 아래로 코드 읽기
    - 한 함수 다음에 추상화 수준이 한 단계 낮은 함수가 온다.
    - 위에서 아래로 프로그램을 읽으면 함수 추상화 수준이 한 번에 한 단계식 낮아진다.

### Switch 문

- 본질적으로 switch문은 N가지를 처리하고 작게 만들기 어렵다. 물론 다형성을 이용하여 각 switch문을 저차원 클래스에 숨겨 반복하지 않는 방법도 있다.

```java
public Money CalculatePay(Employee e) throws InvalidEmployeeType {
	switch (e.type) {
		case COMMISSIONED: 
			return calceulateCommissionedPay(e);
		case HOURLY:
			return calculateHourlyPay(e);
		case SALARIED:
			return calculateSalariedPay(e);
	}
}
```

- 위 코드의 문제점
    1. 함수가 길고 새 직원 유형을 추가하면 더 길어진다.
    2. 한 가지 작업만 수행하지 않는다.
    3. 코드를 변경할 이유가 여럿 있어 `SRP`를 위반한다.
    4. 새 직원 유형을 추가할 때마다 코드를 변경해야 해 `OCP`에 위반한다.
- 개선 방법
    - switch문을 추상 팩토리에 꽁꽁 숨긴다.
    - 팩토리는 switch문을 사용해 적절한 `Employee` 파생 클래스의 인스턴스를 생성한다.
    - `calculatePay`, `isPayday` 등과 같은 함수는 `Employee` 인터페이스를 거쳐 호출하면 다형성으로 인해 실제 파생 클래스의 함수가 실행된다.

### 서술적인 이름을 사용하라

- 한 가지만 하는 작은 함수에 좋은 이름을 붙이면 깨끗한 코드 원칙 달성에 절반은 성공한 것이다.
- 길고 서술적인 이름이 짧고 어려운 이름보다 좋고 길고 서술적인 주석보다 좋다.
- 함수 이름을 정할 때는 여러 단어가 쉽게 읽히는 명명법을 사용한다. 그리고 여러 단어를 사용해 함수 기능을 잘 표현하는 이름을 선택한다.
- 이름을 붙일 때는 일관성이 있어야 하고 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용한다.

### 함수 인수

- 함수에서 이상적인 인수 개수는 0개다.
- 테스트 관점에서 보면 인수는 더 어렵다. 갖가지 인수 조합으로 함수를 검증해야 하는 테스트 케이스를 작성해야 한다.

**많이 쓰는 단항 형식**

- 인수에 질문을 던지는 경우 - `boolean fileExists(”MyFile”)`
- 인수를 변환해 결과를 반환하는 경우 - `InputStream fileOpen(”MyFile”)`
String형의 파일 이름을 InputStream으로 변환한다.
- 이벤트 함수는 입력 인수만 있다. - `passwordAttemptFailedNtimes(int attempts)`
이벤트라는 사실이 코드에 명확히 드러나야 해 이름과 문맥을 주의해서 선택한다.

이항 함수

- `writeField(outputStream, name)`
- 인수가 2개인 함수는 인수가 1개인 함수보다 이해하기 어려운데, 위 함수는 첫 인수를 무시해야 한다는 사실을 깨닫는 시간이 필요하다.
- 두 인수의 자연적인 순서가 없어 두 값을 반대로 넣는 실수도 발생한다.
- 위 함수 개선
    - writeField 메소드를 `outputStream` 클래스 구성원으로 만들어 `outputStream.writeField(name)`으로 호출한다.
    - `outputStream`을 현재 클래스 구성원 변수로 만들어 인수로 넘기지 않는다.
    - `FieldWrite`라는 새 클래스를 만들어 구성자에서 `outputStrea m`을 받고 `write` 메소드를 구현한다.

인수 객체

- 인수가 2~3개 필요하다면 일부를 독자적인 클래스 변수로 선언할 가능성을 짚어 본다.

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

- x, y를 변수로 묶어 넘기려면 이름을 붙여야 해 결국은 개념을 표현할 수 있게 된다.

동사와 키워드

- 단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야 한다.
    - `write(name)` - 이름이 무엇이든 쓴다는 의미다.
    - `writeField(name)` - 좀 더 나은 이름으로 이름이 필드라는 사실이 분명히 드러난다.
- 함수 이름에 키워드를 추가하는 형식이 있다.
    - `assertExpectedEqualsActual(expected, actual)` - 인수 순서를 기억할 필요가 없어 `assertEquals`보다 좋다.
