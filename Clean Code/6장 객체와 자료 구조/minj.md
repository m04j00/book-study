# 6. 객체와 자료 구조

### 자료 추상화

```java
// 구체적인 Point class
public class Point {
	public double x;
	public double y;
}

// 추상적인 Point class
public interface Point {
	double getX();
	double getY();
	void setCartesian(double x, double y);
	double getR();
	double getTheta();
	void setPolar(double r, double theta);
}
```

- 변수 사이에 함수라는 계층을 넣는다고 구현이 감춰지지 않는다. **구현을 감추려면 추상화가 필요하다.**
- 조회 함수와 설정 함수로 변수를 다룬다고 클래스가 되지 않는다. **추상 인터페이스를 제공해 사용자가 구현을 모른 채 자료의 핵심을 조작할 수 있어야 진정한 클래스다.**

```java
// 구체적인 Vehicle class
public interface Vehicle {
	double getFuelTankCapacityInGallons();
	double getGallonsOfGasoline();
}

// 추상적인 Vechicle class
public interface Vehicle {
	double getPercentFuelRemaining();
```

- 자료를 세세하게 공개하기 보다는 추상적인 개념으로 표현하는 편이 좋다.
- 인터페이스나 조회/설정 함수만으로는 추상화가 이루어지지 않는다. 객체가 포함하는 자료를 표현할 가장 좋은 방법을 고민해야 한다.

### 자료/객체 비대칭

- 위의 코드는 객체와 자료 구조 사이에 벌어진 차이를 보여준다.
- **객체**는 추상화 뒤로 자료를 숨기고 자료를 다루는 함수만 공개한다.
- **자료 구조**는 자료를 그대로 공개하며 별다른 함수는 제공하지 않는다.

```java
// 6-5 절차적인 도형
public class Square {
	public Point topLeft;
	public double side;
}

public class Geometry {
	public final double PI = 3.14;

	public double area(Object shape) {
		if (shape instanceof Square) {
			Square s (Square)shape;
			return s.side * s.side;
		}
	}
}

// 6-6 다형적인 도형
public class Square implements Shape {
	private Point topLeft;
	private double side;

	public double area() {
		return side*side;
	}
}
```

- 6-5 코드에서 둘레 길이를 구하는 perimeter() 함수를 추가하고 싶을 경우 도형 클래스는 아무 영향도 받지 않는다. 도형 클래스에 의존하는 다른 클래스도 마찬가지다. 
반대로 새 도형을 추가하고 싶다면 Geometry 클래스에 속함 함수를 모두 고쳐야 한다.
- 6-6 코드에서 area()는 다형 메소드다. 따라서 Geometry 클래스가 따로 필요 없다. 그러므로 새 도형을 추가해도 기존 함수에 아무런 영향을 미치지 않는다.
반면 새 함수를 추가하고 싶다면 도형 클래스를 전부 고쳐야 한다. (area() 외의 다형 메소드를 추가하는 경우)

- 객체 지향 코드에서 어려운 변경은 절차적인 코드에서 쉬우며, 절차적인 코드에서 어려운 변경은 객체 지향 코드에서 쉽다.
- 새로운 자료 타입이 필요한 경우에는 **클래스와 객체 지향 기법**이 가장 적합하다.
- 새로운 함수가 필요한 경우에는 **절차적인 코드와 자료 구조**가 적합하다.

### 디미터 법칙

- **모듈**은 자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙이다.
- 클래스 C의 메소드 f는 다음과 같은 객체의 메소드만 호출해야 한다.
    - 클래스 C
    - f가 생성한 객체
    - f 인수로 넘어온 객체
    - C 인스턴스 변수에 저장된 객체

```java
// 디미터 법칙 위반 코드
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

참고 글 [[https://mangkyu.tistory.com/147](https://mangkyu.tistory.com/147)]

**기차 충돌**

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

- 한 함수가 아는 지식이 굉장히 많다. 위 코드를 사용하는 함수는 많은 객체를 탐색할 줄 안다는 말이다.
- 위 예제가 디미터 법칙을 위반하는지 여부는 ctxt, Options, ScratchDir이 객체인지 자료 구조인지 달렸다.
    - 객체라면 내부 구조를 숨겨야 하므로 확실히 디미터 법칙을 위반한다.
    - 자료 구조라면 당연히 내부 구조를 노출하므로 디미터 법칙이 적용되지 않는다.
- 단순한 자료 구조에도 조회 함수와 설정 함수를 정의하라 요구하는 프레임워크와 표준(ex bean)이 존재한다.

**잡종 구조**

- 중요한 기능을 수행하는 함수도 있고 공개 변수나 공개 조회/설정 함수도 있다. 공개 조회/설정 함수는 비공개 변수를 그대로 노출한다.
- 새로운 함수는 물론이고 새로운 자료 구조도 추가하기 어려워 양 쪽 세상에서 단점만 모아놓은 구조다.

### 자료 전달 객체

- 때로는 자료 전달 객체라 한다. DTO는 굉장히 유용한 구조체다. 
데이터베이스와 통신하거나 소켓에서 받은 메시지의 구문을 분석할 때 유용하다.
- 일반적인 형태는 Bean 구조다. 빈은 비공개 변수를 조회/설정 함수로 족한다.

**활성 레코드**

- DTO의 특수한 형태다.
- 공개 변수가 있거나 비공개 변수에 조회/설정 함수가 있는 자료구조지만, 대게 save 또는 find와 같은 탐색함수도 제공한다.
- 활성 레코드는 데이터베이스 테이블이나 다른 소스에서 자료를 직접 변환한 결과다.
- 비즈니스 규칙을 담으면서 내부 자료를 숨기는 개체는 따로 생성한다.

### 결론

- 객체
    - 동작을 공개하고 자료를 숨긴다.
    - 기존 동작을 변경하지 않으면서 새 객체 타입을 추가하기 쉽다.
    - 기존 객체에 새 동작을 추가하기는 어렵다.
- 자료 구조
    - 별다른 동작 없이 자료를 노출한다.
    - 기존 자료 구조에 새 동작을 추가하기 쉽다.
    - 기존 함수에 새 자료 구조를 추가하기 어렵다.

## 느낀점
객체와 자료 구조의 개념을 다시 한 번 이해하고 둘의 차이 및 사용 용도를 알아갈 수 있는 챕터였다. 
DTO는 자료 구조인데 그동안 나는 객체처럼 사용하고 있었다. 이 점을 반성하여 다음부터는 자료 구조로 코드를 짤 수 있도록 해야겠다. 
