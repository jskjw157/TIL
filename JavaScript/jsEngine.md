# JS.engine 🎢
<br/>

## JavaScript 내부 동작 원리 📑
<br/>

```js

/* 자바스크립트는 일반 다른 프로그래밍언어 처럼 순서대로 코드가 실행 되는게 아닌, 바로 실행되는 코드부터 실행된다.

바로 실행할 수 없는 코드 : setTimeout(),  Ajax 요청 코드, 이벤트 리스너

*/
console.log(1+1) //1번
setTimeout(function(){console.log(2+2)}, 1000) //3번
console.log(3+3) //2번

console.log(1+1) //1번
setTimeout(function(){console.log(2+2)}, 0) // 3번(대기가 0초여도 settimeout함수는 무조건 뒤에 실행된다.)
console.log(3+3) //2번
```
<br/>

+ stack에서 코드를 한줄 한줄 실행하면서 변수를 만나면, heap의 공간에 채워 넣고 변수를 사용할 떄 마다 heap을 참조한다.
<br/>

+ 자바스크립트 stack(코드를 실행주는 곳)은 하나이다. (single threaded language)
<br/>

+ 바로 실행이 안되는 코드들은 대기실로가서 대기된다.
<br/>

+ 대기실에서 처리가 완료된 대기 코드들은 완료 순서대로 Queue로 옮겨 가게 된다.
<br/>

+ stack에서 코드실행이 끝나서 stack이 비게되면, 큐에서 순서대로 stack으로 옮겨가서 실행된다. (FIFO = first in first out)
<br/>

+ 10초 이상 걸리는 어려운 연산 코드가(ex : for 반복문안에 어려운 연산) 있으면, stack이 차있으므로 버튼클릭이나 타이머 코드는 계속 대기하게 되서 작동이 안된다.
<br/>

+ 하여 stack을 바쁘게 하지말자!(바쁘면 사용자가 접속시 응답대기중 안내문구가 뜬다.)
<br/>

+ Queue도 바쁘게 하지말자!(너무 많은 이벤트리스너는 과유불급)
<br/>

+ 자바스크립트는 동기적으로 처리된다. (위에서부터 한줄씩 코드가 실행된다.)
<br/>

+ 가끔 자바스크립트는 비동기적인 처리도 한다.(대기실을 거치는 setTimeout, 이벤트 리스너, ajax함수)
<br/>
