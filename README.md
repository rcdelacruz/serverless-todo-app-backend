# serverless-todo-app-backend
TODOリストアプリ用のバックエンドサーバ。

## 事前準備

### 環境変数の設定

動作に必要な環境変数を設定します。
以下は.bash_profileへの設定例です。

```bash
echo export TODO_APP_BACKEND_BASE_URI=https://test999999.execute-api.ap-northeast-1.amazonaws.com/dev >> ~/.bash_profile
source ~/.bash_profile
```

## デプロイ
```bash
yarn run deploy
```

## lint（チェックのみ）
```bash
yarn run lint
```

## lint（修正を行う）
```bash
yarn run lint:fix
```

## テスト実行方法

### Integrationテスト（結合テスト）

実際にデプロイされたAWSサービスに対してリクエストを送信しその返り値や挙動を確認する。

- 存在する全てのテストケースを実行する

```bash
yarn run test:all
```

- 一部のテストファイルだけを実行する
下記場合は `src/tests/integration/functions/todo/create.spec.ts` のみが実行対象になります。

```bash
yarn run test src/tests/integration/functions/todo/create.spec.ts
```

- 特定のテストファイル中の特定のテストケースのみを実行
`-g` の後にテストケース名を入力します。

```bash
yarn run test src/tests/integration/functions/todo/create.spec.ts -g testSuccess
```

## ローカルサーバの起動

```bash
yarn run server
```

もしもDebuggerを使ってデバッグを行いたい場合は `yarn run server:debug` を実行してサーバを立ち上げて下さい。

[こちら](https://github.com/keita-nishimoto/aws-serverless-prototype/wiki/Local-Debugging) に載っている手順と同様にデバッグが可能です。

### ローカルサーバに対してIntegrationテスト（結合テスト）を実行する

事前にローカルでDynamoDBを起動しておく必要があります。（以下の手順を実行して下さい。）

- `yarn run dynamodb:instal` を実行する。（最初だけでOKです。）
- `yarn run dynamodb:start` を実行しローカルでDynamoDBを起動する。
- `yarn run dynamodb:migrate` を実行しローカルのDynamoDBにテーブルの作成を行う。

- 存在する全てのテストケースを実行する
```bash
yarn run test:all:local
```

- 一部のテストファイルだけを実行する
```bash
yarn run test:local src/tests/integration/functions/todo/create.spec.ts
```

- 特定のテストファイル中の特定のテストケースのみを実行
`-g` の後にテストケース名を入力します。

```bash
yarn run test:local src/tests/integration/functions/todo/create.spec.ts -g testSuccess
```
