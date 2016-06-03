# gulp-watchでファイルを監視しよう！

今回はgulp-watchを使ってファイルに変更があったら即gulpのタスクを実行する事を行います。
複数のjsファイルを一つのファイルにまとめて出力してみましょう。

使用するライブラリは`gulp-concat`を利用します。

## 手順

1. gulpとプラグインのインストール
1. gulpfile.jsにtaskを記述する
1. gulp-watchの設定をしよう

## 1. gulpとプラグインのインストール

```
$ npm install --save-dev gulp gulp-concat
```

## 2. gulpfile.jsにtaskを記述する

前回のサンプルを元に自分で書いてみましょう。  
`src/js/alert.js`と`src/js/alert2.js`をつなぎあわせます。  
つなぎあわせた後に出力するファイル名は`alert.js`とします。  

出力先は`dist/js`となります。

タスク名は`js-concat`にしましょう。

## 3. gulp-watchの設定をしよう

デフォルトタスクを以下のように修正してください。

```
// gulpfile.js
...

gulp.task("watch", function(){
  gulp.watch('./src/js/*.js', ['js-conncat']);
});

gulp.task('default',['js-conncat','watch']);
```

適当にalert1.jsかalert2.jsを変更してみてください。
