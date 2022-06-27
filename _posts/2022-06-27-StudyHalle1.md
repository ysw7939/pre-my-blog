---
layout: post
title:  "JVM"
author: Yang
categories: [JAVA]
tag: [바이트코드, JIT컴파일러, 자바컴파일방법 , 자바실행방법 ,JRE와 JDK차이 , JVM 구성요소]
img_path: /assets/img/
---
# 스터디 할래 1주차

자산 유형: JDK와 JRE차이, JIT 컴파일러란?, JVM, JVM 구성 요소, 바이트코드란?, 실행하는 방법, 컴파일 하는 방법

![HALLE](HALLE.png)

# JVM

**J**ava **V**irtual **M**achine 의 약자다. 자바 이전에 C언어는 기계어로 번역하는 작업 즉, 컴파일 작업을 운영체제 마다 다른 컴파일러로 컴파일 하는 작업을 거쳐야 했다.  하지만 자바는 자바컴파일러를 거쳐 운영체제로 가기전에 JVM이 사이에서 중개자 역할을 한다. JVM은 운영체제가 뭐가 되었든 상관없이 프로그램을 실행할 수 있도록 도와주는 역할을 한다.  

![JVM](JVM.png)

# JDK와 JRE의 차이

java9버전 부터는 JRE가 사라지고 JDK만 있다.

## JDK

자바의 JDK는 **JRE를 포함**에 자바를 실행하고 프로그래밍에 필요한 모든 구성요소를 갖춘 SDK(Softwar DevelopmentKit)이다. 

자바 개발 시 필요한 라이브러리들과 자바를 컴파일 하는 **javac**, 자바 소스파일을 주석및 어노테이션을 이용해 html파일로 문서화 할수 있는 **javadoc**등이 있다. 

## JRE

자바를 실행하고 동작하기 위해 필요한 라이브러리들과 각종 API, JVM을 의미한다. JRE는 개발(작성)은 안되고 실행(읽기)만된다.

# 바이트코드

- 바이너리 코드가 컴퓨터가 인식할 수 있는 코드라면 바이트 코드는 가상머신이 인식할 수 있는 코드이다.
- 자바 소스 파일이 컴파일 과정을 거치면 기계어는 아니지만 JVM이 이해할 수 있는 바이트코드가 된다.
- 자바 컴파일러에 의해 변환되는 코드는 1바이트라서 바이트코드라고 불린다.
- 이러한 자바 바이트코드의 확장자는 .class이다.

### **🤷‍♂️그냥 바로 바이너리 코드로 컴파일 하면 되지 왜 JVM을 거쳐야만 할까?**

1. **운영체제 간에 결합성을 낮출수 있다.** 
JVM은 운영체제를 신경 쓰지않고 실행할수 있도록 도와준다. 
2. **코드를 재사용 하기 위해서.**
JVM에는 JIT 컴파일러가 있다. JIT 컴파일러는 중복되는 바이트코드를 얼마나 중복되는지 확인하고 일정 기준을 넘는다면 저장해 두어 재사용 할 수 있다.

## JIT 컴파일러

인터프리터는 명령어를 하나씩 실행한다. 그러다 보니 각각의 명령어 단위로 본다면 컴파일 언어보다 빠르지만 전체적으로 봤을 때 컴파일러 보다 상대 적으로 실행 속도가 느렸다. 중복되는 코드가 있더라도 라인별로 실행했기 때문에 중복된 부분을 구분할 수 없었기 때문이다. 

JIT(Just-In-Time) 적기 공급, 무재고 방식을 말한다. 다시 말해 **재고를 쌓아 두지 않고 필요한 만큼만 생성해서 사용**한다는 의미다. JIT 컴파일러는 인터프리터 처럼 한줄 씩 실행한다. 한줄 씩 캐시에 기계어로 저장해 두었다가 같은 명령어가 나오면 캐시에 저장되었던 기계어를 사용하게 된다. 

![JIT](JIT.png)

- 인터프리터
    
    컴파일러는 처음부터 끝까지 기계어로 번역하고 실행하는 하는 반변 인터프리터는 코드를 한 줄씩 읽어 내려가며 실행하는 프로그램이다. 파이썬과 자바스크립트는 인터프리터 언어다.
    

# JVM 구성 요소

### 1. Class Loader

class 파일이 된 바이트코드를 JVM이 운영체제로 부터 할당받은 공간 Runtime Date  Area로 전달하는 역할을 한다. 

### 2. Execution Engine

- JIT컴파일러를 활용하여 .class 바이트코드를 명령어 단위로 읽어 실행한다.

### 3. Garbage Collector

- 힙메모리는 클래스로 부터 생성된 객체들의 메모리가 존재하는 공간이다. Garbage Collector(GC)는 힙메모리에 있는 객체들이 참조되고있는지 판별하여 아무도 참조하고 있지 않아 쓸모가 없다면 힙메모리 영역에서 객체를 삭제한다.

### 4. Runtime Data Area

JVM의 메모리 영역으로 자바를 실행할때 사용되는 메모리가 저장되어 있는 공간이다. 
메모리의 종류는 크게 Method Area, Heep Area, Stack Area, PC Register, Native Method Stack로 나눠진다. 

### 1) Method(Static) Area

- JVM이 읽어들인 클래스와 인터페이스, 런타임 상수 풀, 맴버 변수(필드), Static 변수, 생성자와 메소드를 저장하는 공간

### 2) Heep Area

- `new` 연산자로 생성된 객체들 또는 인스턴스와 배열을 저장한다. 배열 또한 new ArrayList로 시작되는 객체 이다. 그냥 **`new`**를 통해 생성되는 모든 객체들이 저장되는 공간이다.
- 객체들이 생성과 동시에 인스턴스 변수를 초기화 할수 있는 생성자도 결국 하나의 객체안에 포함되는 개념이기 때문에 생성자로 초기화된 변수 값들도 힙 영역에 저장된다.

### 3) JVM Stacks

쓰레드는 프로그램을 실행하는 단위이며, 실행하는 주체다. JVM Stacks는 그런 쓰레드의 영역이다. 스레드를 생성하지 않았다면 main 스레드만 존재 한다. main 메서드를 호출하면 stack프레임을 생성하게 되고 그안에서 실행되는 지역변수를 저장하게 된다. 이때 기본 자료형은 변수의 값 그데로 같이 저장되지만 참조형 자료형은 변수에 실제 데이터의 주소 값만 갖게된다. 실제 데이터는 heep영역에 생성된다.  

스택메모리는 메소드의 호출과 함께 할당되고 메소드의 호출이 완료되면 소멸한다. 

**예시**

```java
 class Car {

    private String modelName;

    private int modelYear;

    private String color;

    private int maxSpeed;

    private int currentSpeed;

 

    Car(String modelName, int modelYear, String color, int maxSpeed) {

        this.modelName = modelName;

        this.modelYear = modelYear;

        this.color = color;

        this.maxSpeed = maxSpeed;

        this.currentSpeed = 0;

    }

 

    public String getModel() {

        return this.modelYear + "년식 " + this.modelName + " " + this.color;

    }

}

 

public class Method02 {

    public static void main(String[] args) {

        Car myCar = new Car("아반떼", 2016, "흰색", 200); // 생성자의 호출

        System.out.println(myCar.getModel()); // 생성자에 의해 초기화되었는지를 확인함.

    }

}
```

![Memory](Memory.png)

### 4) PC Registers

소프트웨어는 명령어와 데이터로 이루어져있다. 프로그램 카운터 에서는 데이터들을 처리할 명령어를 저장하는 공간이다. 

### 5) Native Method Stack

자바가 아닌 다른언어로 작성된 네이티브 메서드를 지원하기 위해 사용되는 스택이다.

# 컴파일 하는 방법

자바에서 컴파일 하는 방법으로는 두가지가 있다. 하나는 Java Compiler(javac), 나머지 하나는 JIT 컴파일러다

### javac로 컴파일 하는 법

Hello.java 파일을 생성한다.

```java
public class Hello {
    public static void main(String args[]){
        System.out.println("Hello,Java");
    }
}
```

![cmd1](cmd1.png)

cmd에서 javac Hello.java 명령어를 입력하여 컴파일 한다.

![cmd5](cmd5.png)

바이트코드인 .class파일이 생성된다

![cmd2](cmd2.png)

javap 명령어로 실행하게 되면 사람이 읽을 수 있는 형태로 출력되게 된다.
위 코드를 OP코드(operation code)라고 한다.

클래스 파일을 실행할 때는 java 클래스 파일명을 실행한다.

![cmd3](cmd3.png)

### 🤷‍♂️만약 다른 버전의 자바컴파일러로 컴파일 했을 때 실행이 될까?

상위 버전으로 컴파일한 .class 파일은 실행할수 없다. 하지만 하위 버전 컴파일러로 컴파일한 파일은 상위버전에서 실행이 가능하다. 

![cmd4](cmd4.png)
```java
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main" java.lang.UnsupportedClassVersionError: Hello has been compiled by a more recent version of the Java Runtime (class file version 61.0), this version of the Java Runtime only recognizes class file versions up to 52.0
```

상위 버전으로 컴파일 하고 하위버전에서 실행했을 때 출력되는 에러 메세지를 기억해 두자. 스프링이나 라이브러리가 자신이 쓰고 있는 자바 버전보다 상위의 버전으로 패키징하였을 경우 위와 같은 에러 메세지가 출력될 수 있다.

### 🤷‍♂️상위 버전에 컴파일러로 컴파일 하더라도 실행되도록 할 수 있을까?

컴파일 할때 컴파일 옵션을 주면된다. -source, -target 옵션으로 실행가능하도록 할 버전을 선택한다. 

```java
javac -source 1.8 -target 1.8 Hello.java
```

```java
warning: [options] bootstrap class path not set in conjunction with -source 8
1 warning
```

컴파일은 잘되지만 위와 같은 경고 메세지가 나온다. 실행가능하도록 할 버전의 rt.jar위치를       

-bootclasspath옵션을 주어 표시해 한다. 

```java
javac -source 1.8 -target 1.8 Hello.java -bootclasspath C:\Users\Owner\java8\lib\rt.jar Hello.java
```

이제 경고메시지도 출력되지 않고 하위 버전으로 실행해도 잘 동작한다.

![cmd6](cmd6.png)