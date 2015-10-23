# Full Stack Angular 2

## Link
http://fullstackangular2.com/

## Why
* save time
* sell one technology stack
  * less contention
  * less political games
  * ...
* remove duplication

## JS
Much more powerful nowadays and the trend will continue over the years:
* ES2015
* ES2016
* ...

## Dependency injection
Reuse code across client & server sides through DI.

Configure the Angular injector depending on whether we run on the client or on the server. This can be done at compile time

## Universal rendering
Your angular 2 app -> Application Layer -> Rendering Layer (DomRenderer VS ServerDomRender)

Steps:
* write client-side Angular 2
* install the server-side plugin

Demo notes:
* different file for the App class and the boostrap code (import App + bootstrap)
* server bootstrap code:
```
ìmport * as express from 'express';
import {ng2engine} from 'angular2-universal-preview';

let app = express();

import {App} from './src/app';

app.use(express.static(__dirname));
app.use('/', function(req, res){
    res.render('index', { App });
});

app.engine('.ng2.html',ng2engine);
app.set('views', __dirname);
app.set('view engine', 'ng2.html')

app.listen(3000, () => {
    console.log('Server started');
});
```
