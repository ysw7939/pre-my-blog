---
layout: post
title:  "[자바]문자열(String)"
author: Yang
categories: [JAVA]
tag: [자료형, 문자열, equals, 문자열 포메팅, StringBuffer, stringBuilder]
img_path: /assets/img/
---


# 문자열(String)

![String](String.png)

- 위 자료형은 원시(primitive) 자료형이다. 이런 자료형은 `new` 키워드로 값을 생성 할 수없다.  리터럴(literal)로만 값을 대입할 수 있다

**예시**

```java
boolean result = true;
char capitalC = 'C';
int i = 100000;
```

# 문자열

문자열을 나타내는 자료형은 String이다. Stirng은 `new` 키워드로 String 클래스를 생성해서 사용할수 있고 리터럴로 사용할 수있다. 보토은 가급적이면 리터럴 방식으로 사용한다 가독성에 이점이 있고 컴파일 시에도 최적화에 도움을 준다고 한다. 

**예시**

```java
String a = "Happy Java";      //리터럴
String a = new String("Happy Java");  // String 클래스를 생성하여 대입
```

## 문자열 내장 메서드

### equals

equals는 두개의 문자열이 동일한지 비교하여 결과값을 리턴한다. 

```java
String a = "hello";
String b = "java";
String c = "hello";
System.out.println(a.equals(b)); // false 출력
System.out.println(a.equals(c)); // true 출력
```

**🤷 왜 굳이 비교연산자를 사용하지 않고 equals를 사용할까?** 

`==` 연산자를 사용할 경우 String 클래스로 생성했을 때 문제가 발생할 수 있다.

```java
String a = "hello";
String b = new String("hello");
System.out.println(a.equals(b));  // true
System.out.println(a == b);  // false
```

a와 b는 값은 같지만 서로 다른 객체이다. `==` 은 동일한 객체인지를 판별하는 연산자이기 때문에 false를 리턴한다  그래서 문자열의 값을 비교할 때는 반드시 equlas를 사용해야한다.

## 문자열 포메팅

문자열 포메팅은 `String.format` 메소드를 사용한다 문자열 안에서 특정 값을 넣어주고 싶은 자리에 이스케이프 문자를 넣어 특정값과 결합된 문자열을 만들어 낼 수 있다.

```java
System.out.println(String.format("I eat %s apples.", "five"));  // "I eat five apples." 출력
```

### 문자열 포맷 코드

| 코드 | 설명 |
| --- | --- |
| %s | 문자열(String) |
| %c | 문자 1개(character |
| %d | 정수(Integer) |
| %f | 부동소수(floating-point) |
| %o | 8진수 |
| %x | 16진수 |

🤓여기서 재미있는 점은 %s 포맷코드는 어떤 형태의 값이든 문자열로 변환하여 쓰기 때문에 숫자값이든 소수값이든 상관없이 사용할 수 있다.

```java
System.out.println(String.format("I have %s apples",  3));  // "I have 3 apples" 출력
System.out.println(String.format("rate is %s", 3.234));  // "rate is 3.234" 출력
```

### 포맷 코드와 숫자 함께 사용

```java
System.out.println(String.format("%10s", "hi"));  // "        hi" 출력
```

숫자와 함께 사용하게되면 숫자만큼의 빈공간을 비워두고 출력하게 된다. 

```java
System.out.println(String.format("%.4f", 3.42134234));  // 3.4213 출력
```

소수점 네번째 자리까지만 나타내고 싶은경우 `%.4f` 를 사용하여 나타 낼 수있다. 

### System.out.printf

`System.out.printf` 메서드를 사용하면 `String.fomat` 메소드 없어도 동일한 문자열 포메팅을 사용할 수 있다.

```java
System.out.printf("I eat %d apples.", 3);  // "I eat 3 apples." 출력
```

## StringBuffer

한번 생성된 String은 불변(immutable)하는 성격을 가지고 있다. 따라서 다음과 같이 작성 한다고 했을 떄

```java
String result = "";
result += "hello";
result += " ";
result += "hi java";
System.out.println(result);
```

결과값은 hello hi java 가 되겠지만 내부적으로 총 4개의 String객체가 생성된 것이다. 그렇게 된다면 메모리 낭비가 심하게 발생할 수 있다. 

이때 같은 동작을 StringBuffer로 하게되면 StringBuffer는 변경하능(mutable)하기 떄문에 

```java
StringBuffer sb = new StringBuffer();  // StringBuffer 객체 sb 생성
sb.append("hello");
sb.append(" ");
sb.append("hi java");
String result = sb.toString();
System.out.println(result);
```

객체는 총 한번만 생성된다.

🙋 **그럼무조건 StringBuffer를 사용하는 것이 좋을까?**

그건 상황에 따라 다르다. StringBuffer 자료형은 String 자료형보다 메모리 사용량도 많고 속도도 느리다. 따라서 문자열 추가 변경등의 작업이 지속적으로 많을 경우에는 StringBuffer를 사용하고 문자열 변경 작업이 거의 없는 경우에는 그냥 String을 사용하는 것이 유리하다.

### stringBuilder

Stringbuffer와 사용법이 동일한 StringBuilder가 있다 다만 둘의 차이점은 StringBuffer는 멀티 스레드 환경에서 동기화(Synchronzation)을 보장하고 StringBuilder는 StringBuffer보다 성능이 우수한 장점이 있다. 따라서 동기화필요 여부에 따라서 StringBuilder 혹은 StringBuffer를 적절하게 사용하는 것이 유리하다.