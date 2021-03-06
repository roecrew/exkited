# exkited

<img width="100px" height="100px" align="right" src="https://i.imgur.com/t6pgoeD.gif"></img>

<p align="center"><a href="https://exkited.com">exkited.com</a></p>

Simplistic Template Language

Exkited is a minimalistic templating language that lets you generate markup with JavaScript.

## Example: .exkited File

```js
<html>
    <div class="title">
        <@ return data.title @> // A 'data' object may be passed rendering.
    </div>
    <@
        let result = '';
        for(let x=0;x<10;x++) {
            for(let i=0;i<4;i++) {
                for(let j=0;j<4;j++){
                    result += `<div>@{i+j}</div>`;
                }
            }
        }
        return result;
    @>
    <div class="average-price">
        <@ return data.prices.reduce((accum, val) => accum += val) / data.prices.length; @>
    </div>
    <div class="day-of-week">
        <@
            switch(data.dayIdx) {
                case 0:
                return 'Sunday';
                case 1:
                return 'Monday';
                case 2:
                return 'Tuesday';
                case 3:
                return 'Wednesday';
                case 4:
                return 'Thursday';
                case 5:
                return 'Friday';
                case 6:
                return 'Saturday';
            }
        @>
    </div>
</html>
```

## Example: Using include(...)

function include(path)

Parameter "path" is the filepath to the file which you want to include.

Returns a processed string of the given file.

```
...
<@ return include('./views/somefile.exkited'); @>
...
```

## Example: Using as a Standalone

```
npm install exkited
```

```js
const exkited = require('exkited');
...
exkited.renderFile(
    './views/example.exkited',
    { a: 0, dayIdx: 3, prices: [1, 2, 3, 4, 5, 6, 7, 8, 9] },
    (err, rendered) => {
        ...
    }
);
...
```

## Example: Pairing with Express.js

```
npm install exkited express compression
```

```js
const http = require('http');
const express = require('express');
const compression = require('compression');
const app = express();

app.use(compression());
app.set('view engine', 'exkited');
app.set('views', './views');

let server = http.createServer(app).listen(8888, '127.0.0.1');

app.get('/', function(req, res) {
  res.render('basic', {}, function(err, html) {
    res.send(html);
  });
});
```

## Benchmarks

Check them out at <a href="https://exkited.com">exkited.com</a>
