# gPRC学習用ブランチ

## 環境
- devcontainer
- go 1.24.2

## 起動方法

## メモ
### RPCとは
Remote Procedure Callの略．   
別サーバ上の関数を呼び出し，実行すること．

### gRPCとは
Google社によって開発され，マイクロサービス間（バックエンド間）での通信やモバイルアプリとバックエンドの通信で使用される．

gRPCでは，HTTP/2とProtocol Buffersを使用．
- HTTP/2
  * リクエストのパスに呼び出す関数の情報を保持．
  * HTTPリクエストボディに呼び出す関数の引数を保持．
  * HTTPレスポンスボディに呼び出した関数の戻り値を保持．

- Protocol Buffers
  * HTTPリクエストの情報を圧縮（シリアライズ）

### gRPCのメリットデメリット
* メリット
  * HTTP/2を使用．
  * バイナリ形式を使用．
  * 双方向通信が簡単．
  * コードをサービスに自動生成できる．
  * 多言語に対応．
* デメリット
  * バイナリ形式のため，デバッグが難しい．
  * 可読性が低い．
  * 学習コストが高い．
  * フロントからバックには適していない．  

※参考 https://qiita.com/S4nTo/items/0ff0445542538ef49a05

### protoファイル
関数の定義をするファイル．
```proto
syntax = "proto3";

// 自動生成するGoのコードの保存先
option go_package = "pkg/grpc";

package demo;

// サービスの定義
service HelloWorldService {
  // サービスが持つメソッドの定義
  // Hello関数で引数にHelloRequestを受け取り，HelloResponseを返す
  rpc Hello (HelloRequest) returns (HelloResponse);
}

// 型
message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}
```
