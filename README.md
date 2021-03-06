[gulp](https://github.com/wearefractal/gulp)-connect  [![NPM version][npm-image]][npm-url] [![Downloads][downloads-image]][downloads-url] [![Travis][travis-image]][travis-url]
==================


> Gulp plugin to run a webserver (with LiveReload)

## Install

```
npm install --save-dev gulp-connect
```


## Usage

```js
var gulp = require('gulp'),
  connect = require('gulp-connect');

gulp.task('connect', function() {
  connect.server();
});

gulp.task('default', ['connect']);
```


#### LiveReload
```js
var gulp = require('gulp'),
  connect = require('gulp-connect');

gulp.task('connect', function() {
  connect.server({
    root: 'app',
    livereload: true
  });
});

gulp.task('html', function () {
  gulp.src('./app/*.html')
    .pipe(connect.reload());
});

gulp.task('watch', function () {
  gulp.watch(['./app/*.html'], ['html']);
});

gulp.task('default', ['connect', 'watch']);
```

#### Multiple server

```js
var gulp = require('gulp'),
  stylus = require('gulp-stylus'),
  connect = require('gulp-connect');

gulp.task('connectDev', function () {
  connect.server({
    root: ['app', 'tmp'],
    port: 8000,
    livereload: true
  });
});

gulp.task('connectDist', function () {
  connect.server({
    root: 'dist',
    port: 8001,
    livereload: true
  });
});

gulp.task('html', function () {
  gulp.src('./app/*.html')
    .pipe(connect.reload());
});

gulp.task('stylus', function () {
  gulp.src('./app/stylus/*.styl')
    .pipe(stylus())
    .pipe(gulp.dest('./app/css'))
    .pipe(connect.reload());
});

gulp.task('watch', function () {
  gulp.watch(['./app/*.html'], ['html']);
  gulp.watch(['./app/stylus/*.styl'], ['stylus']);
});

gulp.task('default', ['connectDist', 'connectDev', 'watch']);

```

## API

#### options.root

Type: `Array or String`
Default: `Directory with gulpfile`

The root path

#### options.port

Type: `Number`
Default: `8080`

The connect webserver port

#### options.host

Type: `String`
Default: `localhost`

#### options.https

Type: `Boolean`   
Default: `false`

#### options.livereload

Type: `Object or Boolean`
Default: `false`

#### options.livereload.port

Type: `Number`
Default: `35729`

#### options.fallback

Type: `String`
Default: `undefined`

Fallback file (e.g. `index.html`)

#### options.middleware

Type: `Function`
Default: `[]`

```js
gulp.task('connect', function() {
  connect.server({
    root: "app",
    middleware: function(connect, opt) {
      return [
        // ...
      ]
    }
  });
});
```

## Contributors

[AveVlad](https://github.com/AveVlad) and [schickling](https://github.com/schickling)


[npm-url]: https://npmjs.org/package/gulp-connect
[npm-image]: https://badge.fury.io/js/gulp-connect.svg
[travis-url]: https://travis-ci.org/AveVlad/gulp-connect
[travis-image]: https://travis-ci.org/AveVlad/gulp-connect.svg
[downloads-url]: https://github.com/AveVlad/gulp-connect/
[downloads-image]: http://img.shields.io/npm/dm/gulp-connect.svg
