# gulp-shell

[![NPM version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Coveralls Status][coveralls-image]][coveralls-url]
[![Dependency Status][david-dm-image]][david-dm-url]

[npm-url]:         https://badge.fury.io/js/gulp-shell
[npm-image]:       https://badge.fury.io/js/gulp-shell.png
[travis-url]:      https://travis-ci.org/sun-zheng-an/gulp-shell
[travis-image]:    https://travis-ci.org/sun-zheng-an/gulp-shell.png?branch=master
[coveralls-url]:   https://coveralls.io/r/sun-zheng-an/gulp-shell
[coveralls-image]: https://coveralls.io/repos/sun-zheng-an/gulp-shell/badge.png?branch=master
[david-dm-url]:    https://david-dm.org/sun-zheng-an/gulp-shell
[david-dm-image]:  https://david-dm.org/sun-zheng-an/gulp-shell.png?theme=shields.io

> A handy command line interface for gulp

## Installation

```shell
npm install --save-dev gulp-shell
```

## Usage

```js
var gulp  = require('gulp')
var shell = require('gulp-shell')

gulp.task('example', function () {
  return gulp.src('*.js')
    .pipe(shell([
      'echo  <%= file.path %>',
      'ls -l <%= file.path %>'
    ]))
})
```

If you just want to execute a series of commands only once, starting the stream with `gulp.src('')` should do the trick.

Or you can use this shorthand:

```js
gulp.task('shorthand', shell.task([
  'echo hello',
  'echo world'
]))
```

Note: All the commands will be executed in an environment where `PATH` prepended by `./node_modules/.bin`, allowing you to run executables in your Node's dependencies.

## API

### shell(commands, options) or shell.task(commands, options)

#### commands

type: `Array` or `String`

A command can be a [template][] which can be interpolated by some [file][] info (e.g. `file.path`).

[template]: http://lodash.com/docs#template
[file]:     https://github.com/wearefractal/vinyl

#### options.ignoreErrors

type: `Boolean`

default: `false`

By default, it will emit an `error` event when the command finishes unsuccessfully.

#### options.quiet

type: `Boolean`

default: `false`

By default, it will print the command output.

#### options.cwd

type: `String`

default: `null`

Sets the current working directory for the command.
