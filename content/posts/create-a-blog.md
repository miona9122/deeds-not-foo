---
title: "Blogサイトを作る"
date: 2021-09-20T09:25:51+09:00
draft: false
categories: ['IT']
---

## 概要

学んだことをアウトプットをすることで、何が理解出来ているのか或いは出来ていないのかがわかるというメリットがあると言います。
私はどうも物事をアウトプットするのが苦手なので、難しいブログサイトやコミュニケーションサイトだとすぐに挫折してしまうのです。
というわけで、簡単に静的サイトを作成できるHugoを使って今回は頑張っていこうという感じです。

## Hugo

HugoはGolangで書かれたWebサイトジェネレーターで、コンテンツをHTML, Markdownファイルで記述することが出来ます。
サイトのデザインは[Hugo Themes](https://themes.gohugo.io/)から選択でき、サブモジュールを追加するだけで反映が可能です。
面倒くさいことはhugoコマンドで簡易化できるので、そこも楽ちんですね。

公式サイト：https://gohugo.io/

## 導入手順

### hugoをインストールする

実際行った作業手順についてです。
私はmacOSを利用しているので、brewコマンドでcliのインストールを行いました.

```
$ brew install hugo
```

一応バージョンも

```
$ hugo version
hugo v0.88.1+extended darwin/arm64 BuildDate=unknown
```

### ページを作成する

そして早速、大枠を作っていきます。

```
$ hugo new site deeds-not-foo
```

Congratulations! サイトできましたよ!と言われると思うので次はテーマを入れていきます。
ちなみに現状でサーバーを立ち上げると、何も準備していないので真っ白なページが表示されます。

## テーマを入れる

テーマを入れる方法は、すでに作成してくれているものを使うかと自分で作るかの二種類があります。
今回は楽に作りたいがテーマなのでDoItというテーマを引っ張ってきました。

Hugo Themes：https://themes.gohugo.io/

DoIt内にある手順を参考に実行していきます。
DoItのgitからzipファイルを用いて行う方法もありますが、あえてそうする必要もないので`git submodule`でやっていきます。

```
$ git init
$ git submodule add https://github.com/HEIGE-PCloud/DoIt.git themes/DoIt
```

config.toml でテーマを適用するために必要な情報を追加していきます。
初期はこんな感じでした。

```
$ cat config.toml
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
```

DoItに必要な最低限の追加情報はthemeとversionのようなのでこの二つを追加していきます。
その他は任意なので割愛。

```
theme = 'DoIt'
[params]
  version = '0.2.X'
```

手順ドキュメント：https://hugodoit.pages.dev/theme-documentation-basics/

## 記事を追加する

ここまできたらページはほぼ完成しています。
あとはコンテンツを追加するだけです。

```
$ hugo new posts/create-a-blog.md
```

作成されたファイルの項目は、archetypes配下のdefault.mdを見て作成されます。
デフォルトの設定だとこんな感じ。

```
$ cat content/posts/create-a-blog.md
---
title: "Create a Blog"
date: 2021-09-24T14:12:40+09:00
draft: true
---

```

実際使う時にタイトルは考えたいというのと、ジャンル分けのために`categories`項目を作りたいという気持ちがあったので
テンプレートを少し変更しました。
テンプレートを複数作成する方法もあるみたいですが今回は不要なので割愛。

```
$ cat archetypes/default.md
---
title: ''
date: {{ .Date }}
draft: true
categories: ['', '']
---
```

ざっくり入門編でした。
Hugoでもっとなんかできないかってなった時にはまたドキュメント見てガチャガチャやりたいと思います。
