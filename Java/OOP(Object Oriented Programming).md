 > # 목차
 ><br/>
 >
 > 	> [1.객체지향 프로그래밍](#객체지향-프로그래밍)
 > 	> <br/>
 > 	>
 > 	> [2. static method and instance method](#static-method-and-instance-method)
 > 	> <br/>
 > 	>
 > 	> [3. 접근 제한자](#접근-제한자)
 > 	> <br/>
 > 	>
 > 	> [4. 생성자](#생성자)
 > 	> <br/>
 > 	>
 > 	> [5. Getters and Setters](#Getters-and-Setters)
 > 	> <br/>
 > 	>
 > 	> [6. Has A 상속](#Has-A-상속)
 > 	> <br/>
 > 	>
 > 	> [7. 재사용](#재사용)
 > 	> <br/>
 > 	>
 > 	> [8. IS A 상속](#IS-A-상속)
 > 	> <br/>
 > 	>
 > 	> [9. Override](#Override)
 > 	> <br/>
<br/>
 
 
 ### 객체지향 프로그래밍
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

### static method and instance method
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

### 접근 제한자
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

### 생성자
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

### Getters and Setters
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

### Has A 상속
<br/>

+ 캡슐들은 서로를 사용하거나 사용되는 관계를 가지고 있다.
<br/>

+ 부품으로 물려받은 상속(캡슐이 구현해야 할 기능을 구현할 떄, 도구로 사용할 수 있는 형태의 부품으로서 갖는다.)
<br/>

+ 캡슐이 다른 캡슐의 객체를 부품으로 가지고 있는 상태로, 기능을 사용할 수 있는 상속
<br/>

+ Composition(구성요소) Has A : 캡슐이 생성될 떄, 필요로하는 객체를 한번에 다 갖고있는 형태
<br/>

+ Aggregation(집합) Has A : 필요할때마다 객체를 수시로 모집해서 집합적으로 갖고있는 형태
<br/>

#### UI 코드의 분리
<br/>

+ 입력하는 방법과 출력하는 방법의 코드는 어떤 UI(콘솔, 윈도우, 웹, 모바일)를 쓰느냐에 따라 달라지게 되어 있다.
<br/>
	
#### dependancy(의존)
<br/>

+ 함수내에서 일시적으로 생성해서 사용했다가 제거하는 의존객체 ex) Scanner 함수
<br/>

***

<br/>

### 재사용
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

### IS A 상속
<br/>

+ 부품이 아닌 틀(Framework)로 가져다가 사용하는 상속
<br/>

+ 틀(Framework)를 그대로 사용하기 때문에, 생산성이 높아지고 비용도 절감된다.
<br/>

+ 하지만 서비스를 개발할떄, 유니크한 특성을 살리기 힘들다.
<br/>

+ 최근에는 발전속도가 빨라서, 서비스를 프레임워크 없이 다 개발하기는 어렵고, 90%정도 프레임워크를 사용하고, 나머지 10%를 개발하는 추세이다.
<br/>

***

<br/>

### Override
<br/>

+ 상속을 받은 클래스를 객체화 할떄, 상속을 해주는 부모 클래스의 객체들을 가진다.
<br/>

+ instance method 호출시 객체를 넘겨받을떄, 묵시적으로 넘겨받은 객체는 this, 그 중에 상속받은 객체만 지명하는 이름은 super 이다.
<br/>

+ 상속받은 객체가 method를 호출할 떄, 기존 클래스내에 해당 method가 없으면, 차선책으로 부모 클래스의 method를 호출 한다.(하지만, 부모클래스의 method는 해당 영역에 정의된 변수만 사용한다.)
<br/>

+ Override method : 부모 method 보다 우선순위가 높고, 부모가 갖고 있는 기능을 가리고 method 내용을 재정의하는 함수.
<br/>

+ Override method는 부모 method와 함수명, 반환타입, 매개변수가 동일해야 된다.

```java

public class Exam {
	int kor;
	int eng;
	int math;

	public int total() {
		
		return  eng+kor+math;
	}

	public float avg() {
		
		return total()/3.0f;
	}
}


public class NewlecExam extends Exam {

	private int com;
	
	@Override
	public int total() {
		
		return super.total()+com;
	}
	
	@Override
	public float avg() {
		
		return total()/4.0f;
	}
	
}
```
<br/>

#### 자식 클래스의 객체 초기화
<br/>

+ 자식 클래스에서 객체를 초기화 할 떄(자식 생성자),  초기화해야되는 내용 일부분이 부모객체이면, 부모의 기능(부모 생성자)으로 초기화 한다.(super())

```java

public class Exam {
	int kor;
	int eng;
	int math;
	
	public Exam() {
		this(0,0,0);
	}
	
	public Exam(int kor, int eng, int math) {
		this.kor = kor;
		this.eng = eng;
		this.math = math;
	}
}


public class NewlecExam extends Exam {

	private int com;

	public NewlecExam() {
		this(0,0,0,0);
	}
	
	public NewlecExam(int kor, int eng, int math, int com) {
		
		🔸super(kor,eng,math);
	
		this.com =com;
	}
}
```
<br/>

***

<br/>

### 참조형식과 호출되는 메소드의 관계
<br/>

```JAVA
NewlecExam exam = new Exam(); // X
```
```JAVA
Exam exam = new NewlecExam(); // O
```
+ WHY? 참조 형식보다 객체 생성 형식의 객체가 더 커야 되기 떄문이다. 


+ 객체를 생성할떄, 부모 참조 형식과 자식 객체 생성 형식이면, 참조 형식과 객체 생성 형식 2가지를 참조한다.

<br/>


+ 자바는 참조형식의 함수보다 객체 생성 형식의 함수 호출을 우선으로 한다.
```java
class exam {

	public void total() {
		return kor + eng + math;
	}
}

class NewlecExam extends Exam {
	
	public noid total() {
		return kor + eng + math + com;
	}
}
```

```java
NewlecExam exam1 = new NewlecExam(1,1,1,1); // 참조형식 : NewlecExam, 객체형식 : NewlecExam
system.out.println(exam1.total());
```
출력 : 4

```java
Exam exam2 = new NewlecExam(1,1,1,1); // 참조형식 : Exam, 객체형식 : NewlecExam
system.out.println(exam2.total());
```
출력 : 4

<br/>

+ 침조 형식이 가지고 있는 메소드에 한해서 오버라이딩 메소드를 호출 할 수 있으며, 가지고 있지 않으면 아예 호출이 불가능하다.
```java
class exam {

	// 없음
}

class NewlecExam extends Exam {
	
	public noid total() {
		return kor + eng + math + com;
	}
}
```

```java
NewlecExam exam1 = new NewlecExam(1,1,1,1); // 참조형식 : NewlecExam, 객체형식 : NewlecExam
system.out.println(exam1.total());
```
출력 : 4

```java
Exam exam2 = new NewlecExam(1,1,1,1); // 참조형식 : Exam, 객체형식 : NewlecExam
system.out.println(exam2.total());
```
출력 : 오류

<br/>

해결방안 :
```java
Exam exam2 = new NewlecExam(1,1,1,1); // 참조형식 : Exam, 객체형식 : NewlecExam
system.out.println((NewlecExam(exam2)).total()); //
```
출력 : 4

+ (NewlecExam(exam2)).total()에서 (NewlecExam(exam2)) 괄호를 밖에 더두르는 이유는 형 변환하는 NewlecExam(exam2)보다 .total()이 우선순위 이기 때문이다.

<br/>

***

<br/>

### 메소드 동적 바인딩(함수 호출 위치 결정 방식 이해하기)
<br/>

```java
class Exam {

	public void total() {   // 함수 주소 : 2A3F
		return kor + eng + math;
	}
}

class NewlecExam extends Exam {
	@Override
	public void total() {    // 함수 주소 :7D3A
		return super.total() + com;
	}
}

public static void print(Exam exam) {
	
	int total = exam.total(); // total 메소드는 print메서드의 전달되는 파라미터 객체에 따라(Exam, NewlecExam) 호출되는 total 메소드가 다르다.
	System.out.println(total);
}

public static void main(String args[]) {

	print(new Exam(1,1,1)); // Exam 객체 전달
	printf(new NewlecExam(1,1,1,1)); // NewlecExam객체 전달
}
```

원래 컴파일러가 메소드를 해석할 경우, 함수가 있는 위치 주소를 적어서 그 위치로 가게 되어 있다.

그 함수를 호출하는 메소드가 어떤객체를 파라미터로 받는냐에 따라서 호출되는 함수 위치가 달라진다.

<br/>

+  정적 바인딩 : 참조 함수 주소를 참조 형식의 의한 결정, 컴파일 시점에 결정, 한번 컴파일되면 바뀌지 않는 함수 바인딩
<br/>

+ 동적 바인딩 : 실행중에 함수의 위치가 결정되는 바인딩, 객체 전달 시점에서 함수 주소 위치를 결정 자바는 동적 바인딩

	+ 동적 바인딩을 지원하기 위한 클래스, 객체들은 데이터를 담는 공간 외에, 추가적으로 **자기의 메서드 테이블을 가리키는 주소 번지 4byte 공간을 더 갖고 있다.**
<br/>

***

<br/>

### 추상화
<br/>

+ 추상화 : 코드 집중화(X) > 서비스 집중화(캡슐 단위의 공통 서비스)
<br/>

**추상 클래스(공통 분모의 클래스)**

|도형|
|:---:|
|+draw()|
|+setX()|
|+setY()|
|+move()|
<br/>

🔻🔻🔻🔻

<br/>

|원|
|:---:|
|draw()|
|setX()|
|setY()|
|move()|
|setOrigin()|

|네모|
|:---:|
|draw()|
|setX()|
|setY()|
|move()|
|setWidth()|

|선|
|:---:|
|draw()|
|setX()|
|setY()|
|move()|

공통 서비스를 갖고 있는추상 클래스에 IS A 상속으로(틀로) 물려 받아 서비스를(코드) 구현할 필요가 없다.

<br/>

+ 추상 클래스의 생성(공통 서비스화)으로 얻을 수 있는 장점

	1. 코드 집중화
	
	2. 일괄 처리 (부모 추상 클래스로 배열을 만들어서 자식 클래스들을 한번에 참조시킬 수 있다.)
	```java
	Shape shapes = new Shape[10];
	
	shapes[0] = new Circle();
	shapes[1] = new Rect();
	shapes[2] = new Line();
	
	for(int...)
		shapes[i].move();
	```
<br/>

#### 추상 클래스
<br/>

+ 클래스가 뼈대로만 사용할 수 있도록 만든다. 즉 객체화 되는 것을 막는다. Ex) new Exam(); X
<br/>

+ 클래스명 앞에 abstract를 붙이면 추상 클래스가 생성
<br/>
