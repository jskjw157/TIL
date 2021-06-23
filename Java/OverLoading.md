+ 함수 오버로드 : 기존의 함수에 똑같은 함수를 또 만드는것 



+ 오버로드 함수

  + ***같은 기능 하지만 다른 추가 인자를 가지는 함수***

  + 공통의 기능을 갖고 있는 함수들을 모두 구현할 필요가 없고, 인자가 가장 많은 오버로드 함수 하나만 구현한다.(코드 집중화)
  ```java
  static void printList(ExamList list){
    printList(list, 3) // 오버로드 함수를 호출해서 코드를 생략한다.
  }
  
  static void printList(ExamList list, int size){
    //(기능 구현 코드)
  }
  ```
  + 기본함수에 사용자를 위해서 옵션으로 좀더 세밀한 인자를 갖고 있는 함수

  + 인자를 갖고있는 기본함수로부터, 친절하게 오버해가면서 인자를 추가하는 함수

  + 오버로드 함수를 구현하면 사용자가 골라 쓸 수 있다.


+ 기본함수


**printList(list);**
  ```java
  static void printList(ExamList list){
    //(생략)
  }
  ```
 
 
 
+ 오버로드 함수
 

**printList(list,3);**
  ```java
  static void printList(ExamList list, int size){
    //(생략)
  }
  ```
 
  **printList(list,1,3);**
  ```java
  static void printList(ExamList list, int offset, int size){
    //(생략)
  }
  ```
