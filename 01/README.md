# タスクを動かしてみよう

まずは、Gulpのタスクを動かすところまで、やってみましょう。  
※gulp-cliは入っているものとします。

## 手順

1. gulpのインストール
1. gulpfile.jsにtaskを記述する
1. gulpを実行する
1. defaultについて
1. タスクからタスクを実行してみましょう。

## 1. gulpのインストール

Gulpをインストールしましょう。
ターミナルを開いて次のコマンドを実行してください。

```
$ npm install --save-dev gulp
```

## 2. gulpfile.jsを作成しましょう。

Gulpのタスクはgulpfile.jsに記述します。  

```
// gulpfile.js

var gulp = require('gulp');

gulp.task('test',function(){
  console.log("run gulp task");
});

```

## 3. gulpを実行する

gulpコマンドを使ってgulpを実行します。  
正しく設定できていれば`run gulp task`と表示されるます。

```
$ gulp test
[21:42:05] Using gulpfile ~/workspace/nodejs/workshop201606/01/gulpfile.js
[21:42:05] Starting 'test'...
run gulp task
[21:42:05] Finished 'test' after 96 μs
```

## 4. defaultについて

タスク名を`default`を指定すると`gulp`コマンド実行時にタスク名を指定しない場合に実行されます。

```
// gulpfile.js

var gulp = require('gulp');

gulp.task('default',function(){
  console.log("run gulp default task");
});
```

gulpコマンドを実行してみましょう。

```
$ gulp
[21:47:47] Using gulpfile ~/workspace/nodejs/workshop201606/01/gulpfile.js
[21:47:47] Starting 'default'...
run gulp default task
[21:47:47] Finished 'default' after 111 μs
```

## 5. タスクからタスクを実行してみましょう。

Gulpではタスクからタスクを実行することができます。

```
// gulpfile.js
var gulp = require('gulp');

gulp.task('test',function(){
  console.log("run gulp task");
});

gulp.task('default',['test']);
```

他にも、指定したタスクの後に実行させる事も出来ます。

```
// gulpfile.js
var gulp = require('gulp');

gulp.task('test',function(){
  console.log("run gulp task");
});

gulp.task('default',['test'],function(){
    console.log("run gulp task default");
});
```
