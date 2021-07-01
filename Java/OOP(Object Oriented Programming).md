 # 객체지향 프로그래밍
 <br/>
 
 + oop의 기본 컨셉은 프로그램 내에서 표현하고자 하는 **실 세계의 일들을 객체를 사용해서 모델링 하고** , 
객체를 사용하지 않으면 불가능한 또는 많이 어려웠을 일들을 쉽게 처리하는 방법을 제공한다는 것이다.
<br/>

+ 객체는 변수와 함수와 데이터구조로 구성된다.
<br/>
 
 + 절차적인 프로그래밍 > 구조적인 프로그래밍 > 객체지향 프로그래밍
 <br/>
 
 + 객체에서 함수는 데이터를 위주로 클래스에 수납한다. WHY? 구조화된 데이터를 사용하는 함수 모듈의 독립성을 침해하는 문제를 해결 할 수 있기 떄문이다.
 <br/>
 
 + 함수는 외부의 수정에 절대 영향을 받아서는 안된다.
 <br/>
 
 + 구조적인 프로그래밍에서 함수가 다른 클래스 내에 지역변수를 받아서 사용하는 경우, 변수가 수정될 경우 함수도 영향을 받는다.
 <br/>
 
 + 구조화된 객체를 사용하는 함수는 객체의 구조 변경에 아주 취약하다.
   
   + 해결방법: **구조화된 데이터를 사용하는 모든 함수들을 데이터구조를 정의하고 있는 클래스 내부에 정의한다.** 데이터구조를 변경했을 경우 범위가 한정되므로, 수정의 부담이 줄어든다.
<br/>

 + 데이터와 데이터를 사용하는 함수를 같이 모아놓은것을 캡슐이라고 한다.
<br/>
 
 + 캡슐의 가장 중요한점은 데이터구조의 변화가 캡슐 내부에서만 이뤄진다.
<br/>
 
 + 캡슐화: 데이터 구조와 함수를 하나의 영역에 함께 모아 놓는 작업
<br/>

***

<br/>

# static method와 instance method
<br/>

+ static method : 고전적인 함수로 모든값을 파라미터를 통해서 넘겨 받고 일반적인 함수와 같은 의미로 사용하는 함수

```java
public static void main(String[] args){
  ExamList list = new ExamList();
  🔸ExamList.inputList(list);
}
```
🔻🔻🔻
```java
class ExamList
{
  public static void inputList(ExamList list)
  {
    list.exams[list.current] = new Exam();
  }
}
```
<br/>

+ instance method : 인스턴스 객체를 통해서 호출되고, 묵시적으로 객체를 넘겨받는 함수

```java
public static void main(String[] args){
  ExamList list = new ExamList();
  🔸list.inputList();
}
```
🔻🔻🔻
```java
class ExamList
{
  public void inputList()
  {
    this.exams[this.current] = new Exam();
  }
}
```
  함수를 정의하는 부분에서 static과 파라미터가 없고, 파라미터 대신 this로 작성한다.(this는 생략 가능)

<br/>

***
<br/>

+ 접근 제한자 : 캠슐을 꺠지 못하게 하는 도구(클래스내의 데이터구조와 함수를 외부에서 접근하지 못하게 하는 것)
  
  + private   : 동일 클래스 O, 파생 클래스 X, 외부 클래스 X
  
  + protected : 동일 클래스 O, 파생 클래스 O, 외부 클래스 X
  
  + public    : 동일 클래스 O, 파생 클래스 X, 외부 클래스 O
<br/>

+ 일반적으로 데이터 구조는 private으로 서비스 해야되는 함수는 public으로 정의한다.
```java
public class ExamList {
 
 private Exam[] exams;
 private int current;
 
 public void printList() {
 //(생략)
 }
 
 public void inputList() {
 //(생략)
 }

}
```
<br/>

***

<br/>

+ 객체의 실체화 : 객체의 데이터 구조가 메인 메모리에 공간을 확보하여 실존하고 있는 상태
<br/>

+ 객체의 초기화 : 처음에 객체를 생성할 떄, 변수의 공간에 가지고 있어야 할 기본적인 값을 넣어줌
<br/>

+ 생성자 : 객체의 초기화를 위한 특별한 함수
  
  + new ExamList(); = new ExamList {객체의 실체화} + (); {앞에서 만들어진 객체를 초기화 하는 생성자를 호출}
  
  + 갓 생성된 객체가 있어야만 호출 할 수 있는 함수
<br/>

+ 생성자의 조건
 
  1. 객체가 생성 되자 마자 무조건 제일 먼저 실행되어야 만 한다.
  
  2. 생성될 떄 단 한번만 실행되어야 만 한다. 
<br/>

+ 생성자는 함수명이 없다.(정의할 떄의 함수명은 클레스와 같은 이름으로 표기하며, 초기화 할 객체를 한정하기 위한 한정사이다. 또한, **정의시 반환타입은 없다.**)
<br/>

```java
class ExamList{

 public ExamList() {
		exams = new Exam[3];
		current = 0;
		
	}
 
}
```
<br/>

+ 생성자의 오버로드

	+ 기본 생성자에서 오버로드 생성자를 호출 할 떄, 생성자는 객체가 생성 될 떄 호출 할 수 있으므로, 기존의 생성자가 넘겨받은 **객체 this를 통해서 호출한다.**

```java
class ExamList(){
	
	private Exam[] exams
	private int current;
	
	public ExamList(){
		this(3);
	}
	
	public ExamList(int size){
		exams = new Exam[size];
		current = 0;
	}
}
```
<br/>

+ 생성자를 하나도 정의하지 않는다면? 
	
	+ 컴파일러가 컴파일 할 떄, 기본 생성자를 스스로 만든다. 참조 변수가 실체화 될 경우 null, 값 변수가 실체화 될 경우에는 0으로 초기화 한다.

<br/>

***

<br/>

+ Getters/Setters의 용도
	
	+ 데이터 구조가 변경됨 으로써, 종속되는 문제를 해결하기 위해서 이다.
	
	+ 구조화된 객체를 사용하는 함수는 객체의 구조 변경에 아주 취약하다. 그러므로, 캡슐화를 위해서 Getters/Setters를 사용한다.
<br/>

```java
public class Exam {

	public int kor;
	public int eng;
	public int math;
	
	private int seq; //1
	private int title; // 기말고사
	private int regDate; // 2021-06-13
}
```

🔻🔻🔻

```java
System.out.print("국어:");
exam.kor = scan.nextInt();
```
<br/>

+ 구조적인 변화가 일어났을 떄
<br/>

```java
public class Exam {

	public Subject subject;
	
	private int seq; //1
	private int title; // 기말고사
	private int regDate; // 2021-06-13
}

public class Subject{
	public int kor;
	public int eng;
	public int math;
}
```

🔻🔻🔻

```java
System.out.print("국어:");
exam.subject.kor = scan.nextInt();
```
<br/>

+ 클래스 내부에서 객체의 구조가 변경되면, 외부에서 참조하는 객체도 변경되어야 하는 종속적인 문제가 발생한다.

	+ 이를 해결하기 위해서 Getters/Setters를 사용한다.
<br/>

```java
System.out.print("국어:");
exam.setKor(scan.nextInt());
```
<br/>

+ 클래스 내부에 객체의 구조 변경이 발생해도, 외부에서 Getters/Setters 함수를 사용하면 변경해야 되는 종속적인 문제가 해결된다.
<br/>

***

<br/>

+ UI 코드의 분리
	
	+ 입력하는 방법과 출력하는 방법의 코드는 어떤 UI(콘솔, 윈도우, 웹, 모바일)를 쓰느냐에 따라 달라지게 되어 있다.
<br/>

+ 캡슐들은 서로를 사용하거나 사용되는 관계를 가지고 있다.
<br/>

+ Has A 상속

	+ 부품으로 물려받은 상속(캡슐이 구현해야 할 기능을 구현할 떄, 도구로 사용할 수 있는 형태의 부품으로서 갖는다.)
	
	+ 캡슐이 다른 캡슐의 객체를 부품으로 가지고 있는 상태로, 기능을 사용할 수 있는 상속

	+ Composition(구성요소) Has A : 캡슐이 생성될 떄, 필요로하는 객체를 한번에 다 갖고있는 형태

	+ Aggregation(집합) Has A : 필요할때마다 객체를 수시로 모집해서 집합적으로 갖고있는 형태
<br/>
	
+ dependancy(의존) : 함수내에서 일시적으로 생성해서 사용했다가 제거하는 의존객체 ex) Scanner 함수
<br/>

***

<br/>

+ 재사용

	+ 재사용이란 소스코드를 재사용 하는게 아닌, 배포 코드를 재사용 하는 것을 의미한다.
<br/>

+ 코드 배포 과정
	
	1. 컴파일 -> Exam.class
	
	2. 압축 -> Exam.zip
	
	3. jar(java archive = java class파일을 압축한 형태) -> Exam.jar
<br/>

+ 이클립스 프로젝트 배포 파일 생성하는 방법

	+ 프로젝트 선택 > export > java > JAR file > 클래스파일 선택 > browse 눌러서 저장경로 설정 > 확장자를 jar로 지정 > Finish
<br/>

+ 배포 파일(라이브러리) Classpath 지정하는 방법

	+ 프로젝트 선택 > bulid path > Configure Build Path > Libraries > Classpath > Add External JARs 선택 > Apply and Close
<br/>

***

<br/>

+ Is a 상속
+ 부품이 아닌 틀(프레임)로 가져다가 사용하는 상속
+ 틀(Framework)를 그대로 사용하기 때문에, 생산성이 높아지고 비용도 절감된다.
+ 하지만 서비스를 개발할떄, 유니크한 특성을 살리기 힘들다.
+ 최근에는 it발전속도가 빨라서, 서비스를 프레임워크 없이 다 개발하기는 어렵고, 90%정도 프레임워크를 사용하고, 나머지 10%를 개발하는 추세이다.
