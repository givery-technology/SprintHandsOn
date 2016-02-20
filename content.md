## Sprint ハンズオン

@Sony

http://givery-technology.github.io/SprintHandsOn

=====

## 自己紹介

### Takayuki Oda
GitHub: github.com/takayukioda  
Twitter: twitter.com/da0shi  
@Givery, Inc.

-----

Givery において
- Scala でのバックエンド開発  
- Ansible や docker を用いたインフラ周りの整備  
- Sprint やオフィシャルなコンテンツの制作 / マネジメント

等をしています。  
今はコンテンツのマネジメントが主になってます。

=====

## 流れ

- コンテンツのおさらい
- 今日のゴール確認
- 用語解説
- Hands-on

Note:
前半3項目で40分ほどを想定
Hands-on 2時間  
20分は Hands-on 中の api-first-spec の説明で無くなるかも

Hands-on の中では
- [Heroku Deploy](https://app.code-check.io/orgs/codecheck_official/challenges/69)
- [Portfolio](https://app.code-check.io/orgs/codecheck_official/challenges/74)

の2つのチャレンジを実施予定。
Heroku の Deploy 経験が無い人が居なければ飛ばして hands-on の時間を増やすかも。

api-first-spec 等に関しては Portfolio の方に移った時に説明
api-first-spec の説明で 20 分かかるかも

=====

## コンテンツのおさらい

- GitHub のアカウントを作って
- Heroku にデプロイ
- REST API サーバーを実装して
- オリジナル機能を追加する

=====

## 今日のゴールの確認

-----

GitHub 上で管理されている

-----

Node.js で実装した

-----

REST API サーバーを

-----

Test が通る事を確認して

-----

Heroku に Deploy する

-----

GitHub 上で管理されている  

Node.js で実装した  

REST API サーバーを  

Test が通る事を確認して  

Heroku に Deploy する

-----

要約すると  
REST API サーバーをNode.js で実装してHeroku に Deploy

-----

もっというと  
[このチャレンジ](https://app.code-check.io/orgs/codecheck_official/challenges/74)を終わらせる

-----

余裕があれば追加機能の実装も

=====

## 用語の確認

- GitHub
- Node.js
- REST API
- Test
- Heroku
- Deploy

Note:
用語の解説は一つ一つ分からない人がいるかを聞いていく。
いる場合は下に掘り下げたりするけど、居なければそのまま次の内容にスライド


=====

## GitHub

Git を使ったソースコードのホスティングサービス

Social Coding をキーワードに、OSS 文化の中心地として  
開発者から圧倒的な支持を得ている

Givery も僕個人も大ファン

-----

### Git
ソフトウェア開発におけるデファクトスタンダードとなった  
ソースコード管理ツール （バージョン管理ツールとも）

-----

### Git なにそれな貴方に

-----

### Git を使う意味
編集履歴が見れるようになるよ！  
「お、こいつ中々やるやん」って思われるよ！

アピールしたいことは富士山のようにあるけど、  
グッとこらえるよ！

-----

### 今回使う最低限のコマンド
- git clone
- git status
- git add .
- git commit -m "Improve!"
- git log
- git push origin master

-----

#### git clone
GitHub からソースコードをダウンロードする  
コマンドでダウンロードするのは同期を楽にするため

-----

#### git status
今のファイルの変更状況を見る

-----

#### git add .
今まで変更した全てのファイルを履歴の保存対象に含める

-----

#### git commit -m "Improve!"
履歴を一言添えて保存する。

-----

#### git log
編集履歴を確認する

-----

#### git push origin master
編集履歴を GitHub と同期させる

=====

## Node.js

JavaScript をブラウザ以外でも実行できるようにしたで！！

ブラウザ用の言語だった JavaScript をブラウザ無しの  
サーバーでも使えるようにした JavaScript 実行環境。

今回お世話になります。

-----

### JavaScript
知らないって言われたら色々な意味で泣いちゃうくらい有名な言語

ブラウザで動く唯一のプログラミング言語  
ちなみにコンパイラを必要としないスクリプト言語  
C++ や Java といった言語とは違った概念を取り入れた言語  

その気軽さとキモさからファンが沢山。嫌う人も沢山。

=====

## REST API

REST の思想に則った設計を行っている Web API

`GET /users` とか `POST /projects` とかとか

-----

### REST

最近の Web API 設計の主流となっている設計パターン。
REpresentational State Transfer の略

URL と HTTP 通信のメソッドを利用して  
「リソース」と「リソースに対する操作」を表現する。

-----

#### 操作とリソースの例

-----

#### `GET /users`
users というリソースを GET する。  
=> ユーザーの一覧取得

-----

#### `GET /users/:name`
users の `:name` で指定されたリソースを GET する。
=> 指定されたユーザーの詳細取得

-----

#### `POST /projects`
projects というリソースに POST する。
=> プロジェクトを作成

-----

#### `DELETE /projects/:id`
`:id` で指定された projects のリソースを DELETE する
=> プロジェクトを削除

-----

### エンドポイント

Web API にアクセスする際の URI の事。  
ホスト名等、基本的に変更のないベース部分と  
リソースを意味するパス部分に分かれる。

-----

### エンドポイント

`https://api.example.com/v1/users`
とあったら
- ベース部分 --> `https://api.example.com/v1`
- パス部分 --> `/users`

に分けられる

ドキュメント等ではベース部分を省略して  
`/users` のようにパス部分のみで表記される事が多い

例： https://developer.github.com/v3/pulls/

=====

## Test

決して学校の試験の事ではありません。

ソフトウェアが想定通りの振る舞いをするかの確認する事。  
その確認内容がコードに落とし込んだものが「テストコード」

codecheck ではテストを通らないとデプロイ禁止です。

-----

### 色々なテスト

- ブラックボックステスト
- ホワイトボックステスト
- 単体テスト (Unit test)
- 結合テスト (Integration test)
- などなど

-----

### ブラックボックス / ホワイトボックス

-----

### ブラックボックステスト
偶数かを判定する even 関数があった時に
- `even(4) === true`
- `even(1) === false`

となるかを確認する。

-----

### ホワイトボックステスト
以下のコードがあった時に
```javascript
function even (x) {
  if (x % 2 === 0) {
    return true;
  } else {
    return false;
  }
}
```
- x に 4 を入れた時に上の if 文にマッチするか？
- x に 1 を入れた時に下の else 文にマッチするか？

を確認する。

-----

今回のテストは **ブラックボックステスト** です。

-----

### 単体 / 結合
前提として「自身が実装したプログラム」に着目している  
（外部のライブラリとかは考慮に入れないことが普通）

-----

### 単体テスト (Unit Test)
ある一つのプログラムに着目し、その動作をテストする事
```javascript
assert.equal(even(4), true);
assert.equal(even(1), false);
assert.equal(even(-6), true);
```

-----

### 結合テスト (Integration Test)
ある複数のプログラムを組み合わせて作った機能に着目し、  
その動作をテストする事
```javascript
function rowStyle(data, index) {
  var cssClass = even(index)? "even": "odd";
  var row = document.creteElement('tr');
  row.textContent = data;
  row.className = cssClass;
  return row;
}
```

-----

今回のテストは **結合テスト** です。

-----

### テストコード
スライドでコードが出てくるけど、  
見づらいので gist 用意しました  
https://gist.github.com/takayukioda/494079672aae767cd4f7
-----
### テストコード
プログラムの挙動を確認するためのコード

```javascript
console.log("even 関数のテスト");
if (even(3) === false) {
  console.log("You pass the test!");
} else {
  console.log("You fail the test...");
}
console.log("マイナス値でも動作するかのテスト");
if (even(-4) === true) {
  console.log("You pass the test!");
} else {
  console.log("You fail the test...");
}
```
```bash
$ node pure.js
even 関数のテスト
You pass the test!
マイナス値でも動作するかのテスト
You pass the test!
```

-----

### テストフレームワーク
生のコードだと書くのシンドイ & 集計が面倒  
あと「なんのためのテストか」をまとめるのも大変

**テストのためのフレームワーク**

```javascript
describe("even function", function() {
  it("should return false on odd number", function() {
    assert.equal(even(3), false);
  });
  it("should work for negative number", function() {
    assert.equal(even(-4), true);
  });
});
```
```bash
$ mocha framework.js
  even function
    ✓ should return false on odd number
    ✓ should work for negative number

  2 passing (9ms)
```

=====

## Heroku

インフラ管理を劇的に楽にしてくれる、  
サービスのホスティングサービス

面倒なインフラ環境の構築を簡略化し、  
「アドオン」という形で提供してくれる。

codecheck も Heroku を使ってホスティングされていたり。

=====

## Deploy

ソースコード等をサーバー側に送り、  
サービスの内容を最新の状態にアップグレードする事

元々は「軍隊を戦闘配備する・布陣を敷く」という  
軍事用語だそうな。

へぇ〜

=====

## api-first-spec について
REST API のテスト用に作られた テストフレームワーク  
種類としてはブラックボックステスト

指定された URL に対して指定されたメソッドでリクエスト送信  
期待するレスポンスが返ってくるかを判定

-----

### 使い方はハンズオンの中でお伝えします

Note:
ここまでで 40 分  
一つ一つを丁寧に説明していたらもっとかかるかも

=====

## ハンズオン

Note:
Heroku Deploy で 30 分
Portfolio で 1時間半 取れる事を目標に

=====

### Heroku Deploy

元となってるリポジトリは  
https://github.com/code-check/challenge-heroku-deploy

キーワードは

- Procfile
- Buildpacks
- Addon (特に Rails 使う人は)

-----

Node.js の Heroku Deploy Challenge は以下から
https://app.code-check.io/orgs/codecheck_official/challenges/69

https://app.code-check.io/openchallenges  
から探せます。

-----

#### Try Challenge
まずは `Try Challenge` ボタンを押しましょう。

安心してください  
すぐにカウントダウンが始まるわけじゃないです ;)

-----

#### Fork to GitHub
`Fork to GitHub` というボタンを押して  
リポジトリを作成しましょう。

リポジトリ名にはデフォルトで  
`codecheck-***` みたいな名前が入ってます

作成すると 「作ったよ！」という表示とリンクが出るので  
リンクをクリックしてリポジトリに行きましょう！

-----

作った直後は空かもしれませんが、  
すぐにコードが現れるはずです。

コードが生成された事が確認できたら  
[Heroku](https://heroku.com) にアクセスしてください。

-----

### Heroku Application
まずは [Heroku で空のアプリを作成](https://dashboard.heroku.com/new)しましょう。

`App Name` は空でも自分でセットしても構いません。  
変えたければ後から変更もできます ;)

-----

Deployment method から GitHub を選んで、
さっき生成したリポジトリを指定して connect しましょう！

次に master リポジトリに対してAutomatic deploys をオンにしたら  
GitHub の方に戻ってリポジトリを編集します。

-----

### Procfile
Procfile を編集して  
Deploy 時に起動するコマンドを指定しましょう！

今回のリポジトリは `main.js` がサーバー起動のファイルなので

```
web: node main.js
```

と記入して保存、commit　そして push します。

-----

### テストを確認

まず、どの Heroku アプリケーションにアクセスするかを
`account.json` で指定しましょう！

ついでに commit して push しておきましょう :)

-----

ターミナル（コマンドプロンプト上）で以下のコマンドを実行して、　　
テストが通るかの確認をしましょう！

```javascript
$ npm install
$(npm bin)/mocha specifications
```

=====

### Portfolio

-----

### api-first-spec の見かた
```javascript
var API = spec.define({
  // エンドポイントのベース部分
  "endpoint": "/api/projects",

  // HTTP Request のメソッド
  "method": spec.Method.POST,

  // Request 関連の定義
  "request": {
    "contentType": spec.ContentType.URLENCODED,

    // Request で送るパラメータとその型
    "params": {
      "title": "string",
      "url": "string",
      "description": "string"
    },

    // パラメータに関する制約
    "rules": {

      // required => このパラメータは必須
      "title": { "required": true },
      "description": { "required": true },

      // url => URL 形式で定義されている必要がある
      "url": { "url": true }
    }
  },

  // Response 関連の定義
  "response": {
    "contentType": spec.ContentType.JSON,

    // Response で帰ってくるべきデータの内容
    "data": {
      "id": "int",
      "title": "string",
      "url": "string",
      "description": "string"
    },
  }
});

```

-----

### テストの確認方法
まずはサーバーを起動させておく
```bash
$ npm install
$ node index.js
```

次にテストを実行する
```bash
$ $(npm bin)/mocha specifications/localhost
```

-----

### テスト結果の見方
```bash
$ $(npm bin)/mocha specifications/localhost
  Validate API spec. /api/projects/[id]
    ✓ endpoint is correct.
    ✓ method is correct.
    ✓ unknown config keys
    Validate request spec.
      ✓ contentType is correct.
    Validate response spec.
      ✓ response is defined.
      ✓ data is defined.
      Validate response param.
        ✓ datatype

  DELETE /api/projects/:id
    ✓ should be not found if not exists
    ✓ should succeed if exsits

# ... 中略...

  POST /api/projects
    ✓ should contains title
    ✓ should contains description
    ✓ should succeed


  48 passing (187ms)
```

=====

## 参考文献

-----

### ライブラリ
- mocha
- chai
- api-first-spec

-----

### テストの種類とか
- http://gihyo.jp/dev/serial/01/tech_station/0001
- http://magazine.rubyist.net/?0042-FromCucumberToTurnip#l1
- http://qiita.com/ktarow/items/8c3d94d6c21a0c86b799
