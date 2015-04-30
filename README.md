##1 INSTALL NODE
https://nodejs.org/
####2 INSTALL EXPRESS 
http://expressjs.com/starter/installing.html
* npm init
* npm install express --save
* express . --ejs 
* npm install

######//remove favicon
* npm rm serve-favicon --save
```
>app.js

//var favicon = require('serve-favicon');
```
######//run application to test if no error
* node app.js
* DEBUG=test:* ./bin/www
* DEBUG=test /bin/www
* npm start

####3 INSTALL ANGULARJS

######//create file .bowerrc
```
{
  "directory": "public/bower"
}
```
* npm install bower -g
* bower install angular
* bower install angular-route

```
>view>index.ejs

<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <div ng-app="myApp">
		<div ng-controller="AppCtrl">
			<input ng-model="test">
			{{test}}
		</div>
	</div>
	<script src="/bower/angular/angular.min.js"></script>
	<script src="/bower/angular-route/angular-route.min.js"></script>
	<script src="/javascripts/app/test.js"></script>
  </body>
</html>
```

```
>public>javascripts>app>test.js

(function(){
	angular.module('myApp', [])
    	.controller('AppCtrl', ['$scope', '$http', function($scope, $http) {
            $scope.test = 'sample';
        }]);
})();
```
####4 INSTALL BOOTSTRAP
* bower install bootstrap

```
>view>index.ejs

<link rel='stylesheet' href='/bower/bootstrap/dist/css/bootstrap.min.css' />
<link rel='stylesheet' href='/bower/bootstrap/dist/css/bootstrap-theme.min.css' />
```
####5 INSTALL MONGODB
######//download mongdb
https://www.mongodb.org/downloads
######//run mongodb
* cd D:\mongo\bin
* mongod

######//modify mongodb
* cd D:\mongo\bin
* mongo

######//show all db
* show dbs

######//switch db
* use test

######//insert data
* db.test.insert({name: 'Tom', email: 'tom@testemail.com', number: '(444)444-4444'})
* db.test.find().pretty()


####6 ROUTING
```
>app.js

var test = require('./routes/test');

app.use('/test', test);
```

```
>routes>test.js

var express = require('express');
var router = express.Router();

/* GET users listing. */
router.get('/', function(req, res, next) {
  	res.render('index', { title: 'Express' });
});

module.exports = router;
```
####7 TEST ANGULARJS CONNECTION IN NODE.JS ROUTE
```
>public>javascripts>app>test.js

.controller('AppCtrl', ['$scope', '$http', function($scope, $http) {
	$http.get('/test').success(function(response){
        	console.log('success request');
        });
}]);
```

```
>routes>test.js

router.get('/', function(req, res, next) {
  	console.log('get request');
});
```
####8 CONNECT NODE.JS IN MONGODB USING MONGOJS
* npm install mongojs --save
```
>routes>test.js

var mongojs = require('mongojs');
var db = mongojs('test', ['test']);

/* GET users listing. */
router.get('/', function(req, res, next) {

	db.test.find(function (err, docs) {
        	console.log(docs);
        	res.json(docs);
    	});	
});

```
######//ANGULARJS GET DATA FROM NODE
```
>public>javascripts>app>test.js

.controller('AppCtrl', ['$scope', '$http', function($scope, $http) {
            $http.get('/test').success(function(response){
            	console.log('success request');
            	console.log(response);
            });
}]);
```
