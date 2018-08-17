# kosen14s-member

kosen14sのメンバー紹介ページを作りました。

> A Vue.js project
used : vue-cli webpack-simple

## Github pagesで公開したい誰か助けて

 `npm run dev` だと見れる。
github pagesで公開しようと思ってたんだけど、buildしてもindex.htmlがbuild.jsを引っ張ってきてくれない。
現在のwebpackの設定が、コンパイル時にパスをうまく付けてくれてないみたいなんだけど、どう変えたらいいかわからん。

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).

## 機能
* メンバーの表示
    * メンバーはJSONファイルを記述することで自分の自己紹介文が追加できます。
    * 自分のアイコン画像、出身学校名、生息地などが入力できますが、公開したくない情報などは消すことができます。JSON内の値を `null` にすることで、そのプロパティが表示されなくなります。
    * 自分の持っているSNSなどのアカウントにアクセスできるボタンを付けられます。自分のサイト,twitter,facebook,instagram,github,tumblr,自分のブログページ,youtubeのリンクに対応しています。
    * 自己紹介としてコメントが記述できます。改行にも対応しています。
    * 出没チャンネルを設定できます。kosen14sのSlackには様々なチャンネルがあり、それぞれが好きなチャンネルで自由に会話しています。しかし14sへの新規加入者が、どのチャンネルに入ればいいかが分かりづらいので付けた機能です。
* 検索機能
    * メンバーの名前と学校名、生息地、コメント内からキーワード検索します。
    * 大文字と小文字の違いも判別されます。
    * スペースキーを使用したAND検索はできません。
* 表示数指定
    * 検索の隣のボタンでデフォルトの表示件数を変えられます。
    * メンバーのリストの最後に追加で3人分を読み込むボタンがあります。
* チャンネルタグでフィルタリング
    * 各メンバー欄の出没チャンネルの任意のチャンネル名をクリックすると、そのチャンネルを出没チャンネルとして登録しているメンバーだけが表示されます。
    * 複数のチャンネルでフィルタをかけることもできます。
* 表示数の表示
    * 検索やフィルタリングによりヒットした件数のうち、現在何人を表示しているかを示しています。
