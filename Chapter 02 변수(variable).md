# Chapter 02 변수(variable)

## 변수란?

- 값을 저장할 수 있는 메모리 상의 공간

## 변수의 선언과 초기화

```java
int age = 21; //age라는 이름의 변수를 선언하고 21로 초기화
```

## 두 변수의 값 교환하기

```java
int x = 10;
int y = 20;
//x와 y의 값을 교환
int tmp = 0; //x값을 임시로 저장할 수 있는 변수 선언
tmp = x;
x = y;
y = tmp;
```

## 변수의 명명규칙

- 대소문자가 구분되며 길이에 제한이 없음 ( True와 true는 다른것으로 간주됨)

- 예약어를 사용 x

- 숫자로 시작 x

- 특수문자는 '_'와 '$'만을 허용

  그 외 권장하는 규칙(암묵적인 약속)

  - 클래스 이름의 첫 글자는 항상 대문자로함
  - 여러 단어로 이루어진 이름은 단어의 첫 글자를 대문자로 함
  - 상수의 이름은 모두 대문자로 한다. 여러 단어로 이루어진 경우 '_'로 구분함

## 변수의 타입

###    1. 기본형(primitive type) - 실제 값(data)을 저장

|        | 1 byte  | 2 byte | 4 byte | 8 byte |
| :----: | :-----: | :----: | :----: | :----: |
| 논리형 | boolean |        |        |        |
| 문자형 |         |  char  |        |        |
| 정수형 |  byte   | short  |  int   |  long  |
| 실수형 |         |        | float  | double |

- 논리형 - boolean

  - boolean형 변수에는 true와 false 중 하나를 저장할 수 있으며 기본값(default)은 false이다.

- 문자형 - char

  - char타입의 변수는 단 하나의 문자만을 저장할 수 있다. 

    ```java
    char ch = 'A' //문자'A'를 char타입의 변수 ch에 저장
    ```

  - 변수에 '문자'가 저장되는 것이 아닌 '문자의 유니코드(정수)'가 저장됨

  - 특수 문자 다루기

    |      특수 문자       | 문자 리터럴 |
    | :------------------: | :---------: |
    |         tab          |     \t      |
    |      backspace       |     \b      |
    |      form feed       |     \f      |
    |       new line       |     \n      |
    |   carriage return    |     \r      |
    |       역슬래쉬       |     \\      |
    |     작은 따옴표      |     \'      |
    |       큰따옴표       |     \"      |
    | 유니코드(16진수)문자 | \u유니코드  |

  - 인코딩과 디코딩(encoding & decoding

    - 문자를 코드로 변환하는 것 - 문자 인코딩
    - 코드를 문자로 변환하는 것 - 문자 디코딩

  - 아스키(ASCII)

    - 정보교환을 위한 미국 표준 코드 (128개의 문자 집합을 제공하는 7 bit 부호)

- 정수형 - byte, short, int, long

  - 모든 정수형은 부호있는 정수이므로 왼쪽의 첫 번째 비트를 '부호 비트'로 사용

  |    정수형의 표현형식    |  종류  | 값의 개수 |
  | :---------------------: | :----: | :-------: |
  | 부호 비트 = 0 (n-1 bit) | 0,양수 |  2^(n-1)  |
  | 부호 비트 = 1 (n-1 bit) |  음수  |  2^(n-1)  |

  | 타입  | 저장 가능한 값의 범위 |     크기      |
  | :---: | :-------------------: | :-----------: |
  | byte  |      -2^7~2^7-1       | 8bit = 1byte  |
  | short |     -2^15~2^15-1      | 16bit = 2byte |
  |  int  |     -2^31~2^31-1      | 32bit = 4byte |
  | long  |     -2^63~2^63-1      | 64bit = 8byte |

  - 정수형의 오버플로우 : 연산과정에서 해당 타입이 표현할 수 있는 값의 범위를 넘어서는 것
    - 부호없는 정수의 오버플로우 : 2진수로 '0000'이 될 때 오버플로우 발생
    - 부호있는 정수의 오버플로우 : 부호비트가 0에서 1이 될 때 오버플로우 발생

- 실수형 - float, double

  - 실수형의 범위와 정밀도

  | 타입   | 저장 가능한 값의 범위(양수) | 정밀도 | 크기          |
  | ------ | --------------------------- | ------ | ------------- |
  | float  | 1.4x10^(-45)~3.4x10^38      | 7자리  | 32bit = 4byte |
  | double | 4.9x10^(-324)~1.8x10^308    | 15자리 | 64bit = 8byte |

  - 실수형의 저장방식

    - 실수형은 값을 부동소수점수의 형태로 저장

    $$
    부동소수점수의 형태 = \pm M*2^E
    $$

    - 부호지수가수

###    2. 참조형(reference type) - 어떤 값이 저장되어 잇는 주소(memeory address)를 값으로 가짐

``` java
클래스이름 변수이름; // 변수의 타입이 기본형이 아닌 것들은 모두 참조변수이다.
```

###    3. 상수와 리터럴(constant & literal)

- 리터럴 - 기존에 알고 있던 '상수' 

- 상수 - 값을 저장할 수 있는 공간이지만 변수와 달리 한번 값을 저장하면 다른 값으로 변경x

- 변수의 타입 앞에 키워드 'final'을 붙여주기

- 상수는 반드시, 선언과 동시에 초기화를 해주어야함

  ``` java
  final int MAX_SPEED = 10; 
  ```

- 상수가 필요한 이유 : 코드의 이해와 수정을 쉽게 만든다.

## 형식화된 출력 - printf()

- println() 은 사용하기엔 편하지만 변수의 값을 그대로 축력하므로, 값을 변환하지 않고는 다른 형식으로 출력할 수 없음 (println()은 출력 후 줄바꿈을 함)
- printf()는 '지시자(specifier)'를 통해 변수의 값을 여러 가지 형식으로 변환하여 출력하는 기능을 가짐

## 화면에서 입력받기 - Scanner

- Scanner클래스를 이용하면 화면으로부터 입력을 받을 수 있다.

``` java
import java.util.* //Scanner 클래스를 사용하기 위해 추가
Scanner scanner = new Scanner (System.in); //Scanner 객체 생성
String input = scanner.nextLine(); //입력받은 내용을 input에 저장
int num = Integer.parseInt(input); //입력받은 내용을 int타입의 값으로 변환
```



## 진법

### 1. 10진법과 2진법

- 10진법 : 우리가 일상생활에서 주로 사용함 (0~9까지 사용)
- 2진법 : 컴퓨터와 같은 전기회로에서 사용함 (0과 1만을 사용)

### 2. 비트(bit)와 바이트(byte)

- 한 자리의 2진수를 '비트(vinary digit)'라고함 - 컴퓨터가 값을 저장할 수 있는 최소 단위
- 1비트 8개를 묶어서 '바이트(byte)'라고 함 - 데이터의 기본 단위
- '워드(word)' - CPU가 한 번에 처리할 수 있는 데이터의 크기 (ex/ 32비트 CPU에서 1워드 == 32비트)

### 3. 8진법과 16진법

- 2진법으로 값을 표현하면 자리수가 상당히 길어진다는 단점 --> 8진수, 16진수
- 2진수를 8진수로 변환 --> 2진수를 뒤에서부터 3자리씩 끊어서 그에 해당하는 8진수로 바꿈
- 2진수를 16진수로 변환 --> 2진수를 뒤에서부터 4자리씩 끊어서 그에 해당하는 16진수로 바꿈

### 4.정수의 진법변환

- 10진수를 n진수로 변환 : 10진수를 다른 진수로 변환하려면 해당 진수로 나누고 나머지 값을 옆에 적는것을 더 이상 나눌 수 없을 때까지 반복한 다음 마지막 몫과 나머지를 아래부터 위로 순서대로 적으면 됨
- n진수를 10진수로 변환 : 각 자리의 수에 해당 단위의 값을 곱해서 모두 더하면 됨 

### 5.실수의 진법변환

- 10진 소수점수를 2진 소수점수로 변환 : 10진 소수점수에 2를 소수부가 0이 될 때까지 반복하고 정수부를 위에서 아래로 적음

### 6. 음수의 2진표현 - 2의 보수법

- n의 보수 : 더했을 때 n이 되는 수

- 10진수 2는 2진수로 '10'이고 2진수로 '10'은 **자리올림이 발생하고 0이 되는수**를 뜻함--> 2의 보수관계에 있는 두 2진수를 더하면 0이 됨

- 음수를 2진수로 표현하기 --> 10진 음의 정수의 절대값을 2진수로 변환한뒤 그 2진수의 2의 보수를 구함 

- 2의 보수 구하기
  $$
  2의 보수 = 1의 보수 + 1 (어떤 2진수에 1의 보수 + 1을 하면 0이 되므로)
  $$

- 

- 1의 보수 == 0을 1로, 1을 0으로 바꾼 수

## 형변환

### 형변환(캐스팅, casting)이란?

- 서로 다른 타입간의 연산을 수행하기 위해 변수나 리터럴의 타입을 다른 타입으로 변환하는 것

### 형변환 방법

- 형변환하고자 하는 변수나 리터럴의 앞에 변환하고자 하는 타입을 괄호와 함께 붙여주면 됨 -> (타입)피연산자
- 위에 사용되는 괄호()는 '캐스트 연산자' 또는 '형변환 연산자'라고 하며, 형변환을 '캐스팅(casting)'이라고도 함

``` java
double d = 85.4;
int score = (int)d; //double타입의 변수 d를 int타입으로 형변환
```

- 형변환 연산자는 그저 피연산자의 값을 읽어서 지정된 타입으로 형변환하고 결과를 반환함 --> 피연산자인 변수 d의 값은 형변환 후에도 아무런 변화가 없다.
- 기본형(primitive type) 에서 boolean을 제외한 나머지 타입들은 서로 형변환이 가능함
- 기본형과 참조형간의 형변환은 불가능

### 정수형간의 형변환

- 큰타입에서 작은타입으로의 변환 --> 경우에 따라 '값손실(olss of data)'이 일어날 수 있음(크기의 차이만큼 잘림)
- 작은타입에서 큰 타입으로 변환 -->저장공간의 부족으로 잘려나가는 일이 없고 빈공간이 0 또는 1로 채워짐

### 실수형간의 형변환

- 작은타입에서 큰 타입을 변환 --> 빈 공간을 0으로 채움

### 정수형과 실수형 간의 형변환

- 정수형을 실수형으로 변환 --> 정수를 2진수로 변환한 다음 정규화를 거쳐 실수의 저장형식으로 저장
- 실수형을 정수형으로 변환 --> 실수형의 소수점이하 값은 버려짐

### 자동형변환

- 다른 타입간의 대입이나 연산을 할 때, 형변환으로 타입을 일치시키는 것이 원칙이지만 경우에 따라 생략 가능

  ``` java
  float f = 1234; //형변환의 생략 . float f = (float)1234;와 같음
  ```

- 명시적 형변환 : 형변환이 프로그래머의 실수가 아닌 의도적인 것으로 간주하고 컴파일러가 에러발생 x

  ``` java
  char ch = (char)1000; //명시적 형변환. 에러가 발생하지 않음
  ```

- 서로다른 두 타입간의 덧셈에서는 두 타입 중 표현범위가 더 넓은 타입으로 형변환하여 타입을 일치시킨 다음에 연산을 수행 --> 이처럼 연산과정에서 자동적으로 발생하는 형변환을 '산술 변환'이라고 함

### 자동형변환의 규칙

- 컴파일러의 자동 형변환 판단 기준 : 기존의 값을 최대한 보존할 수 있는 타입으로 자동 형변환함
