 + oop의 기본 컨셉은 프로그램 내에서 표현하고자 하는 **실 세계의 일들을 객체를 사용해서 모델링 하고** , 
객체를 사용하지 않으면 불가능한 또는 많이 어려웠을 일들을 쉽게 처리하는 방법을 제공한다는 것이다.

 + 객체는 변수와 함수와 데이터구조로 구성된다.  
 
 + 절차적인 프로그래밍 > 구조적인 프로그래밍 > 객체지향 프로그래밍
 
 + 객체에서 함수는 데이터를 위주로 클래스에 수납한다. WHY? 구조화된 데이터를 사용하는 함수 모듈의 독립성을 침해하는 문제를 해결 할 수 있기 떄문이다.
 
 + 함수는 외부의 수정에 절대 영향을 받아서는 안된다.
 
 + 구조적인 프로그래밍에서 함수가 다른 클래스 내에 지역변수를 받아서 사용하는 경우, 변수가 수정될 경우 함수도 영향을 받는다.
 
 + 구조화된 객체를 사용하는 함수는 객체의 구조 변경에 아주 취약하다.
   + 해결방법: **구조화된 데이터를 사용하는 모든 함수들을 데이터구조를 정의하고 있는 클래스 내부에 정의한다.** 데이터구조를 변경했을 경우 범위가 한정되므로, 수정의 부담이 줄어든다.
   
 + 데이터와 데이터를 사용하는 함수를 같이 모아놓은것을 캡슐이라고 한다.
 
 + 캡슐의 가장 중요한점은 데이터구조의 변화가 캡슐 내부에서만 이뤄진다.
 
 + 캡슐화: 데이터 구조와 함수를 하나의 영역에 함께 모아 놓는 작업

***

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

***

+ 접근 제어 지시자
  + p
