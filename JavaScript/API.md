# API 📚
<br/>

## API의 정의
<br/>

+ 한 프로그램에서 다른 프로그램으로 데이터를 주고받기 위한 방법
<br/>

## API 적용 예시(node.js)
<br/>

```js

app.get('/detail/:id', function (req, res) { // 이부분이 API
  db.collection('웹툰').findOne( {_id: parseInt(요청.params.id) }, function (에러, 결과) { // API 실행코드
    console.log(결과);
    res.render('detail.ejs', { data: 결과 });
 })
 
 ```
<br/>
 
## API 적용 예시(JS fetch API)
<br/>

```js
fetch("hi.txt").then(function(response) {
  response.text().then(function(text) {
    alert(text)
  })
 })
```
<br/>

```txt
/* hi.txt 파일 */

{ "id" : "ksdf223", "name" : "gildong:} //json형식(자바스크립트 객체 형식)
```
<br/>

```js
fetch("hi.json").then(function(response) {
  
  response.json().then(function(data) {
    console.log(data.id)
    console.log(data.name)
  })
 })
```
<br/>

🔻🔻🔻

<br/>

```js
fetch("hi.json").then(function(response) {
  
 return response.json()
 
}).then(function(data) {

  return data.id
}).then(function(data) {
  console.log(data)
})
```
<br/>

## API가 가져야할 내용
<br/>
 
+ (GET 요청)comic.naver.com/webtoon/detail?id=318995 
<br/>

+ => 1.요청방식(method)/2.무슨자료요청할지(endpoint)/3.파라미터(자료요청에 필요한 정보)
<br/>

## API 종류
<br/>

+ public APi : 누구나 사용가능한 공개 API
<br/>

+ private API : 사내에서 몰래쓰는 API
<br/>

+ partner API : 미리 정해둔 놈만 쓰는 API
<br/>

