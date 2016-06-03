# Webサーバを動かそう！

gulpでwebサーバを動かす事も出来ます。  
apacheもnginxもいらないんです。  

今回はECTを利用して、htmlの使い回しなども

## 手順

1. gulpとプラグインのインストール
1. ECTについて
1. gulpfile.jsにectからHTMLに変換するtaskを記述する
1. gulp-webserverを使ってみる
1. gulp-watchの設定

## 1. gulpとプラグインのインストール

gulp,gulp-ect,gulp-webserverをインストールします。  

```
$ npm install --save-dev gulp gulp-ect gulp-webserver
```

## 2. ECTについて

ECTはJavaScriptのテンプレートエンジンです。  

以下の機能を持ってます。

- Inheritance（内容の継承）
- Partials（別ファイルを読み込み、include）
- Blocks（プレースホルダ）
- Conditions（条件分岐）
- Loops（ループ処理）

他の機能については[公式サイト](http://ectjs.com/)を見ましょう。

ECT使うとヘッダー・フッターの共通化が楽になったり、変数が使えるようになるのでHTMLを作るときに便利です。

## 3. gulpfile.jsにectからHTMLに変換するtaskを記述する

ectのファイルは`index.ect`のディレクトリを`gulp.src`のターゲットにすればいいので
`gulp.src('./src/ect/*.ect')`となります。

```
var gulp = require('gulp');
var ect = require('gulp-ect');

gulp.task('ect',function(){
  gulp.src('./src/ect/*.ect')
    .pipe(ect({data: function(filename, cb){
      cb({
        projectName: "test",
        menuList: {
          "about" : "/about.html",
          "2about": "/about.html"
        }
      });
    }}))
    .pipe(gulp.dest("dist/"))
});

gulp.task('default',['ect']);

```

## 4. gulp-webserverを使ってみる

gulpfile.jsにwebserverの設定をしていきます。
まずは、gulp-webserverをrequireします。

```
var webserver = require('gulp-webserver');
```

次にwebserver用のタスクを書きます。

```
gulp.task('webserver', function() {
  gulp.src('dist/')
    .pipe(webserver({
      livereload: true,
      open: true
    }));
});
```

最後にdefaultタスクにwebserverタスクを追記しましょう。

```
gulp.task('default',['ect','webserver']);
```

## 5. gulp-watchの設定

前回同様にgulp-watchの設定をしましょう。

```
gulp.task('watch', function(){
  gulp.watch('src/ect/*.ect',['ect']);
})
```

今回はファイルが更新されたら画面もリロードするようにしたいです。  
とういうことで以下のように書き換えてみましょう。

```
gulp.task('watch', function(){
  gulp.watch('src/ect/*.ect',['ect'],function(){
    webserver.reload();
  });
})
```

これでectファイルを更新したら、自動的にBrowserのリロードまで行われます。
