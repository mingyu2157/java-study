# Chapter06 객체지향프로그래밍1(오버로딩~)

## 오버로딩(overloading)

- 메서드 오버로딩 : 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것

**오버로딩의 조건**

1. 메서드 이름이 같아야 한다.

2. 매개변수의 개수 또는 타입이 달라야 한다.

   *반환 타입은 오버로딩을 구현하는데 아무런 영향을 주지 못함



**오버로딩의 예**

- println() - 매개변수로 지정하는 값의 타입에 따라서 호출되는 println메서드가 달라짐



**오버로딩의 장점**

1. 기억하기 쉽고 이름도 짧게 할 수 있어서 오류의 가능성을 줄임 + 메서드의 기능을 쉽게 예측
2. 메서드의 이름을 절약



**가변인자(varargs)와 오버로딩**

- 가변인자 : 메서드의 매개변수 개수를 동적으로 지정할 수 있게 하는 기능 -> 매개변수 중에서 제일 마지막에 선언

  ```java
  public PrintStream printf(String format, Dbject... args) {...} //'타입... 변수명'의 형식으로 선언
  ```

  

- 가변인자는 내부적으로 배열을 이용함 -> 비효율 -> 꼭 필요한 경우에만 사용



## 생성자(Constructor)

- 생성자 : 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 메서드' -> 인스턴스 변수의 초기화 작업에 주로 사용

- 생성자의 조건

  1. 생성자의 이름은 클래스의 이름과 같아야 한다.
  2. 생성자는 리턴 값이 없다.

- 생성자의 정의

  ```java
  클래스 이름(타입 변수명, 타입 변수명, ...) {
      //인스턴스 생성 시 수행될 코드
      //주로 인스턴스 변수의 초기화 코드를 적는다.
  }
  ------------------------------------------------------구분선
  class Card {
      Card() { //매개변수가 없는 생성자
          ...
      }
      Card(String k, int num) { //매개변수가 있는 생성자
          ...
      }
      ...
  }
  ```

  *연산자 new가 인스턴스를 생성하는 것이고 생성자가 인스턴스를 생성하는 것이 아님

  - 수행되는 과정

  ```java
  Card c = new Card();
  
  1.연산자 new에 의해서 메모리(heap)에 Card클래스의 인스턴스가 생성됨
  2.생성자 Card()호출되어 수행된다.
  3.연산자 new의 결과로, 생성된 Card인스턴스의 주소가 반환되어 참조변수 c에 저장됨
  ```

- 기본 생성자(default constructor)

  컴파일 할 때 소스파일의 클래스에 생성자가 하나도 정의되지 않은 경우 컴파일러가 자동적으로 추가

  매개변수x, 내용x

- 매개변수가 있는 생성자

  생성자도 메서드처럼 매개변수를 선언하여 호출 시 값을 넘겨받아서 인스턴스의 초기화 작업에 사용 가능 -> 매우 유용

  ```java
  class Car {
      String color;
      String gearType;
      int door;
      Car() {} //있어야함
      Car(String c, String g, int d) {
          color = c;           //여기에 직접 값을 초기화하면 null null 0 이 됨
          gearType = g;
          door = d;
      }
  }
  public class test6_24 {
      public static void main(String[] args) {
          Car c1 = new Car() ;
          c1.color = "white";
          c1.gearType = "auto";
          c1.door = 4;
  
          Car c2 = new Car ("white", "auto", 4);
          System.out.println(c1.color + c1.gearType + c1.door);
          System.out.println(c2.color + c2.gearType + c2.door);
      }
  }
  
  ```

- 생성자에서 다른 생성자 호출하기 - this(), this

  생성자 간에도 서로 호출이 가능함 (2 조건 만족시)

  1. 생성자의 이름으로 클래스이름 대신 this를 사용한다.
  2. 한 생성자에서 다른 생성자를 호출할 때는 반드시 첫 줄에서만 호출이 가능하다.