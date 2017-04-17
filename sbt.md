# sbt

## shell

### sbt上でオプション追加

* あるprojectにだけ、scalacOptions追加
  ```
  ; project core ; set scalacOptions += "-Ywarn-unused-import"; project FooProject
  ```
  最初の`;`が必須

## test

### 特定のテストだけ実行

* testOnly
    * FooSpec, BarSpecで終わるテスト（class）だけ実行
      ```
      testOnly *FooSpec *BarSpec
      ```
    * テストケースに"foobarbaz"を含むものだけ実行
      ```
      testOnly net.baz.bar.FooSpec -- -z "foobarbaz"
      ```

* testQuick
    * 失敗したテストだけ実行
    * 更新されたテストだけ実行
      ```
      ~testQuick
      ```
