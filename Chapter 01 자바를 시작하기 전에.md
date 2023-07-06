# CH1. 자바를 시작하기 전에

## 1. 자바(Java Programming Language) 

### 자바 언어의 특징

1. 운영체제에 독립적
2. 객체지향언어
3. 비교적 배우기 쉬움
4. 자동 메모리 관리(Garbagge Collection)
5. 네트워크와 분산처리를 지원
6. 멀티쓰레드 지원
7. 동적 로딩(Dynamic Loading)지원

### JVM(Java Virtual Machine)

- 자바를 실행하기 위한 가상 기계
- 자바로 작성된 애플리케이션은 모두 JVM에서만 실행됨
- java 애플리케이션은 JVM하고만 상호작용을 하기 때문에 OS와 하드웨어에 독립적 (단, JVM은 OS에 종속적이기 때문에 해당 OS에서 실행가능한 JVM이 필요)

## 2. 자바개발환경 구축하기

### 자바 개발도구(JDK) 설치하기

#### 	JDK의 bin디렉토리에 있는 주요 실행파일	

- javac.exe : 자바 컴파일러, 자바소스코드를 바이트코드로 컴파일
-  java.exe  : 자바 인터프리터, 컴파일러가 생성한 바이트코드를 해석하고 실행 
- javap.exe : 역어셈블러, 컴파일된 클래스파일을 원래의 소스로 변환

## 3. 자바로 프로그램 작성하기

### Hello.java

``` java
class Hello {
public static void main (String[] args) {
	System.out.println("Hello, world.");
}
}
```

- 자바에서 모든 코드는 반드시 클래스 안에 존재해야 함

```java
class 클래스 이름 {
	public static void main (String[] args) {
	/*
		주석을 제외한 모든 코드는 클래스의 블럭 {} 내에 작성해야 한다.
	*/
	}
}
```

### 자주 발생하는 에러와 해결방법

- cannot find symbol 또는 cannot resolve symbol - 변수나 메서드의 이름을 잘못 사용한 경우 
- ';'expected 세미콜론';'이 필요한 곳에 없다는 뜻
- Exception in thread "main" java.langNoSuchMethodError: main - 'main'메서드를 찾을 수 없다.
- Exception in thread "main" java.langNoClassDefFoundError: Hello - 'Hello'라는 클래스를 찾을수 없다.
- illegal start of expression - 문법적 오류가 있다.
- class, omterface, pr enum expected - '키워드 class나 interface 또는 enum이 없다.' (보통 괄호의 개수가 일치x)

### 주석(comment)

- 프로그램의 설명을 덧붙임
- 범위주석 (/**/)과 한 줄 주석(//~~)이 있음

