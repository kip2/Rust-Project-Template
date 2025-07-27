# Rust-Project-Template

RustでWebアプリを作成する際のテンプレートです。

## 特徴

- 基本的なRust製のWebAPIとDBを用意しています。これを基礎にして好きなアプリを作成できます。
- Dockerを用いているため、どの環境でも実行ができます。
- `cargo make`を使用しています。必要なタスクがあれば追加したり、定義を変更することで柔軟に起動を行うことができます。

## 使用しているツール

| 種類 | 名前・バージョンなど|
| --- | --- |
| DB |  postgres 16 |
| Rust | 1.87 |

その他、Rustで使用しているライブラリなどは`Cargo.toml`をご確認ください。

---

## 使用の前の注意

### `.env`について

`.env-template`ファイルは、`.env`のサンプルとして入れています。

使用する際には、ファイル名を`.env`に変更してから使用して下さい。

`.env`は`.gitignore`に含まれているので、ファイル名を変更するだけで良いです。

その後、環境に合わせて.envの定義を変更してください。

### プロジェクト名の変更

`Cargo.toml`のプロジェクト名を変更してください。

```toml
[package]
# nameを変更したいプロジェクト名にする
name = "template"
version = "0.1.0"
edition = "2024"
```

## 起動の仕方

`cargo-make`を使用しているため、インストールが必要となります。

事前に以下のコマンドでインストールを行って下さい。

```sh
cargo install --force cargo-make

# バージョン確認
cargo make --version
```

コマンドは`Makefile.toml`に記載されているので、参照して下さい。

> `[taks.compose]`と、書かれているのが該当です。
> このタスクであれば、以下の様に起動できます。

> ```sh
> cargo make compose
> ```

### 起動

起動の前にDocker Desktopを起動して下さい。

アプリの起動は以下のコマンドで行います。

```sh
cargo make run
```

これでDocker内でアプリとDBが起動され、アクセスできる状態となります。

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
