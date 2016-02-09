## Sprint ハンズオン

@NTTコミュニケーションズ株式会社
=====

## 自己紹介

### Takayuki Oda
GitHub: github.com/takayukioda  
@Givery, Inc.

=====

## 流れ

- コンテンツのおさらい
- 今日のゴール確認
- 用語解説
- テストについて
- Hands On
- オリジナル機能のアイディア出し
=====

## コンテンツのおさらい

- GitHub のアカウントを作って
- Heroku にデプロイ
- REST API サーバーを実装して
- オリジナル機能を追加する
=====

## ゴールの確認
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
あとはオリジナル機能のアイディアを出す
=====

## 用語の確認

- GitHub
- Heroku
- Node.js
- REST API
- Deploy
- Test
=====

## GitHub

Git を使ったソースコードのホスティングサービス

Social Coding をキーワードに、OSS 文化の中心地として  
開発者から圧倒的な支持を得ている

Givery も僕個人も大ファン
=====

## Heroku

インフラ管理を劇的に楽にしてくれる、  
サービスのホスティングサービス

面倒なインフラ環境の構築を簡略化し、  
「アドオン」という形で提供してくれる。

codecheck も Heroku を使ってホスティングされていたり。
=====

## Node.js

JavaScript をブラウザ以外でも実行できるようにしたで！！

ブラウザ用の言語だった JavaScript をブラウザ無しの  
サーバーでも使えるようにした JavaScript 実行環境。

今回お世話になります。
=====

## REST

最近の Web API 設計の主流となっている設計パターン。
REpresentational State Transfer の略

URL と HTTP 通信のメソッドを利用して  
「リソース」と「リソースに対する操作」を表現する。

`GET /users` とか `POST /projects` とかとか
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

=====

## Deploy

ソースコード等をサーバー側に送り、  
サービスの内容を最新の状態にアップグレードする事

元々は「軍隊を戦闘配備する・布陣を敷く」という  
軍事用語だそうな。

へぇ〜
=====

## Test

決して学校の試験の事ではありません。

ソフトウェアが想定通りの振る舞いをするかの確認する事。  
その確認内容がコードに落とし込んだものが「テストコード」

codecheck ではテストを通らないとデプロイ禁止です。
-----
### 色々なテスト

- ブラックボックステスト / ホワイトボックステスト
- 単体テスト (Unit test) / 結合テスト (Integration test) /  
統合テスト (General test)
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
今回は **ブラックボックステスト** のみを扱います。
-----
### テストコード

プログラムの挙動を確認するためのコード
```javascript
console.log("引数を2乗した値を返す square 関数のテスト");
if (square(4) === 16) {
  console.log("You pass the test!");
} else {
  console.log("You fail the test...");
}
console.log("マイナス値でも動作するかのテスト");
if (square(-3) === 9) {
  console.log("You pass the test!");
} else {
  console.log("You fail the test...");
}
```
```bash
$ node pure.js
引数を2乗した値を返す square 関数のテスト
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
describe("Square function", function() {
  it("should return squared value", function() {
    assert.equal(square(4), 16);
  });
  it("should work for negative value", function() {
    assert.equal(square(-3), 9);
  });
});
```
```bash
$ mocha framework.js
  Squeare function
    ✓ should return squared value
    ✓ should work for negative value

  2 passing (9ms)
```
=====

## api-first-spec について
REST API のテスト用に作られた テストフレームワーク  
種類としてはブラックボックステスト

指定された URL に対して指定されたメソッドでリクエスト送信  
期待するレスポンスが返ってくるかを判定
-----
### 使い方はハンズオンの中でお伝えします
=====

## ハンズオン
=====

### テストコードの見方
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
