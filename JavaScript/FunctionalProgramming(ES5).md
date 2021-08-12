
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


         
         /* 다시 순수 함수
         
         객체를 다루는 순수 함수
         
         원래있던 값을 그대로 두고, 새로운 값을 만들면서 원하는 값이 변형된 새로운 값을 리턴하는 방식
         
         add5함수는 obj1을 받아서 obj1.value를 참조만 할 뿐 값을 변경하는 부분은 없다.
         
         obj와 동일하게 생긴 새로운 객체를 리턴하면서, value의 해당하는 부분을 더해진 값으로 만들어서 리턴하고 있다.
         
         인자로 받은 상태를 변경하지 않고, 외부의 상태도 변경하지 않고 있다. */
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

### filter and map ⏱
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
  _map(_filter(users, function(user) { return user.age < 30; }),
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

***

<br/>

### each ⏱
<br/>

```javascript

// each로 _map, _filter 중복 제거

// each가 적용된 filter
function _filter(list, predi) {
    var new_list = [];
    _each(list, function(vla){ //each함수의 for문의 list[i]를 인자로 받아 매개변수 val의 대입
        if (predi(vla)) 
            new_list.push(vla);
    });
    return new_list;
}


//  each가 적용된 map
function _map(list, mapper) {
    var new_list = [];
    _each(list, function(val){ // each함수의 for문의 list[i]를 인자로 받아 매개변수 val의 대입
        new_list.push(mapper(val));
    });
    return new_list;
}

//for (var i = 0; i < list.length; i++)부분과 list[i]부분의 중복을 제거 해주는 each 함수
function _each(list, iter) {
    for (var i = 0; i < list.length; i++) {
        iter(list[i]);
    }
    return list;
}
```
<br/>

***

<br/>

### 다형성 📚
<br/>

#### 외부 다형성 📕
<br/>

+ 객체 지향 프로그래밍

  + 객체지향 프로그래밍은 메소드가 해당하는 클래스에 준비되어 있지않은 메소드는 사용할 수 없다.
  
  + -> 다형성을 지원하기가 어렵다.

  + 데이터가 먼저 나오는 프로그래밍은 데이터가 있어야 메소드가 생긴다.

  +  객체지향은 평가의 순서가 더 중요하다. 반드시 해당하는 객체가 생겨야 기능을 수행한다
<br/>

```javascript

//array 객체에 map과 filter 메소드가 정의 되어 있다.
console.log(
  [1, 2, 3, 4].map(function(val) {
    return val * 2;
  })
);

console.log(
  [1, 2, 3, 4].filter(function(val) {
    return val % 2;
  })
);
```
<br/>

```javascript

//document.querySelectorAll()의 실행 결과는 array가 아닌 array_like 객체
console.log(document.querySelectorAll('*'));
```
<br/>

```javascript

/* 메소드는 해당클래스의 정의 되어 있기 때문에, 해당 클래스의 인스턴스가 아니면 사용할 수 없다.

array가 아닌 array_like 객체이기 때문에 map이라는 메소드가 준비 되어 있지 않다.
 -> 실행결과 : 오류 */
console.log(document.querySelectorAll('*').map(function(node){
  return node.nodeName
})
);
```
<br/>

+ 함수형 프로그래밍

  + 함수가 기준인 함수형 프로그래밍은 함수를 먼저 만들고 그 함수에 맞는 데이터를 구성해서 함수에 적용한다.

  + -> 다형성이 높다. 유연하고 실용적이다.

  + 함수가 먼저 나오는 프로그래밍은 데이터가 있기 전부터 함수가 있다.

  + 함수 자체는 혼자 먼저 존재하기 때문에 데이터가 생기지 않더라도 평가시점이 상대적으로 유연하다.
<br/>

```javascript

/* querySelectorAll(array_like 객체)의 준비 되어있지 않은 Map(메소드)을 함수형 프로그래밍으로 전환해서 사용할 수 있다.

배열이 아니어도 length가 있고, length에 맞는 값들이 담겨저있는 key-value쌍의 객체라면 모두 동작이 가능하다. */
console.log(
  _map(document.querySelectorAll('*'), function(node) {
    return node.nodeName;
  })
);
```
<br/>

#### 내부 다형성 📗
<br/>

+ 내부의 다형성은 predi, iter, mapper 같은 보조함수가 책임을 진다.
<br/>

+ 보조함수의 함수명은 실행하는 기능에 맞는 이름으로 한다.
<br/>

+ 보조함수는 개발자가 넘기는 배열안에 어떤값이 들어있어도 다 수행 할수 있게 만드는 역할을 한다.

  + -> 내부 다형성이 높아진다.
<br/>

***

<br/>

### curry and curryr 🎰
<br/>

#### curry ⏱
<br/>

+  필요한 인자를 모두 채울 떄 까지, 인자를 적용해 나가다가 모든 인자 갯수가 채워지면 본래의 함수를 실행하는 함수
<br/>

```javascript

// 삼항연산자 적용 전 curry 함수
function _curry_(fn) {
  return function (a, b) {
      if (arguments.length == 2) return fn(a, b); // 입력받은 인자가 2개일 경우 fn함수를 바로 실행
            return function (b) {
              return fn(a, b);
            }
  }
}


// 삼항연산자 적용 후 curry 함수
function _curry(fn){
  return function(a,b){
    return arguments.length == 2 ? fn(a,b) : function(b){ return fn(a,b);};
    }
}

// curry 적용 전 일반함수
var add_o = function(a,b) {
  return a+b;
}

console.log( add_o(1, 2) );


// curry 적용 함수 (덧셈)
var add = _curry(function(a, b) {
  return a + b;
});

var add10 = add(10);
var add5 = add(5);
console.log( add10(5) );
console.log( add(5)(3) );
console.log( add5(3) );
console.log( add(10)(3) );

//실행이 안되고 함수가 리턴
console.log( add(1, 2) );


// curry 적용 함수 (뺄셈)
var sub = _curry(function(a,b) {
  return a-b;
});


console.log( sub(10, 5) );



/*  sub함수의 표현이 좋지 못하다.
 
-> sub10 함수가 되었다는건, 들어오는 인자 5에 sub10 함수를 적용하는 것이다. 
 
-> 그렇다면 5-10이 되어야 더 어울린다.
 
-> 이경우에는 curryr 함수가 더 어울린다. */
var sub10 = sub(10);
console.log( sub10(5) ); // 결과 5, 어울리는 결과 -5
```
<br/>

#### curryr ⏱
<br/>

+ 오른쪽부터 인자를 적용해나가는 curry right 함수
<br/>

```javascript

function _curryr(fn) {
  return function(a,b) {
    return arguments.length == 2 ?  fn(a,b) : function(b){return fn(b,a);};
  } 
} 

// curryr 적용 함수 (뺄셈)
var sub = _curryr(function(a,b) {
  return a-b;
});

var sub10 = sub(10);
console.log( sub10(5) ); // 결과 -5
```
<br/>

***

<br/>

### get ⏱
<br/>

+ get 함수 : object에 있는 값이 null이 아닌지 확인해서, 그값을 안전하게 참조하는 함수.
<br/>

```javascript
function _get(obj, key) {
  return obj == null ? undefined : obj[key] ;
}

//정상 실행
var user1 = users[0];
console.log(user1.name);
console.log(_get(user1,'name'));

// undefined
console.log(_get(user[10],'name'));

// curryr을 적용한 get함수
var _getr = _curryr( function(obj, key) {
  return obj == null ? undefined : obj[key] ;
});


//정상 실행
console.log(_get(user1,'name'));
console.log(_getr('name')(user1));


//객체에 상관 없이 key가 'name'인 vaule를 꺼내는 함수
var get_name = _getr('name');


//다른 객체를 넣어도 정상 동작한다.
console.log(get_name(user1));
console.log(get_name(users[3]));
console.log(get_name(users[4]));

console.log(
  _map(
    _filter(users, function(user) { return user.age >= 30; }),
    _getr('name'))); // <- function(user){return user.name;}
    

/* _map 함수에서 _getr('name')인 인자가 실행되는 원리 */
    
function _curryr(fn) {
  return function(a,b) {
    return arguments.length == 2 ?  fn(a,b) : function(b){return fn(b,a);};
  } 
} function(a,b)인 _getr('name') 에서 받아오는 인자가 하나이기때문에 function(b){return fn(b,a);};가 실행되므로  
fn(b,a)에 _get함수인 function(obj, key) {return obj == null ? undefined : obj[key] ;}가 대입

-> function(b){return function(key, obj) {return obj == null ? undefined : obj[key] ;};} 


function _map(list, mapper) {
  var new_list = [];
  _each(list, function(val){
    new_list.push(mapper(val));
  });
  return new_list;
} map 함수에서 mapper 값에 _getr('name')함수를 대입, 그 후 each함수의 function(val){new_list.push(mapper(val));}인자 에서 mapper안에 대입되서 실행
    
-> _each(list, function(val){ new_list.push(function(b){return function(obj, key) {return obj == null ? undefined : obj[key] ;};});})


function _each(list, iter) {
 for (var i = 0; i < list.length; i++) {
   iter(list[i]);
  }
 return list;
} 에서 다시 iter함수에 대입 되고, iter에 list[i]를 인자로 받아 실행
    
->
for (var i = 0; i < list.length; i++) {
  function(list[i]){ new_list.push(function(b){return function(obj, key) {return obj == null ? undefined : obj[key] ;};});}
} 
```
<br/>

***

<br/>

### reduce ⏱
<br/>

+ 축약하는 함수
<br/>

+ 재귀함수
<br/>

+ 원래 들어온 자료와 다른 축약된 새로운 자료를 만들기 위해 사용하는 함수
<br/>

```javascript

var slice = Array.prototype.slice; // 배열의 메소드인 slice함수의 본연의 기능을 대입

/* rest 함수 : 인자로 들어온 array_like를 array로 변환 후 slice 함수를 사용하는 함수 */

function _rest(list, num) {
  return slice.call(list, num || 1); // array가 아닌 array_like이여도 call함수로 사용할 수 있게 해줌
} // 인자로 받은 num값의 수만큼 배열의 값을 제거 후 새로운 배열로 리턴


function _reduce(list, iter, memo) {
  if (arguments.length == 2 ) { // 받은 인자가 2개 일 경우  초기값(memo)에 값을 대입해주고, 그값을 배열에서 제거
      memo = list[0];
      list = _rest(list);
  }
  _each(list, function(val) {
    memo = iter(memo , val);
  });
  return memo;
}


console.log(
  _reduce([1,2,3,4], function(a,b) {return a+b;}, 0)); //10

//reduce 함수 내부
/* memo = add(0,1);
memo = add(memo, 2);
memo = add(memo, 3);
return memo;

add(add(add(0,1),2),3); */

console.log(
  _reduce([1, 2, 3], add, 10)); // 16


console.log(
  _reduce([1, 2, 3], add)); // 6
// add(add(1,2),3);

console.log(
  _reduce([1, 2, 3, 4], add, 10)); // 20
```
<br/>

#### slice ⏱
<br/>

+ 입력한 인자값의 수 만큼 배열의 맨앞의 값이 제외된 새로운 배열을 리턴하는 함수
<br/>

```javascript

var a =[1,2,3];
a.slice(1); // [2,3]
a.slice(2); // [3]

var a = document.querySelectorAll('*');
a.slice(1); // array_like라서 실행 오류

var slice = Array.prototype.slice;
slice.call(a,2);

var a = { 0: 1, 1: 20, 2: 30, length: 3};
slice.call(a,1);
```
<br/>

***

<br/>

### pipe ⏱
<br/>

+ 인자로 받은 함수들로 연속 실행할 수 있는 함수를 리턴하는 함수.
<br/>

+ pipe는 reduce의 특화된 버전.
<br/>

+ pipe는 redude로 함수들 이라는 배열을 통해서, 인자를 연속적으로 적용한 최종결과로 축약하는 함수.
<br/>

+ pipe는 연속적으로 함수를 실행해줄때 사용하는 함수.
<br/>

```javascript

function _pipe() {
  var fns = arguments;
  return function(arg) { //arg는 pipe함수 실행시 받아오는 인자값
    return _reduce(fns, function(arg, fn) {return fn(arg);}, arg)
  }
}


// 1. pipe 함수에 인자로 함수들을 대입.
var f1 = _pipe(
  function(a) { return a + 1; },
  function(a) { return a * 2; },
  function(a) { return a * a; });

// 2. 함수들을 대입한 pipe함수(f1)에 인자로 일반적인 값을 대입.
console.log( f1(1) );
```
<br/>

### go ⏱
<br/>

+ 즉시 실행되는 pipe 함수
<br/>

+ 첫번째 인자는 일반적인 인자로 받고, 두번째 인자부터 함수들을 받아서 결과를 바로 만드는 함수
<br/>

```javascript

function _go(arg) {
  var fns = _rest(arguments);
  return _pipe.apply(null, fns)(arg);
}


// go 적용 예
_go(1,
  function(a) { return a + 1; },
  function(a) { return a * 2; },
  function(a) { return a * a; },
  console.log);


/* users에 _go 적용 */


// go 함수 적용 전
console.log(
  _map(
    _filter(users, function(user) { return user.age >= 30; }),
    _get('name')));

console.log(
  _map(
    _filter(users, function(user) { return user.age < 30; }),
    _get('age')));


// go 함수 적용 후
_go(users,
  function(users) { //users를 인자로 받아 사용
    return _filter(users, function(user) {return user.age >= 30;});
  },
  function(users){ //users를 인자로 받아 사용
    return _map(users, _get('name'));
  },
  console.log);


// go 함수 적용
_go(users,
  function(users) { //users를 인자로 받아 사용
    return _filter(users, function(user) {return user.age < 30;});
  },
  function(users){ //users를 인자로 받아 사용
    return _map(users, _get('age'));
  },
  console.log);
  
  
  // map과 filter에 curryr함수 적용
  var _map = _curryr(_map),
    _filter = _curryr(_filter);


// go함수에 curryr함수 가 적용된 map과 filter를 적용
_go(users,
  _filter(function(user) { return user.age >= 30; }), // curryr함수를 적용 했기 때문, 인자를 하나 받아서  function(b){return fn(b,a);}를 리턴
  _map(_get('name')), // function(b){return fn(b,a);}를 리턴
  console.log);


// 화살표 함수 적용
_go(users,
  _filter(user => user.age < 30),
  _map(_get('age')),
  console.log);
```
<br/>

