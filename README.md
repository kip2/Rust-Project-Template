# Rust project template

Rustのプロジェクト作成の際に使用できるテンプレートリポジトリです。

---

## 事前準備

タスクランナーとして`cargo-make`を、ファイル監視ツールとして`bacon`を採用しています。

https://github.com/sagiegurari/cargo-make

https://github.com/Canop/bacon

### `cargo-make`のインストール

```sh
cargo install cargo-make
```

### `baocn`のインストール

```sh
cargo install bacon
```

### `.env`ファイルの設定

`.env`ファイルを`.env-template`として用意しています。

ファイル名を`.env`に変更してください。

環境変数の設定値を変える場合は、設定を変更してください。

## 起動の仕方

起動の前にDocker Desktopを起動して下さい。

### 開発環境での起動

開発時は以下のコマンドで実行してください。

ファイルが更新されると、変更を検知してリビルドしてくれます。

```sh
cargo make dev
```

### 本番環境での起動

アプリの起動は以下のコマンドで行います。

```sh
cargo make run
```

これでDocker内でアプリとDBが起動され、アクセスできる状態となります。

起動後は、以下のコマンドで起動が成功しているかを確認できます。

```sh
docker compose logs app

# 以下のように表示されたら成功。サーバーが起動している。
# app-1  | Listening on 0.0.0.0:8080
```

手動での起動確認は以下のコマンドより行ってみてください。

```sh
# APIのヘルスチェック
curl http://localhost:8080/health

# DBのヘルスチェック
curl http://localhost:8080/health/db
```

### cargo makeによる起動テスト

`cargo make`を利用した確認は、以下のコマンドを用いて行います。

```sh
cargo make test
```

このテストにより、サーバ起動からDBへの疎通までの一連の認が行われます。

## 終了方法

アプリやDBを閉じるには以下のコマンドを実行してください。

```sh
cargo make destroy
```

---

## 個別

### DBのみ起動する

1. Dockerを起動する。
2. 以下のコマンドを実行する。

```sh
cargo make compose-up-db
```

接続確認は以下のコマンドで行うこと。

```sh
# 接続テスト(テンプレのままの.envの場合)
psql -h localhost -p 5678 -U app -d app
```

### テスト用のテーブル作成

DB起動後に`sqlx-cli`を用いて、マイグレーションを行うことができる。

まずはマイグレーションファイルを作成する。

```sh
sqlx migrate add -r <migration-file-name>
```

`up`と`down`ファイルが作成されるので、テーブル定義を記載する。

サンプルとして`users`テーブルを記載している。

記載後、マイグレーションを実施する。

```sh
sqlx migrate run
```

行って戻す場合は`revert`する

```sh
sqlx migrate revert
```
