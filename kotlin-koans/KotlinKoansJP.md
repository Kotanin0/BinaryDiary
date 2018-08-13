# Kotlin Koans を日本語化してみたぞ！

という連載をはじめたい。

イントロダクションがここらへんに入ると思う。Kotlinとは。Kotlin Koansとは。とか。


## Kotlin とは

言語のことを簡単に書く。


## Kotlin Koans とは

公安禅のことを簡単に書く。


# Kotlin Koans 第0章 -じゅんび-

Kotlin Koans を使って学習する方法は、大きく2通りあります。


## オンラインで学習する

オンラインとは、Kotlin本家が提供している Try Kotlin というWeb上のエディタで学習することを指します。

http://try.kotlinlang.org/koans

百聞は一見にしかずです、以下をご覧ください。

[といっていい感じの画像 or gifを挿入]

コードを書く、テスト実行する、カンニングする、が気軽に行えます。

このように、ローカルに開発環境が備わっていなくても、Webブラウザ上で気軽に学習することができます。


## オフラインで学習する

オフラインとは、Kotlin本家が提供している、Kotlin Koans のGitHubリポジトリからソースを落として、ローカルで学習することを指します。

https://github.com/Kotlin/kotlin-koans

ここから自分のマシンに落として、お好きなエディタ ( IntelliJ IDEA 一択ですよね ) で学習します。

テスト実行の際は、gradlew コマンドで試す感じになります。

./gradlew test --tests ii_*14*

テスト結果をターミナルで確認する感じになります。

また、テスト実行結果は都度htmlで出力されるので、そちらを確認するのもありです。

[自分のワークスペース]/kotlin-koans/build/reports/tests/test/index.html

カンニングをしたい際は、resolutions ブランチに切り替えると素敵な世界が見えるかと。


# Kotlin Koans 第1章 -はじまり-

ここからは Kotlin Koans の問題とその回答の一例を載せていきます。

なんとしても自力で解きたい方、ごめんなさいネタバレ含むなので、自己判断でご覧ください。

また、英語力はそこまで高くないので、独断と偏見のエモい意訳が多々ありますがご容赦ください。


## 0. こんにちは世界

問題
README読んでみたりいろいろしたりしてからの、"OK" という文字列を返却する関数を作ってみよう！

解答と解説
```kotlin
fun task0(): String {
    return "OK"
}
```
これはシンプルに、Kotlin の関数(fun)を扱うだけ。

高みを目指して
ただ実は、単一式関数というKotlinの解釈に従うと、もっとかなりスッキリするのです。
http://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E5%8D%98%E4%B8%80%E5%BC%8F%E9%96%A2%E6%95%B0
```kotlin
fun task0() = "OK"
```
素敵。

## 1. JavaをコピってKotlinにペッ

問題
JavaCode1.java内のtask1メソッドをコピってKotlinに貼り付けてみよう！

解答と解説
これはKotlinと親和性の高い IntelliJ IDEA (或いはAndroid Studio) のステマ問題。
Javaから持ってきたコードをKotlinファイル内にペーストするだけで、コードを変換してくれるという便利機能の紹介でした。

高みを目指して
コピペするだけだとむずかゆいのでリファクタしておいて追加点を狙いにいきます。
と思ったけど次の問題で習うからいいや。

## 2. 名前付き引数

問題
collectionクラスには便利な関数JoinToString()が用意されています。
その関数を、prefix, postfixという引数を使って利用してみよう！

解答と解説
名前付き引数とは、関数の引数を名前付きで定義しておくことで、関数を利用する側にとても利用しやすくする書き方です。
必要なものは全て、名前付き引数でデフォルト値を設定しておくことで、ひとつのメソッドをかなり柔軟に作成・利用可能です。
http://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E5%90%8D%E5%89%8D%E4%BB%98%E3%81%8D%E5%BC%95%E6%95%B0

今回利用したい JoinToString メソッドは、名前付き引数が6つ用意されています。
https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html

今回は、これらのうち、prefix, postfixだけ利用すれば良いとのことです。
```kotlin
fun task2(collection: Collection<Int>): String {
    return collection.joinToString(prefix = "{", postfix = "}")
}
```

高みを目指して
0回目の復習なので割愛します。



