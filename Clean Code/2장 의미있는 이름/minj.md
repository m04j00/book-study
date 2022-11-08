### 의도를 분명히 밝혀라

- 좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 더 많다.
- 변수의 존재 이유는? 수행 기능은? 사용 방법은? 해당 질문에 모두 답할 수 있어야 한다.

```jsx
public List<int[]> getThem() {
	List<int[]> list1 = new Arraylist<int[]>();
```

- 문제는 코드의 단순성이 아니라 코드의 함축성이다. 코드 맥락이 코드 자체에 명시적으로 드러나지 않는다.
1. theList에 무엇이 들어있는가?
2. theList에서 1번째 값이 어째서 중요한가?
3. 값 4는 무슨 의미인가?
4. 함수가 반환하는 list1을 어떻게 사용하는가?

```jsx
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
		return flaggedCells;
}
```

- 정보 제공은 충분히 가능하다.
- 지뢰 찾기 게임을 만든다고 가정한다면, `theList`가 게임판이라는 사실을 알 수 있다.
- 단순히 이름만 고쳤는데도 함수가 하는 일을 이해하기 쉬워졌다.

### 그릇된 정보를 피하라

- `hp`, `aix`, `sco`는 유닉스 프랫폼이나 유닉스 변종을 가리키는 이름이라 변수 이름으로 적합하지 않다.
- 여러 계정을 그룹으로 묶을 때 실제 `List`가 아니면, `accountList`라 명명하지 않는다. 실제 `List`가 아니면 그릇된 정보를 제공하는 셈이다.
`accountGroup`, `bunchOfAccounts`, `Accounts` 등으로 명명할 수 있다.
- 유사한 개념은 유사한 표기법을 사용한다.

### 의미 있게 구분하라

- 연속된 숫자를 덧붙이거나 불용어를 추가하는 방식은 적절하지 못하다.
- `Product`라는 클래스가 있는데, 다른 클래스를 `ProductInfo` 혹은 `ProductData`라 부른다면 개념을 구분하지 않은 채 이름만 달리한 경우다.
Info나 Data는 a, an, the와 마찬가지로 의미가 불분명한 불용어다.
- 명확한 관례가 없다면 구분이 안되니 읽는 사람이 차이를 알도록 이름을 지어라.
    - moneyAmount - money
    - accountData - account
    - theMessage - message

### 발음하기 쉬운 이름을 사용하라

- 발음하기 어려운 이름은 토론하기도 어렵고 바보처럼 들리기 십상이다.

### 검색하기 쉬운 이름을 사용하라

- `MAX_CLASSES_PER_STUDENT`는 찾기 쉽지만 `7`은 까다롭다. 
`7`이 들어가는 파일 이름이나 수식 모두 검색되기 때문이다.
- 이름 길이는 범위 크기에 비례해야 한다.

### 자신의 기억력을 자랑하지 마라

- 똑똑한 프로그래머는 자신의 정신적 능력을 과시하고 싶어한다. `r`이라는 변수가 소문자 `URL`이라는 사실을 언제나 기억한다면 확실히 똑똑한 사람이다.
- 똑똑한 프로그래머와 전문가 프로그래머 사이에 나타나는 차이점 하나만 들자면, 전문가 프로그래머는 명료함이 최고라는 사실을 이해한다.
- 전문가 프로그래머는 자신의 능력을 좋은 방향으로 사용해 남들이 이해하는 코드를 내놓는다.

### 클래스 이름

- 클래스 이름과 객체 이름은 명사나 명사구가 적합하다.
- Good! - Customer, WikiPage, Account AddressParser
- Bad! - Manager, Processor, Data, Info 등은 피하고 동사는 사용하지 않는다.

### 메소드 이름

- 메소드 이름은 동사나 동사구가 적합하다.
- Good! - postPayment, deletePage, save
- Accessor, Mutator, Predicate는 javabean 표준에 따르면 값 앞에 get, set, is를 붙인다.
- 생성자를 중복정의할 때는 정적 팩토리 메소드를 사용한다.
    
    ```jsx
    Good! - Complex fulcrumPoint = new Complex(23.0);
    bad! - Complex fulcrumPoint = Complex.FromRealNumber(23.0);
    ```
    

### 한 개념에 한 단어를 사용하라

- 메소드 이름은 독자적이고 일관적으로 지어야 주석을 뒤져보지 않고 프로그래머가 올바른 메소드를 선택할 수 있다.
- 동일 코드 기반에 `controller`, `manager`, `driver`를 섞어 사용하면 혼란이 온다. 이름이 다르면 독자는 당연히 클래스도 다르고 타입도 다르다고 생각한다.

### 말장난을 하지 마라

- 한 단어를 두 가지 목적으로 사용하지 않는다.
- 여러 클래스에는 기존 값 두 개를 더하거나 이어서 새로운 값을 만드는 `add` 메소드가 있다. 새로 작성하는 메소드는 집합에 값을 추가하는데 이 메소드를 `add`라 부를 수 있을까? 일관성을 지키기 위해 `add`라 부르기에는 기존 `add` 메소드와 맥락이 다르다. 그러므로 `insert`나 `append`라는 이름으로 지어야 한다.

### 해법 영역에서 가져온 이름을 사용하라

- 전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어를 사용해도 괜찮다.
- 모른 이름을 문제 영역에서 가져오는 정책은 현명하지 못하다.

### 의미 있는 맥락을 추가하라

- 클래스, 함수, 이름 공간에 의미 있는 맥락을 부여한다. 모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다.

```jsx
firstName, lastName, street, houseNumber, city, state, zipcode
-> addrFirstName, addrLastName, addrState
```

### 불필요한 맥락을 없애라

- 고급 휘발유 충전소라는 애플리케이션을 짠다고 가정했을 때 모든 클래스 이름을 `GSD`로 시작한다는 것은 바람직하지 못하다. 
`GSD` 회계 모듈에 `MailingAddress` 클래스를 추가하면서 `GSDAccountAdress`로 이름을 바꿨다. 나중에 다른 고객 관리 프로그램에 고객 주소가 필요해 해당 클래스를 사용하게 된다면, 이름이 적절한가? 이름 17자 중 10자는 중복이거나 부적절하다.
- 일반적으로 긴 이름보다 짧은 이름이 좋다.
- `accountAddress`와 `customerAddress`는 `Address` 클래스 인스턴스로 적합하나 클래스 이름으로는 적합하지 못하다.
