# Cassandra CheatSheet

## 構造

- <span style="background: #aff;">Claster（Cassandra Instance）</span>
  - <span style="background: #acf;">Keyspace</span>
    - <span style="background: #aaf;">ColumnFamily</span>
      - <span style="background: #a7f;">Raw-Key（Partition Key）</span>
        - <span style="background: #fcc;">Column</span>
            - <span style="background: #ffc;">name</span>
            - <span style="background: #ffc;">value</span>
            - <span style="background: #ffc;">timestamp</span>
        - <span style="background: #fcc;">Column</span>
            - <span style="background: #ffc;">name</span>
            - <span style="background: #ffc;">value</span>
            - <span style="background: #ffc;">timestamp</span>

- <span style="background: #a7f">Raw-Key</span>と<span style="background: #fcc">Column</span>の間にSuperColumnsを入れる事もできるが公式非推奨（最新状況は不明）。
  https://www.datastax.com/dev/blog/introduction-to-composite-columns-part-1

## CLIコマンド/cassandra-cli

- Keyspace確認
  ```
  show keyspaces;
  ```

- Keyspace選択
  ```
  use keyspace_name;
  ```

- ColumnFamily一覧
  ```
  describe
  ```

- 値の取得
  ```
  get columnfamily [column]
  ```

## CLIコマンド/cqlsh

- Keyspace確認
  ```
  DESCRIBE keyspaces;
  ```

- Keyspace選択
  ```
  USE keyspace_name;
  ```

- ColumnFamily一覧
  ```
  DESCRIBE tables;
  ```

- 値の取得
  ```
  SELECT *
  FROM keyspace.columnfamily
  WHERE key = '...';
  ```
  e.g.
  ```
  cqlsh:keyspaceName> select * FROM columnFamilyName WHERE key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';

   key                              | column1 | value
  ----------------------------------+---------+---------------------
   xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx |  x_9999 | 2017-11-07 19:31:14

  (1 rows)
  ```

