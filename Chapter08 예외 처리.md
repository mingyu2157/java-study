# Chapter08 예외 처리

**프로그램 오류** : 프로그램이 실행중 어떤 원인에 의해서 오작동을 하거나 비정상적으로 종료되는 경우

1. 컴파일 에러 : 컴파일 시에 발생하는 에러
2. 런타임 에러 : 프로그램 실행 시에 발생하는 에러
3. 논리적 에러 : 실행은 되지만 의도와 다르게 동작

*자바에서는 실행 시 발생할 수 있는 프로그램 오류를 **에러**와 **예외**로 구분한다.

- 에러 : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
- 예외 : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

예외 클래스의 계층구조 

<img src = "https://github.com/mingyu2157/java-study/blob/main/%EC%98%88%EC%99%B8%20%ED%81%B4%EB%9E%98%EC%8A%A4%20%EA%B3%84%EC%B8%B5%20%EA%B5%AC%EC%A1%B0.png?raw=true">

모든 예외의 조상은 Exception클래스이며 두 그룹으로 나눠져 있다

1. Exception클래스들 : 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외 (checked exception - 필수 예외)
   - FileNotFoundException : 존재하지 않는 파일의 이름을 입력하는 경우
   - ClassNotFoundException : 클래스의 이름을 잘못 적은 경우
   - DataFormatException : 입력된 데이터 형식이 잘못된 경우
2. RuntimeException클래스들 : 프로그래머의 실수로 발생하는 예외 (unchecked exception - 선택 예)
   - IndexOutofBoundsException : 배열의 범위를 벗어나는 경우
   - NullPointerException : 값이 null인 참조변수의 멤버를 호출하는 경우
   - ClassCastException : 클래스간의 잘못된 형변환을 하는 경우
   - ArithmeticException : 산술 계산 예외

|                           |                     checkde exception                     |      unchecked exception      |
| :-----------------------: | :-------------------------------------------------------: | :---------------------------: |
|         처리 여부         |                 반드시 예외를 처리해야 함                 | 명시적인 처리를 강제하지 않음 |
|         확인 시점         |                        컴파일 단계                        |           실행 단계           |
| 예외 발생시 트랜잭션 처리 |                  **rollback 하지 않음**                   |        **rollback 함**        |
|         대표 예외         | Exception의 상속을 받는 클래스 중 RuntimeException을 제외 |   RuntimeException하위 예외   |

- 체크 예외 : Rollback이 되지 않고 트랜잭션이 commit까지 완료
- 언체크 예외 : Rollback이 됨

**트랜잭션** : 하나의 작업 단위

예) 쇼핑몰의 상품발송 트랜잭션 -> 포장 / 영수증 발행 / 발송 

3가지 작업중 하나라도 실패하면 3가지 모두 취소하고 상품발송 전의 상태로 되돌림 == rollback(롤백)

상품발송 프로그램 의사코드

```java
상품발송() {
    try {
        포장();
        영수증발행();
        발송();
    }catch(예외) {
        모두취소();  // 하나라도 실패하면 모두 취소한다.
    }
}

포장() throws 예외 {  // 포장, 영수증 발행, 발송 메서드에 try - catch문으로 예외 처리를 하면 뒤죽박죽 될 수 있음
   ...
}

영수증발행() throws 예외 {
   ...
}

발송() throws 예외 {
   ...
}

```





## 예외 처리하기 - try - catch 문

**예외처리** : 프로그램 실행 시 발생할 수 있는 예외에 대비한 코드를 작성하는 것

목적 : 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것

-> 처리되지 못한 예외는 JVM의 예외처리기가 받아서 예외의 원인을 화면에 출력

try - catch 문

```java
try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다.
} catch (Exception1 e1) {
    // Exception1이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch (Exception2 e2) {
    // Exception2가 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch (ExceptionN eN) {
    // ExceptionN이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
}
```

발생한 예외의 종류와 일치하는 catch블럭이 없으면 예외는 처리되지 않음

try - catch 문에서의 흐름

- try블럭 내에서 예외가 발생한 경우
  1. 발생한 예외와 일치하는 catch블럭이 있는지 확인한다.
  2. 일치하는 catch블럭을 찾게 되면, 그 catch블럭 내의 문장들을 수행하고 전체 try - catch문을 빠져나가서 그 다음 문장을 수행
- try블럭 내에서 예외가 발생하지 않은 경우
  1. catch블럭을 거치지 않고 try - catch문을 빠져나가서 수행을 계속한다.

```java
public class Sample {
    public static void main(String[] args) {
        int c;
        try {
            c = 4 / 0; //산술에 문제가 생겼다는 ArithmeticException 예외가 발생
        } catch(ArithmeticException e) { // e 는 ArithmeticException 클래스의 예외 객체
            c = -1;  // 예외가 발생하여 이 문장이 수행된다.
        }
    }
}

```



**printStackTrace()**와 **getMessage()**

printStackTrace() : 예외발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를 화면에 출력한다.

getMessage() : 발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.



- 멀티 catch 블럭

  '|'기호로 연결할 수 있는 예외 클래스의 개수에는 제한이 없음

  멀티 catch는 여러 개의 예외를 통짜로 처리하는 것이기 때문에 각 예외마다 세세하게 제어하고 싶다면 if문과 instanceOf 연산자로 하나하나 분기하며 처리해야 한다.

```java
try {
    // ...
} catch (NullPointException | ArrayIndexOutOfBoundsExcetion e) {
    if(e instanceOf NullPointException) {
    	// ...
    } else if(e instanceOf ArrayIndexOutOfBoundsExcetion) {
    	// ...
    }
}
```



### 예외 발생시키기

키워드 throw를 사용해서 프로그래머가 고의로 예외를 발생시킬 수 있다

1. 연산자 new를 이용해서 발생시키려는 예외 클래스의 객체를 만든다

   ```java
   Exception e = new Exception("고의로 발생시킴")
   ```

2. 키워드 throw를 이용해서 예외를 발생시킴

   ```java
   throw e;
   ```

```java
throw new Exception("고의로 발생시켰음"); // 위 두 줄을 줄여 쓸 수 있음
```



### 메서드에 예외 선언하기

메서드에 예외를 선언하려면 메서드의 선언부에 키워드 throws를 사용해서 메서드 내에서 발생할 수 있는 예외를 적어주기만 하면 됨

```java
void method() trhows Exception1, Exception2, ... ExceptionN {
    // 메서드의 내용
}
```

Exception클래스를 메서드에 선언하면 모든 종류의 예외가 발생할 가능성이 있다는 뜻 --> 그 자손타입의 예외까지도 발생할 수 있음

```java
class ExceptionEx12 {
    public static void main (String[] args) throws Exception {
        method1(); //같은 클래스내의 static 멤버이므로 객체생성없이 직접 호출가능
    } //main메서드의 끝
    
    static void method1 () throws Exception {
        method2();
    } //method1의 끝
    
    static void method2 () throws Exception {
        throw new Exception();
    } //method2의 끝	
}
```



1. 예외가 발생했을 때, 모두 3개의 메서드(main, method1, method2)가 호출스택에 있었으며,
2. 예외가 발생한 곳은 제일 윗줄에 있는 method2()라는 것과
3. main메서드가 method1()을, 그리고 method1()은 method2()를 호출했다는 것을 알 수 있다.

**throw와 throws의 차이**

- throw: 메서드 내에서 예외를 발생시키는 데 사용됨
- thorws: 메서드 선언부에서 사용되며, 해당 메서드가 처리하지 않은 예외를 호출자에게 전달함을 나타냄

### finally 블럭

finally 블럭은 예외의 발생여부에 상관없이 실행되어야 할 코드를 포함시킬 목적으로 사용됨

try - catch문의 끝에 선택적으로 덧붙일 수 있음

```java
try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다.
} catch (Exception1 e1) {
    // 예외처리를 위한 문장을 적는다.
} finally {
    // 예외의 발생여부에 관계없이 항상 수행되어야 하는 문장들을 넣는다.
    // finally블럭은 try - catch문의 맨 마지막에 위치해야 한다.
}
```



### 자동 자원 반환 try - with - resources문

주로 입출력에 사용되는 클래스 중에서는 사용한 후에 꼭 닫아줘야 하는 것들이 있음 -> 사용했던 자원이 반환되기 때문

```java
try (FileInputStream fis = new FileInputStream("score.dat");
    DataInputStream dis = new DataInputStream(fis)) {
    
    while(true) {
        score = dis.readInt();
        System.out.println(score);
        sum += score;
    }
} catch (EOFException e) {
    System.out.println("점수의 총합은 " + sum + "입니다.");
} catch (IOException ie) {
    ie.printStackTrace();
}
```

try - with - resources문의 괄호()안에 객체를 생성하는 문장을 넣으면, 이 객체는 따로 close()를 호출하지 않아도 try블럭을 벗어나는 순간 자동적으로 close()가 호출

### 사용자정의 예외 만들기

기존의 예외 클래스를 상속받아서 새로운 예외 클래스를 정의할 수 있음(보통 Exception클래스나 RuntimeException클래스를 상속받)

```java
class MyException extends Exception {
    MyException (String msg) { // 문자열을 매개변수로 받는 생성자
        super(msg); // 조상인 Exception클래스의 생성자를 호출한다
    }
}
```

- Exception클래스는 생성시에 String 값을 받아서 메시지로 저장할 수 있

### 예외 되던지기 (exception re - throwing)

예외를 처리한 후에 다시 예외를 발생시켜서 호출한 메서드로 전달하는 것

```java
class ExceptionEx17 {
	public static void main(String[] args) {
    	try {
        	method1();
        } catch (Exception e) {
        	System.out.println("main메서드에서 예외가 처리됐습니다.");
        }
    } // main 메서드의 끝
    
static void method1() throws Exception{
	try {
    	throw new Exception();
    } catch (Exception e) {
    	System.out.println("method1메서드에서 예외가 처리됐다.");
        throw e; // 다시 예외를 발생시킨다.
    }
} // method 메서드의 끝
}
```

반환값이 있는 return문의 경우, catch블럭에도 return문이 있어야 함 -> 예외가 발생했을 경우에도 값을 반환해야 

### 연결된 예외

한 예외가 다른 예외를 발생시킬 수 있음 -> 예외 A가 예외 B를 발생시켰다면 예외 A를 B의 원인 예외 라고 함

```java
try {
	startInstall(); // SpaceException 발생
    copyFiles();
} catch (SpaceException e) {
	InstallException ie = new installException("설치중 예외발생") // 예외 생성
    ie.initCause(e); // InstallException의 원인 예외를 SpaceException으로 지정
    throw ie; // InstallException을 발생시킨다.
} catch (MemoryException me)
	...
```

initCause()는 Exception클래스의 조상인 Throwable클래스에 정의되어 있기 때문에 모든 예외에서 사용가능

- Throwable initCause (Throwable cause) : 지정한 예외를 원인 예외로 등록

- Throwable getCause() : 원인 예외를 반환

굳이 원인 예외를 등록해서 다시 예외를 발생시키는 이유 

1. 여러가지 예외를 하나의 큰 분류의 예외로 묶어서 다루기 위함

2. 필수 예외(Exception과 그 자손들)를 선택 예외(RuntimeException과 그 자손들)로 변경할 때 연결된 예외로 처리함 

   checked예외로 예외처리를 강제한 이유는 프로그래밍 경험이 적은 사람도 견고한 프로그램을 작성할 수 있도록 유도하기 위한 것

   -> 컴퓨터 환경이 많이 달라짐 -> checked예외가 발생해도 예외를 처리할 수 없는 상황이 발생 -> 선택 예외로 변환

