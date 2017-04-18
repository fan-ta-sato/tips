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

### ライブラリをローカルにjar化して読み込み

1. GitHubからcloneしてくる
1. `sbt publishLocal`する
    * `~/.ivy2/local`配下にライブラリが作成される
1. 自分のbuild.sbtに
  ```
  libraryDependencies ++= Seq(
    "org.scalikejdbc"    %% "scalikejdbc"                 % "3.0.0-SNAPSHOT" changing(),
  )
  ```
  みたいに書けば読み込まれる。
    * 当然binary versionが一致している必要がある

#### scalikejdbc

* 以下のURLのように、version指定してpublishLocalを実行  
  https://github.com/scalikejdbc/scalikejdbc/blob/master/travis.sh
  ```
  sbt '++ 2.12.1' root211/publishLocal
  ```
* tagsではなく、branchから取得してくる必要あり
