# 新人向けチュートリアル (rest-json-quickstart)

このプロジェクトは、環境構築が完了した新人が Quarkus を実際に動かし、ソースコードの構造を理解するためのチュートリアルです。
公式の [REST JSON Quickstart](https://quarkus.io/guides/rest-json) をベースにしていますが、プロジェクト固有の設定が含まれています。

## 1. アプリケーションの起動方法

Quarkus の **Dev Mode** を使用すると、コードの変更が即座に反映されます（ライブコーディング機能）。
本プロジェクトでは、ビルド時に特定のフラグが必要です。

```shell
./gradlew quarkusDev -Pbuild_logic=quarkus_3.15.2
```

> **注意:** 起動後、ブラウザで [http://localhost:8080/](http://localhost:8080/) にアクセスして、デフォルトのページが表示されることを確認してください。

---

## 2. ソースコードの構成

このプロジェクトは、簡単な「フルーツ」と「豆類（Legume）」の情報を管理する REST API です。

### ディレクトリ構成
```text
src/main/java/org/acme/rest/json/
├── Fruit.java           # データモデル（フルーツ）
├── FruitResource.java   # API エンドポイント（フルーツ用）
├── Legume.java          # データモデル（豆類）
└── LegumeResource.java  # API エンドポイント（豆類用）
```

### 主要クラスの解説

- **Fruit.java**:
    - フルーツの名前 (`name`) と説明 (`description`) を持つシンプルな POJO です。
- **FruitResource.java**:
    - `/fruits` パスでアクセス可能な REST エンドポイントです。
    - `@GET`: フルーツのリストを取得します。
    - `@POST`: 新しいフルーツを追加します（メモリ上に一時保存されます）。
- **LegumeResource.java**:
    - `/legumes` パスでアクセス可能な REST エンドポイントです。
    - こちらは読み取り専用の例として、固定のリストを返します。

---

## 3. 動作確認

起動したら、以下の方法で動作を確認してみましょう。

### A. ブラウザで確認（UI）
ブラウザで以下の URL にアクセスすると、データが表示される HTML ページが用意されています。
- [http://localhost:8080/fruits.html](http://localhost:8080/fruits.html)
- [http://localhost:8080/legumes.html](http://localhost:8080/legumes.html)

### B. コマンドで確認 (curl)
ターミナルから直接 API を叩いてみましょう。

**データ取得 (GET):**
```shell
curl http://localhost:8080/fruits
```

**データ追加 (POST):**
```shell
curl -X POST -H "Content-Type: application/json" -d '{"name":"Banana","description":"Yellow fruit"}' http://localhost:8080/fruits
```

---

## 4. 便利な機能

### Dev UI
Dev Mode で起動中、以下の URL から Quarkus の内部状態や設定を確認できる管理画面（Dev UI）にアクセスできます。
- [http://localhost:8080/q/dev/](http://localhost:8080/q/dev/)

### テストの実行
ユニットテストを実行するには以下のコマンドを使用します。
```shell
./gradlew test -Pbuild_logic=quarkus_3.15.2
```

---

## 次のステップ
1. `FruitResource.java` の中身を書き換えて（例：初期データに自分の好きなフルーツを追加）、ブラウザをリロードしてみましょう。
2. 新しいフィールドを `Fruit.java` に追加し、API の挙動がどう変わるか確認してみましょう。
