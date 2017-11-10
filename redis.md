# Redis CheatSheet

## データ型

- Document  
  http://redis.shibu.jp/datatypes.html

- キーの一覧
  ```
  > keys *
  ```

- 値のタイプを取得
  ```
  > type key_name
  ```

## String型

```
> type key_name
string
```

- 値を取得
  ```
  > get key_name
  ```

## List型

```
> type key_name
list
```

- リストの長さ
  ```
  > llen key_name
  ```

- 指定範囲のリストを取得
  ```
  > lrange key_name start end
  ```

- 指定Indexの値を取得
  ```
  > lindex key_name index
  ```

## Set型

```
> type key_name
set
```

- セットへ追加
  ```
  > sadd key_name member1 member2 member3, ...
  ```

- セットの値を全取得
  ```
  > smembers key_name
  ```

- セットに値が含まれている場合は1を返す。なければ0を返す
  ```
  > sismember key_name member
  ```

## SortedSet型

```
> type key_name
zset
```

## Hash型

```
> type key_name
hash
```

- 値をセット
  ```
  > hset key_name field value
  ```

- 複数値をセット
  ```
  > hmset key_name field1 value1 field2 value2 ... fieldN valueN
  ```

- 値を取得
  ```
  > hget key_name field
  ```

- 複数値を取得
  ```
  > hmget key_name field ... fieldN
  ```

- 全フィールドと値を取得
  ```
  > hgetall key_name
  ```
