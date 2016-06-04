# sassをcssに変えてみよう

基本的なタスクの使い方がわかったところで、次はsassをcssに変換してみましょう。  
`gulp-sass`プラグインを使ってsassをcssに変換します。  

## 手順

1. gulpのインストールと、gulp-sassのインストール
1. gulpfile.jsにtaskを記述する
1. gulpを実行する
1. pipe()をつなぎ合わせてみよう

## gulpのインストールと、gulp-sassのインストール

ターミナルを開いて次のコマンドを実行してください。

```
$ npm install --save-dev gulp gulp-sass
```

## gulpfile.jsにtaskを記述する

gulpfile.jsにsassをcssに変換するタスクを記述してみましょう。

```
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass',function(){
  var stream = gulp.src('src/sass/*.scss')
    .pipe(sass())
    .pipe(gulp.dest('dist/css'))
});

gulp.task('default',['sass']);

```

## gulpを実行する

Gulpを実行してみましょう。

```
$ gulp

[22:16:26] Using gulpfile ~/workspace/nodejs/workshop201606/02/gulpfile.js
[22:16:26] Starting 'sass'...
[22:16:26] Finished 'sass' after 10 ms
[22:16:26] Starting 'default'...
[22:16:26] Finished 'default' after 5.63 μs
```

`dist/css/base.css`ディレクトリが生成されているかと思います。

```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

## pipe()をつなぎ合わせてみよう

gulpはpipe()で処理をつなげることが出来ます。  
今回は`sassからcssへ変換`→`cssを圧縮`という手順で実行します。

今回はminifyするにあったって[`gulp-clean-css`](https://github.com/scniro/gulp-clean-css)というプラグインを使います。


```
$ npm install --save-dev gulp-clean-css
```

次にgulpfile.jsを修正しましょう。

```
var gulp = require('gulp');
var sass = require('gulp-sass');
var cleanCSS = require('gulp-clean-css');

gulp.task('sass',function(){
  var stream = gulp.src('src/sass/*.scss')
    .pipe(sass())
    .pipe(cleanCSS())
    .pipe(gulp.dest('dist/css'))
});

gulp.task('default',['sass']);
```

修正が完了したらgulpを実行しましょう

```
$ gulp
[23:37:43] Using gulpfile ~/workspace/nodejs/workshop201606/02/gulpfile.js
[23:37:43] Starting 'sass'...
[23:37:43] Finished 'sass' after 14 ms
[23:37:43] Starting 'default'...
[23:37:43] Finished 'default' after 8.18 μs
```

`dist/css/base.css`を確認するとminifyされていると思います。
