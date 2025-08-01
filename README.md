# Poc Image Upload Service

画像をアップロードするだけの簡単なAPIを作成する

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
