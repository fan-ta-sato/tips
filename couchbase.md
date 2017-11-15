# Couchbase

## 用語

### 物理構造

- クラスタ
  - 複数のノード（Serverインスタンス）の集合

- ノード（Couchbase Server）
  - Couchbase Serverの1インスタンス

### 論理構造

- https://developer.couchbase.com/documentation/server/current/n1ql/n1ql-intro/sysinfo.html

- Datastores
  - 1インスタンスの事（とニアリーイコール）
- Namespaces
  - RDBでいうところのデータベース
- Keyspaces
  - RDBでいうところのテーブル

- Buckets
  - https://developer.couchbase.com/documentation/server/current/architecture/core-data-access-buckets.html
  - 現在はKeyspace≒Bucketらしい
  - バケットタイプ
    - Couchbase: 永続性のあるドキュメントベースストレージ
    - Ephemeral: 永続性のないドキュメントベースストレージ
    - Memcache: いわゆるKVSタイプのストレージ

## CLIコマンド

### cbq

- パスワードあるバケットは
```
cbq -e=http://localhost:8091 -c=bucket_name:password
```

### N1QL

#### SELECT System Infomation

- https://developer.couchbase.com/documentation/server/5.0/n1ql/n1ql-intro/sysinfo.html

#### キー取得、キーの値取得

- https://developer.couchbase.com/documentation/server/4.1/n1ql/n1ql-language-reference/metafun.html
- 一覧
  ```
  SELECT meta(bucket_name) FROM bucket_name;
  ```
- キーから値取得 
  ```
  SELECT * FROM bucket_name WHERE meta(bucket_name).id = the_key;
  ```
