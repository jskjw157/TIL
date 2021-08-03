
# Functional Programming
<br/>

### 함수형 프로그래밍📚
<br/>

+ 함수형 프로그래밍은 성공적인 프로그래밍을 위해 부수 효과를 미워하고 조합성을 강조하는 프로그래밍 패러다임이다.
<br/>

+ 부수 효과를 미워한다. => 순수 함수를 만든다.📕
  
  + 순수 함수는 부수 효과가 없는 수학적 함수(들어온 인자가 같으면 항상 동일한 결과를 리턴하는 함수)
  
  + 함수가 받은 인자 외에 다른 어떤 외부의 상태에 영향을 끼치지않는 함수
  
  +  리턴값외에는 외부와 소통하는것이 없는 함수
<br/>

+ 조합성을 강조한다. => 모듈화 수준을 높인다.📗

  +  순수함수로 묘듈화수준을 높이게 되면 오류는 적고 안정성은 높아진다.

  + 모듈화 수준이 높다 => 성공적인 프로그래밍이다. WHY? 생산성을 높이고, 재사용성이 높고, 팀워크도 좋고, 기획변경에 대한 대응력도 좋다.
<br/>

#### 순수함수📑
<br/>

+ 순수함수는 언제 실행되도 항상 동일한 값을 리턴하기 떄문에 조합성을 강조 시킬 수 있다
<br/>

+ 순수함수는 언제 평가되도 상관 없기 때문에, 평가시점을 개발자가 다룰 수 있다.
<br/>

+ 순수함수를 다른 함수의 인자로 넘기던가, 서로 다른 쓰레드에 함수를 평가 시켜도 항상 동일한 결과를 리턴하기 때문에 굉장히 안전하고 다루기 쉬운 함수가 된다.
<br/>

+ **함수형 프로그래밍에서는 순수함수를 통해서 조합성을 강조하는 프로그래밍이다.**
<br/>

+ 순수함수를 통해서 조합성을 강조하는 이유는 평가시점을 다루는것을 통해서 다양한 로직등을 만들고, 다양한 이점등을 만들고자하는 컨셉이 있다.

```javascript
        
        /* 순수함수 */
        
        function add(a,b) {
            return a + b;
        }

        console.log(add(10,5));
        console.log(add(10,5));
        console.log(add(10,5));

        /*순수함수가 아닌 함수는 평가시점이 중요하다. c가 변경 되기 전인가 변경 된 후인가가 중요.
        순수함수는 평가시점에 따라 로직이 정해진다.*/
        var c = 10;
        function add2(a,b) {
            return a + b + c;
        }

        console.log(add2(10,5)); //22
        console.log(add2(10,6));
        console.log(add2(10,7));
        c=30;
        console.log(add2(10,5)); //32
        console.log(add2(10,6));
        console.log(add2(10,7));
        
        /* 순수함수가 아닌 함수는 부수효과를 일으키는 함수. 
        부수 효과는 외부의 상태를 변경하는것 또는 들어온 인자의 상태를 집적 변경하는것.
        add3함수는 리턴값 외의 다른 방식으로 외부의 상태에 직접 관여하고 있다. */
        var c = 20;
        function add3(a,b) {
            c=b;
            return a+b;
        }

        console.log('c: ', c);
        console.log(add3(20,30));
        console.log('c: ',c);

        /* add4함수는 순수함수도 아니고, 리턴값도 없고, 실행하면 직접 인자로 들어온 값의 상태를 변경하는 함수
        */
        var obj1 = {val:10};
        function add4(obj, b) {
            obj.val += b;
        }

        console.log(obj1.val);
        add4(obj1, 30);
        console.log(obj1.val);


        // 다시 순수 함수
        // 객체를 다루는 순수 함수
        // 원래있던 값을 그대로 두고, 새로운 값을 만들면서 원하는 값이 변형된 새로운 값을 리턴하는 방식
        // add5함수는 obj1을 받아서 obj1.value를 참조만 할 뿐 값을 변경하는 부분은 없다.
        // obj와 동일하게 생긴 새로운 객체를 리턴하면서, value의 해당하는 부분을 더해진 값으로 만들어서 리턴하고 있다.
        // 인자로 받은 상태를 변경하지 않고, 외부의 상태도 변경하지 않고 있다.
        var obj1 = {val:10};
        function add5(obj, b) {
            return {val : obj.val +b}
        }

        console.log(obj1.val);
        var obj2 = add5(obj1, 20);
        console.log(obj1.val);
        console.log(obj2.val);
        
```
<br/>

***

<br/>

### 일급함수📚
<br/>

+ **함수를 값으로 다룰 수 있다.** 📕

  + 함수를 변수에 담을 수도 있다.

  + 변수에 담은 함수가 값으로 다룰 수 있기때문에, 함수를 다른함수에게 인자로 넘겨저서 그인자로 넘겨진 함수를 다른함수가 실행 할 수 있다.
<br/>

+ 런타임에서 언제나 정의 할수있고, 인자로 보낼 수 있고, 내가 원하는 시점에 들고 다니다가 원할때 평가 할 수 있는 함수
<br/>

```javascript
        /* 일급 함수 */
        //변수에 함수가 담길 수 있다.
        var f1 = function(a) { return a * a; };
        console.log(f1);

        var f2 = add;
        console.log(f2);

        //인자로 일급함수를 받을 수 있다.
        function f3(f) {
        return f();
        }

        console.log( f3(function() { return 10; }) );

        console.log( f3(function() { return 20; }) );

        /* add_maker */
        // add_maker는 함수를 바로 값으로 리턴하고, 그 함수는 변수에 대입된다.
        function add_maker(a) { // 일급함수(값으로 넘긴다.)
        return function(b) { // 순수함수(외부에 있는 변수 a의 값을 참조하지만 변경하지는 않는다.)
            return a + b; // a의 값을 기억하는 클로저함수(function(b))
        }
        }

        var add10 = add_maker(10);

        console.log( add10(20) ); //30

        var add5 = add_maker(5);
        var add15 = add_maker(15);

        console.log( add5(10) );
        console.log( add15(10) );

        // 함수의 평가시점이 언제이든 같은 인자의 값을 입력했을때 같은 결과 값이 출력된다.
        console.log( add10(20) ); // 30


        function f4(f1,f2,f3) {
            return f3(f1()+f2());
            
        }

        console.log(f4(
            function() {return2;},
            function() {return3;},
            function() {return a*a;}
        ))
```
<br/>

***

<br/>

### filter and map
<br/>

+ 함수형 프로그래밍은 값을 직접 변경하지 않고 변형된 새로운 값을 리턴한다.
<br/>

```javascript
var users = [
  { id: 1, name: 'ID', age: 36 },
  { id: 2, name: 'BJ', age: 32 },
  { id: 3, name: 'JM', age: 32 },
  { id: 4, name: 'PJ', age: 27 },
  { id: 5, name: 'HA', age: 25 },
  { id: 6, name: 'JE', age: 26 },
  { id: 7, name: 'JI', age: 31 },
  { id: 8, name: 'MP', age: 23 }
];

// 1. 명령형 코드
  // 1. 30세 이상인 users를 거른다.
var temp_users = [];
for(i=0; i<users.length; i++){
    if(users.age>=30){
        temp_users.push(users[i]);
    }
}

console.log(temp_users);

  // 2. 30세 이상인 users의 names를 수집한다.
var names = [];
for (var i = 0; i < temp_users.length; i++) {
  names.push(temp_users[i].name);
}
console.log(names);

  // 3. 30세 미만인 users를 거른다.
var temp_users = [];
for (var i = 0; i < users.length; i++) {
  if (users[i].age < 30) {
    temp_users.push(users[i]);
  }
}
console.log(temp_users);

  // 4. 30세 미만인 users의 ages를 수집한다.
var ages = [];
for (var i = 0; i < temp_users.length; i++) {
  ages.push(temp_users[i].age);
}
console.log(ages);


// 2. _filter, _map으로 리팩토링

function _filter(list, predi){
  var new_list = [];
  for(var i = 0; i < users.length; i++) {
    if(predi(users[i])){
      new_list.push(users[i]);
    }
  }
  return new_list;
}

function _map(list, mapper){
  var new_list = [];
  for (var i = 0; i < list.length; i++) {
    new_list.push(mapper(lsit[i]));
  }
  return new_list;
}


console.log(_filter(users, function(user) { return user.age >= 30; }));

//filter 함수는 꼭 users배열 뿐 아니라, 다른배열에도 똑같이 적용시킬 수 있다.
console.log(_filter( [1,2,3,4,5], function(num) {return num % 2;}));

// over_30 = 나이가 30 이상인 user 객체 배열
var over_30 = _filter(users, function(user) { return user.age >= 30; });
console.log(over_30);

// names = map함수를 이용해서 user 객체의 이름만 있는 배열 생성
var names = _map(over_30, function(user) {
  return user.name;
});
console.log(names);

// under_30 = 나이가 30 미만인 user 객체 배열
var under_30 = _filter(users, function(user) { return user.age < 30; });
console.log(under_30);

// ages = map함수를 이용해서 user 객체의 나이만 있는 배열 생성
var ages = _map(under_30, function(user) {
  return user.age;
});
console.log(ages);

// map 함수는 꼭 users배열 뿐 아니라, 다른배열에도 똑같이 적용시킬 수 있다.
console.log(_map([1,2,3,4], function(num) {
  return num * 2;
}));


// map함수와 filter함수를 동시에 사용하는 함수형 프로그래밍
// 간결하고, 안정성 높고 테스트가 쉬운 코드
console.log(
_map(_filter(users, function(user){return user.age >= 30;}), 
      function(user){return user.name;})
);
console.log(
  _map(
    _filter(users, function(user) { return user.age < 30; }),
    function(user) { return user.age; }));
```
<br/>

#### 응용형 프로그래밍
<br/>

+ 함수를 인자로 받아서 원하는 시점에 평가하고, 함수가 알고있는 특정한 인자를 적용해나가면서 로직을 완성해 나가는 프로그래밍
<br/>

#### 응용형 함수
<br/>

+ 함수가 함수를 인자로 받아서 원하는 시점에 해당하는 함수가 알고있는 인자를 적용하는 함수가 응용형 함수이다.
<br/>

#### 고차함수
<br/>

+ 함수를 인자로 받거나, 함수를 리턴하거나, 함수안에 인자로 받은 함수를 실행하는 함수
<br/>

```javascript
