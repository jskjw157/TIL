# API ๐
<br/>

## API์ ์ ์
<br/>

+ ํ ํ๋ก๊ทธ๋จ์์ ๋ค๋ฅธ ํ๋ก๊ทธ๋จ์ผ๋ก ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ ๋ฐ๊ธฐ ์ํ ๋ฐฉ๋ฒ
<br/>

## API ์ ์ฉ ์์(node.js)
<br/>

```js

app.get('/detail/:id', function (req, res) { // ์ด๋ถ๋ถ์ด API
  db.collection('์นํฐ').findOne( {_id: parseInt(์์ฒญ.params.id) }, function (์๋ฌ, ๊ฒฐ๊ณผ) { // API ์คํ์ฝ๋
    console.log(๊ฒฐ๊ณผ);
    res.render('detail.ejs', { data: ๊ฒฐ๊ณผ });
 })
 
 ```
<br/>
 
## API ์ ์ฉ ์์(JS fetch API)
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
/* hi.txt ํ์ผ */

{ "id" : "ksdf223", "name" : "gildong:} //jsonํ์(์๋ฐ์คํฌ๋ฆฝํธ ๊ฐ์ฒด ํ์)
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

๐ป๐ป๐ป

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

## API๊ฐ ๊ฐ์ ธ์ผํ  ๋ด์ฉ
<br/>
 
+ (GET ์์ฒญ)comic.naver.com/webtoon/detail?id=318995 
<br/>

+ => 1.์์ฒญ๋ฐฉ์(method)/2.๋ฌด์จ์๋ฃ์์ฒญํ ์ง(endpoint)/3.ํ๋ผ๋ฏธํฐ(์๋ฃ์์ฒญ์ ํ์ํ ์ ๋ณด)
<br/>

## API ์ข๋ฅ
<br/>

+ public APi : ๋๊ตฌ๋ ์ฌ์ฉ๊ฐ๋ฅํ ๊ณต๊ฐ API
<br/>

+ private API : ์ฌ๋ด์์ ๋ชฐ๋์ฐ๋ API
<br/>

+ partner API : ๋ฏธ๋ฆฌ ์ ํด๋ ๋๋ง ์ฐ๋ API
<br/>

