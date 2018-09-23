# Kotlin Koans を日本語化してみたぞ！

ー挨拶ー

Kotlin、これからもっともっと人気が出てくるであろうプログラミング言語。

弊社内でも少しずつ採用範囲が広がってきていますが、よく耳にする声はやはり

「Kotlinを学びたいけどどこから始めたらいいかわからない。。。」

わかる、わかりみ、わかりてぃ。

可愛いKotlinには、そういう走り出しを支援してくれるステキな助言が[Kotlin公式リファレンス](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/)のトップに記載されています。

- [Kotlin公式リファレンス](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/)を読みながら[オンラインIDE](http://try.kotlinlang.org/)で遊んでみよう
- 書籍を読もう
- [Kotlin Koans](https://dogwood008.github.io/kotlin-web-site-ja/docs/tutorials/koans.html)に挑戦しよう

また、[日本Kotlinユーザグループ](https://kotlin.connpass.com/)では、Kotlin入門のための助走読本という日本語教科書が提供されています。

と、いくつか勉強方法のアドバイスがある中、Kotlin Koansにフォーカスします。

## Kotlin Koans とは

[Kotlin Koans](https://dogwood008.github.io/kotlin-web-site-ja/docs/tutorials/koans.html)

> インタラクティブなプログラミング演習

とある通り、Kotlinのプログラミング問題集です。

Koans＝コーアンズと呼びます。

名前の由来は「公案」という日本語から来ているそうです。禅問答のことらしい。オシャレ。

Kotlin Koansには、40問ちょいの問題が用意されています。

本連載記事は、それを日本語で解説してみるをテーマに書き進めます。

初回は準備編、第0章です。

# Kotlin Koans 第0章 -準備-

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
JavaCode1.java内のtask1メソッドをコピってKotlinに貼り付けてみましょう。

解答と解説
コピペするだけなので省略。
これはKotlinと親和性の高い IntelliJ IDEA (或いはAndroid Studio) のステマ問題。
Javaから持ってきたコードをKotlinファイル内にペーストするだけで、コードを変換してくれるという便利機能の紹介でした。

高みを目指して
コピペするだけだとむずかゆいのでリファクタしておいて追加点を狙いにいきます。
と思ったけど次の問題で習うからいいや。

## 2. 名前付き引数

問題
collectionクラスには便利な関数JoinToString()が用意されています。
その関数を、prefix, postfixという引数を使って利用してみましょう。

解答と解説
名前付き引数とは、関数の引数を名前付きで定義しておくことで、関数を利用する側にとても利用しやすくする書き方です。
必要なものは全て、名前付き引数で設定しておくことで、ひとつのメソッドをかなり親切に作成・利用可能です。
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
単一式関数最高。
```kotlin
    fun task2(collection: Collection<Int>) = collection.joinToString(prefix = "{", postfix = "}")
```

## 3. デフォルト引数

問題
JavaCode3.java内にたくさんオーバーロードされている関数fooがあります。
Kotlinでは1つの関数に置き換えられるのでやってみましょう。

解答と解説
デフォルト引数とは、関数の引数に初期値を定義しておくことで、同名複数のオーバーライドを減らすことができる書き方です。
問2で学んだ名前付き引数と組み合わせることで、かなり柔軟に同名メソッドを作り重ねることができます。
https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%81%AE%E5%BC%95%E6%95%B0

今回は引数違いで4つあるJavaのfoo関数
```java
    public String foo(String name, int number, boolean toUpperCase) {
        return (toUpperCase ? name.toUpperCase() : name) + number;
    }

    public String foo(String name, int number) {
        return foo(name, number, false);
    }

    public String foo(String name, boolean toUpperCase) {
        return foo(name, defaultNumber, toUpperCase);
    }

    public String foo(String name) {
        return foo(name, defaultNumber);
    }
```

これをKotlinのデフォルト引数を利用して1つにしちゃいましょう。
```kotlin
    fun foo(name: String, number: Int = 42, toUpperCase: Boolean = false): String {
        return (if (toUpperCase) name.toUpperCase() else name) + number
    }   
```

高みを目指して
できてこれだった。。。
`
```kotlin
    fun foo(name: String, number: Int = 42, toUpperCase: Boolean = false) =
        (if (toUpperCase) name.toUpperCase() else name) + number
```

## 4. ラムダ式

問題
JavaCode4.javaにあるコレクションをIterablesで偶数判定しているメソッドをKotlinのラムダで表現しましょう。

解答と解説
ラムダとは、「独立して宣言を行わず、式のひとつとして即時利用する関数」みたいなイメージ。
https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/lambdas.html#%E3%83%A9%E3%83%A0%E3%83%80%E5%BC%8F%E3%81%A8%E7%84%A1%E5%90%8D%E9%96%A2%E6%95%B0
kotlinのラムダは以下のような簡単なルールに基づいています。
- ラムダ式は、常に中括弧で囲まれています
- そのパラメータは、（もしあれば） -> の前で宣言されます（パラメータの型を省略してもかまいません）
- 本体が -> に続きます（存在する場合）
さらに、ラムダの引数が1つの場合、引数の宣言を省略できます。そのときの引数の名前はitとなります。

今回の問題では、collectionの要素に偶数が含まれているか判定したい、という内容です。
collectionの中にひとつでも判定したい要素があるかどうかを調べるには、anyメソッドを利用できそうです。
https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/any.html
anyメソッドは、引数としてBooleanを返す条件式を希望しているようです。

ここでラムダの出番ですね。偶数を判定する式をanyに渡してあげることで今回の問題はクリアです。
```kotlin
    fun task4(collection: Collection<Int>) = collection.any { it % 2 == 0 }
```

高みを目指して
問題の解答はこれでよいとして、ちょっと上にexampleで用意されているメソッドをいじってみましょう。


