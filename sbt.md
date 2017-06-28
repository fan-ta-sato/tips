# sbt

## shell

### sbt上でオプション追加

* あるprojectにだけ、scalacOptions追加
  ```
  ; project core ; set scalacOptions += "-Ywarn-unused-import"; project FooProject
  ```
  最初の`;`が必須

### javaOptions

* `fork := false`なら、JAVA_OPTIONSの設定を読み込んでくれる。
* `fork := true`だと、以下のようにする必要がある
  ```
  sbt ';project core ; scalacOptions += "-Dnend.env=ci"' test
  ```

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
    * テストケースに追加
      ```
      testOnly "project core" -- -n net.baz.bar.FooSpec
      ```
    * テストケースから除外
      ```
      testOnly "project core" -- -l net.baz.bar.FooSpec
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

## jarの作成 - assembly

https://github.com/sbt/sbt-assembly

* 依存を含めてjarを作成する
* project/plugins.sbt
  ```
  addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.4")
  ```
* jarの作成
  ```
  sbt <project>/assembly
  ```
* jarファイル実行
  ```
  java -cp XXX.jar net.bar.foo.MainObject
  ```
    * 当たり前だがmainが指定されているか、Appをmixinしておく必要あり

