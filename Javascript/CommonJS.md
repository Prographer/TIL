  자바스크립트를 클라이언트 뿐만 아닌 범용적으로 사용 할 수 있도록 정의 하는 그룹([link](http://d2.naver.com/helloworld/12864))
  이 문법을 이용하는 대표적인 프레임웤이 Node.js이다.

## 초간단 문법

exports와 require를 이용하여 사용한다.

- a.js

```
exports.sum = function(a,b){
    return a+b;
};
```

- b.js

```
var b= require('b');
b.sum(10,20);
```





