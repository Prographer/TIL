mongoose는 NodeJS에서 사용하는 MongoDB접속 ODM(Object Document Mapping) MVC framework 이다.

## 설치
```
npm install mongoose (-save or -g)
```

## Models [link](http://mongoosejs.com/docs/models.html)
user.js
```
 var mongoose = require('mongoose');
 //[schema 참고](http://mongoosejs.com/docs/guide.html)
 var schema= new mongoose.Schema({
     'name' : String,
     'email' : String,
     'isUse' : Boolean
 });

 var User = mongoose.model(
              "user",//name
               schema,//schema
              "users"//collection
            );
 module.exports = User;
```

## Controller
```
var express = require('express');
var router = express.Router();
var user= require('../models/user');

router.get('/',function(req, res){
    user.find({},function(err,docs){
        docs.forEach(function(doc){
            conolse.log(doc);
        });
    });
});
```

## 접속
app.js
```
var mongoose = require('mongoose');
mongoose.connect('mongodb://54.65.87.219/logs');

var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function callback() {
  console.log('connection successful...');
});

```


