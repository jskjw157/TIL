# 딥다이브 자바스크립트 스터디

### 4.1 변수

---

- **변수**
    
    변수는 하나의 값을 저장하기 위한 수단
    
    [필요한 정보를 저장하기-변수](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/Variables)
    
    프로그래밍 언어에서 데이터를 관리하기 위한 핵심개념으로, 복잡한 애플리케이션도 데이터를 입력(input) / 출력(output) 하는 것이 전부
    
    <aside>
    💡 **하나의 값을 저장하기 위해서 확보한 메모리 공간 자체** 또는 그 메모리 공간을 식별하기 위해서 붙인 이름
    
    </aside>
    
- **컴퓨터의 계산**
    
    계산 혹은 코드를 실행하기 위해서는 기호(리터럴/연산자)의 의미 및 표현식뿐만 아니 의미도 해석(parsing)할 수 있어야 함
    
    - 예시
        
        ```jsx
        10 + 20
        ```
        
        사람이 위의 식을 계산하려면 >> 숫자와 기호의 의미를 알고 이해할 수 있어야 함
        
        컴퓨터가 위의 식을 계산하려면 >> 기호(리터럴 및 연산자)의 의미를 알고 표현식의 의미를 해석(파싱) 할 수 있어야 함
        
        연산은 CPU에서, 데이터 기억은 메모리에서 진행함
        
- **메모리**
    
    <aside>
    💡 데이터를 저장할 수 있는 메모리 셀의 집합체
    
    </aside>
    
    메모리 셀 하나의 크기는 1 byte (8 bit) 단위이며 데이터를 저장하거나 읽어들임
    
    각 셀은 고유의 메모리 주소를 가지며 메모리 공간의 위치를 나타냄 (0부터 정수로 표현됨)
    
    컴퓨터는 모든 데이터 종류와 상관없이 2진수로 저장
    
    - 예시
        
        [식별자](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/326b3f1b-d3d0-41c0-9362-d389e7eb102f/Untitled.png)
        
        10과 20은 메모리 상의 임의의 위치(메모리 주소)에 기억됨
        
        CPU는 이 값을 읽어들여서 연산 수행
        
        연산 결과로 생성된 숫자 값 30도 메모리 상의 임의의 위치에 저장
        
        메모리에 저장된 숫자 값을 편의상 10진수로 표기하였으나 실제로 2진수로 저장되어 있음
        
- **메모리 사용**
    
    연산 결과를 한번만 사용한다면 문제가 없겠지만 연산 결과 30을 재사용 하고 싶다면 메모리 주소를 통해 연산 결과가 저장된 메모리 공간에 직접 접근해야 함
    
    하지만 메모리 주소를 통해 값에 직접 접근하는 것은 치명적 오류를 발생시킬 가능성 높음
    
    - 예시
        
        운영체제가 사용하고 있는 값을 변경하면 시스템을 멈추게 함
        
    
    동일한 컴퓨터에서 코드를 실행해도 코드가 실행될 때마다 값이 저장되는 메모리 주소가 변경됨
    
    <aside>
    💡 프로그래밍 언어는 기억하고 싶은 값을 메모리에 저장하고 저장된 값을 읽어 들여서 재사용하기 위해서 변수라는 메커니즘을 사용함 즉, 값을 저장하고 참조하기 위해서 값의 위치를 가리키는 상징적인 이름
    
    </aside>
    
- **변수 사용 방법**
    
    변수는 하나의 값을 저장하기 위한 메커니즘으로 여러 개의 값을 저장하려면 여러 개의 변수를 사용해야 함
    
    단 배열이나 객체 같은 자료 구조를 사용하면 관련있는 여러 개의 값을 그룹화해서 하나의 값처럼 사용 가능
    
    - 예시
        
        ```jsx
        let userId = 1
        let userName = 'kim'
        
        let user = { id: 1, name: 'kem' }
        
        let users = [{ id: 1, name: 'kim' }, { id: 2, name: 'lee' }]
        ```
        
    - 예시
        
        ```jsx
        let result = 10 + 20
        ```
        
    
    
    변수이름 : 메모리 공간에 저장된 값을 식별할 수 있는 고유의 이름
    
    변수값 : 변수에 저장된 값
    
    할당 = 대입 = 저장 : 변수에 값을 저장하는 것
    
    참조 : 변수에 저장된 값을 읽어들이는 것
    

### 4.2 식별자

---

- **식별자**
    
    같은 메모리 공간 내에 저장되어 있는 어떤 값을 구별해서 식별할 수 있는 고유의 이름
    
    [식별자](https://developer.mozilla.org/ko/docs/Glossary/Identifier)
    
    식별자는 값 자체가 아니라 어떤 값이 저장되어 있는 메모리 주소를 기억함
    
    변수, 함수, 클래스 등의 이름은 모두 식별자에 해당함 
    
    
    

### 4.3 변수 선언

---

- **변수 선언**
    
    변수를 생성하는 것
    
    값을 저장하기 위한 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것
    
    변수를 사용하기 위해서는 반드시 선언이 필요하며 var, let, const 키워드 사용
    
    - 예시
        
        키워드 뒤에 오는 변수 이름으로 새로운 변수를 선언
        
        변수 이름을 등록하고 값을 저장할 메모리 공간을 확보하는 과정을 거침
        
        ```jsx
        var score
        let score
        const score
        ```
        
- **변수 선언 및 할당 단계**
    
    (1) 선언 단계 : 변수 이름을 등록해서 자바스크립트 엔진에 변수 존재를 알림
    
    (2) 초기화 단계 : 값을 저장할 메모리 공간을 확보하고 암묵적으로 undefined 할당해 초기화함
    

### 4.4 변수 선언의 실행 시점과 변수 호이스팅

---

- **변수 선언의 실행 시점**
    
    자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행됨
    
    자바스크립트 엔진은 소스코드를 한 줄씩 실행하기 전 준비 단계로 소스코드 평가 과정을 먼저 거침
    
    소스코드 평가 과정에서 모든 선언문(변수, 함수 선언문 등) 소스코드를 먼저 찾아내서 실행
    
    소스코드 평가 과정이 끝나면 변수 선언을 포함한 모든 선언문을 제외하고 소스코드를 한 줄씩 실행
    
    <aside>
    💡 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점 즉, 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문
    
    </aside>
    
    - 예시
        
        ```jsx
        console.log(score) // undefined
        var score
        console.log(score) // undefined
        var score = 10
        console.log(score) // 10
        ```
        
- **변수 호이스팅**
    
    변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징
    

### 4.5 값의 할당

---

- **변수값 할당**
    
    선언된 변수에 값을 할당하는 것
    
    변수에 값을 할당할 때는 할당 연산자 ( = ) 사용
    
    할당 연산자는 우변의 값을 좌변의 변수 할당하거나 하나의 문으로 단축 표현 가능
    
    - 예시
        
        ```jsx
        var score
        score = 10
        
        var score = 10
        ```
        
- **변수 선언 및 할당 단계**
    
    (1) 선언 단계 : 변수 이름을 등록해서 자바스크립트 엔진에 변수 존재를 알림
    
    (2) 초기화 단계 : 값을 저장할 메모리 공간을 확보하고 암묵적으로 undefined 할당해 초기화함
    
    (3) 변수값 할당 단계 : 지정된 메모리 공간에 undefined 대신 값을 입력함
    
    ```jsx
    console.log(score) // undefined
    
    var score // 1. 변수 선언
    score = 10 // 2. 변수값 재할당
    
    console.log(score) // 10
    ```
    
    단축문으로 지정하더라도 변수 호이스팅에 의해서 변수 선언과 변수값 할당은 별도로 동작
    
    ```jsx
    console.log(score) // undefined
    
    var score = 10 // 변수 선언과 변수값 할당 
    
    console.log(score) // 10
    ```
    

### 4.6 값의 재할당

---

- **변수값 재할당**
    
    이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당하는 것
    
    현재 변수에 저장된 값을 버리고 새로운 값을 저장하는 것
    
    var 키워드로 선언한 변수는 선언과 동시에 undefined로 초기화 되기 때문에 사실상 재할당임
    
    
    
    - 예시
        
        ```jsx
        var score = 10
        score = 20
        ```
        
- **상수**
    
    값을 재할당 할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아닌 상수라 함
    
    ES6부터 도입된 const 키워드는 재할당이 금지되어 있으므로 상수로 표현할 수 있음
    
- **var / let / const 차이점**
    
    
    |  | var | let | const |
    | --- | --- | --- | --- |
    | 변수 재선언 | 가능 | 불가능 | 불가능 |
    | 변수 재할당 | 가능 | 가능 | 불가능 |
    | 변수 스코프 유효범위 | 함수 레벨 스코프 | 블록 레벨 스코프 | 블록 레벨 스코프 |
    | 변수 호이스팅 방식 | 발생 | 발생/다른방식작동 | 발생/다른방식작동 |
    | 전역 개체 프로퍼티 여부 | 맞음 | 아님 | 아님 |
    - 변수재선언 / 변수재할당
        - 예시 (var)
            
            변수 선언을 여러번해도 에러없이 각기 다른 값 출력 가능
            
            같은 이름의 변수명을 남용할 때 문제가 되므로 주의해서 사용할 것
            
            ```jsx
            var A = "변수 선언"
            console.log(A) // 변수 선언
            
            var A = "변수 재선언"
            console.log(A) // 변수 재선언
            ```
            
        - 예시 (let)
            
            var에서 변수명이 중복될 때 발생하는 에러를 방지하기 위해서 ES6부터 추가됨
            
            ```jsx
            let A = "변수 선언"
            console.log(A) // 변수 선언
            
            let A = "변수 재선언"
            console.log(A) // Uncaught SyntaxError: Identifier 'name' has already been declared
            
            A = "변수 재할당"
            console.log(A) // 변수 재할당
            ```
            
        - 예시 (const)
            
            var에서 변수명이 중복될 때 발생하는 에러를 방지하기 위해서 ES6부터 추가됨
            
            ```jsx
            const A = "변수 선언"
            console.log(A) // 변수 선언
            
            const A = "변수 재선언"
            console.log(A) // Uncaught SyntaxError: Identifier 'name' has already been declared
            
            A = "변수 재할당"
            console.log(A) // Uncaught TypeError: Assignment to constant variable.
            ```
            
    - 변수 스코프 유효범위
        - 예시 (var)
            
            함수 레벨 스코프
            
            함수 내부에 선언된 변수만 지역변수로 한정되어 적용
            
            ```jsx
            function test() {
             var a = 1;
             console.log(a) // 1
            } 
            test(); // 1
            console.log(a) // ReferenceError : a is not defined
            ```
            
            나머지는 모두 전역 변수로 간주
            
            ```jsx
            if (true) {
             var a = 1;
             console.log(a); // 1
            }
             
            console.log(a); // 1
            ```
            
        - 예시 (let / const)
            
            블록 레벨 스코프
            
            코드 블럭에서 선언된 변수도 지역 변수로 취급하여 외부에서 사용 불가
            
            ```jsx
            function test() {
             let a = 1;
             console.log(a); // 1
            }
            console.log(a); // ReferenceError : a is not defined
            ```
            
            ```jsx
            if (true) {
             let a = 1;
             console.log(a); // 1
            }
            
            console.log(a); // ReferenceError : a is not defined
            ```
            
    - 변수 호이스팅
        - 예시 (var)
            
            변수 호이스팅 발생
            
            선언된 변수 a가 앞에서 참조되어도 에러 발생하지 않음 
            
            ```jsx
            console.log(a); // undefined
            
            var a = 1;
            console.log(a); // 1
            ```
            
        - 예시 (let / const)
            
            변수 호이스팅 발생하지만 다른 방식으로 작동함
            
            변수 선언 전에 참조하면 에러 발생
            
            ```jsx
            console.log(a); // ReferenceError : Cannot access 'a' before initialization
            
            let a = 1;
            console.log(a); // 10
            ```
            
            ```jsx
            let a = 1 // 전역 변수 a 선언
            
            if (test) {
             console.log(a) // ReferenceError : Cannot access 'a' before initialization
             let a = 2 // 지역 변수 a 선언
             console.log(a) // 2
             }
            
            console.log(a) // 1
            ```
            
    - 전역 개체 프로퍼티 여부
        
        전역 변수란 스크립트 내에 어디든지 사용할 수 있는 가장 바깥쪽 범위에 있는 변수
        
        var - 전역변수 선언 시 전역 객체의 속성으로 포함
        
        let / const - 전역변수 선언하더라도 전역 객체 속성으로 포함되지 않음
        

### 4.7 식별자 네이밍 규칙

---

- **식별자 네이밍 규칙**
    1. 특수 문자를 제외한 문자, 숫자, 언더스코어(_), 달러 기호($) 사용 가능
    2. 특수 문자를 제외한 문자, 언더스코어(_), 달러 기호($)로 시작해야 함
    3. 숫자로 시작하는 것은 허용하지 않음
    4. 예약어는 식별자로 사용할 수 없음
- **예약어**
    
    
    | await | break | case | catch | class | const |
    | --- | --- | --- | --- | --- | --- |
    | continue | debugger | default | delete | do | else |
    | enum | exprot | extends | false | finally | for |
    | function | if | implements | import | in | instanceof |
    | interface | let | new | null | package | private |
    | protected | public | return | super | static | switch |
    | this | throw | true | try | typeof | var |
    | void | while | with | yield |  |  |
- **네이밍 컨벤션**
    1. 다른 언어를 사용할 수 있지만 유니코드 문자로 명명된 식별자는 바람직하지 않음
    2. 쉼표를 이용하여 여러 개를 한번에 선언할 수 있음 - 가독성때문에 권장X
    3. 변수 선언 목적에 맞게 적절한 변수명을 선택하기 위해 단일 글자는 지양할 것
    4. 변수 명의 맨 앞이나 맨 뒤쪽에 언더스코어(_)를 사용하지 않음 - 생성은 되지만 권장X
    5. this를 변수값으로 사용하지 않아야 하며 필요하다면 화살표 함수나 바인딩 사용할 것
    6. 약어는 모두 대문자 혹은 모두 소문자로 표시할 것 
    7. export 되는 파일 내의 모든 상수는 모두 대문자로 표기할 것
    8. 단수형을 기본으로 사용하되 구분할 때는 복수형을 사용할 것
    9. 줄임말을 사용하지 말 것
    10. 단어 2개를 조합해서 변수명을 지정할 때 두번째 단어의 첫글자를 대문자로 할 것
    - 예시
        
        ```jsx
        var 이름 // 영어를 사용해서 선언할 것
        ```
        
        ```jsx
        var person, $elem, _name, first_name, val1 // 여러개 변수명 한번에 선언 가능
        ```
        
        ```jsx
        var x = 1 // x 변수가 의미하는 바를 알 수가 없음
        ```
        
        ```jsx
        var firstName_ // 언더스코어를 맨앞/맨뒤에 사용하지 말 것
        ```
        
        ```jsx
        // this 사용의 나쁜 예
        function A() {
         const B = this;
         return function () {
          console.log(B);
         }
        }
        
        // this 사용의 좋은 예
        function bar() {
         return () => {
          console.log(this);
         }
        }
        ```
        
        ```jsx
        // 약어 사용의 나쁜 예
        const HttpRequest = [ ... ];
        
        // 약어 사용의 좋은 예
        const HTTPRequest = [ ... ];
        ```
        
        ```jsx
        // export되는 파일 내의 상수 사용의 나쁜 예
        export const MAPPING = {
          KEY: 'value'
        };
        
        //  export되는 파일 내의 상수 사용의 좋은 예
        export const MAPPING = {
          key: 'value'
        };
        ```
        
        ```jsx
        const fistName = "A"
        ```
        
        ```jsx
        const apple = 1
        const apples = 1
        ```
        
    

<aside>
✨ 변수 선언의 과정과 변수의 네이밍 컨벤션을 잘 기억해두자.

</aside>
