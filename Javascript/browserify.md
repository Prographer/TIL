#개요

Nodejs등 서버사이드 문법을 클라이언트 사이드 문법으로 변경해주는 라이브러리
<http://browserify.org/>

#설치
```
npm install browserify -g
```

#사용법
```
browserify -t main.js -o bundle.js
```

만약 ES6문법을 사용 했을 경우 ES5로 변경 해줘야 하는데 그럴경우 [bable](http://babeljs.io/)을 사용하여 트렌스퍼 해준다.

```
//설치
npm install babel -g

//compile
browserify -t bable main.js -o bundle.js
```