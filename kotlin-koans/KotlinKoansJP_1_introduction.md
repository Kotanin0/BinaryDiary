# 【Kotlin Koans】解いてみるぞ！ 第1章 -はじまりはじまり-

ー挨拶ー

[前回の記事：【Kotlin Koans】はじめるぞ！ 第0章 -準備-]()

さて、今回からKotlin Koansを実際に解いていきます。

本日は第1章ということで、 `Introduction` にある0-12問を解いていきます。

わたしの環境は、IntelliJ IDEAでEduToolsスタイルです。

なんとしても自力で解きたい方、ごめんなさいネタバレ含むなので、自己判断でご覧ください。

また、英語力はそこまで高くないので、独断と偏見のエモい意訳が多々ありますがご容赦ください。

## 0. こんにちは世界

#### 問題
"OK" という文字列を返却する関数を作ってみましょう！

#### 解答と解説
はじまりのはじまり、 `TODO()` となっている部分に解答を書いてくんだよ、っていうチュートリアルです。

今回はシンプルに、関数の返却を書くだけ。
```kotlin
fun start(): String = "OK"
```
この関数は[単一式関数](http://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E5%8D%98%E4%B8%80%E5%BC%8F%E9%96%A2%E6%95%B0)という表現方法になっています。

単一式関数とは、関数の処理部分が単一の式になっている、シンプルに戻り値を返すつくりです。

こうすることで、処理を挟む余地がなくなり、関数の役割が明確になります。

さらに、型推論できる範囲であれば戻り値の型宣言を省略できます。

```kotlin
fun start() = "OK"
```
素敵。

## 1. JavaをコピってKotlinにペッ

#### 問題
JavaCode1.java内のtask1メソッドをコピってKotlinに貼り付けてみましょう。

#### 解答と解説
コピペするだけなので省略。

これはKotlinと親和性の高い IntelliJ IDEA (或いはAndroid Studio) のステマ問題。

Javaから持ってきたコードをKotlinファイル内にペーストするだけで、コードを変換してくれるという便利機能の紹介でした。

## 2. 名前付き引数

#### 問題
[Collectionクラスの関数joinToString](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html)を利用してみましょう。

その関数にある、prefix, postfixという引数を、名前付き引数として使ってみましょう。

#### 解答と解説
[名前付き引数](http://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E5%90%8D%E5%89%8D%E4%BB%98%E3%81%8D%E5%BC%95%E6%95%B0)とは、関数の引数を名前付きで定義しておくことで、関数を利用する側にとても利用しやすくする書き方です。

今回利用した[Collection.joinToString](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html)には、名前付き引数が6つ用意されています。
```kotlin
fun <T> Array<out T>.joinToString(
    separator: CharSequence = ", ", 
    prefix: CharSequence = "", 
    postfix: CharSequence = "", 
    limit: Int = -1, 
    truncated: CharSequence = "...", 
    transform: (T) -> CharSequence = null
): String
```

今回はこれらのうち `prefix` `postfix` の2つを指定し、それ以外はデフォルトのままでいけます。
```kotlin
fun joinOptions(options: Collection<String>) = 
    options.joinToString(prefix = "[", postfix = "]")
```

## 3. デフォルト引数

#### 問題
問題文内にJavaで書かれたオーバーロードだらけの関数fooがあります。

Kotlinでは1つの関数に置き換えられるのでやってみましょう。

#### 解答と解説
[デフォルト引数](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%81%AE%E5%BC%95%E6%95%B0)とは、関数の引数に初期値を定義しておくことで、同名複数のオーバーライドを減らすことができる書き方です。

今回は引数違いで4つあるJavaのfoo関数
```java
public String foo(String name, int number, boolean toUpperCase) {
    return (toUpperCase ? name.toUpperCase() : name) + number;
}
public String foo(String name, int number) {
    return foo(name, number, false);
}
public String foo(String name, boolean toUpperCase) {
    return foo(name, 42, toUpperCase);
}
public String foo(String name) {
    return foo(name, 42);
}
```

これをKotlinのデフォルト引数を利用して1つにしちゃいましょう。

- `name` は使ってそう
- `number` はデフォルト `42` でよさそう
- `toUpperCase` はデフォルト `false` でよさそう
```kotlin
fun foo(name: String, number: Int = 42, toUpperCase: Boolean = false) =
    (if (toUpperCase) name.toUpperCase() else name) + number
```

## 4. ラムダ式

#### 問題
ラムダを使って、Collection内に偶数が含まれているかどうか判定し、その結果を返しましょう。

#### 解答と解説
[ラムダ](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/lambdas.html#%E9%AB%98%E9%9A%8E%E9%96%A2%E6%95%B0%E3%81%A8%E3%83%A9%E3%83%A0%E3%83%80)とは、「独立して宣言を行わず、式のひとつとして即時利用する関数」みたいなイメージ。

Kotlinのラムダを簡単に表したルールは以下です。

- ラムダ式は、常に中括弧で囲まれています
- パラメータは（もしあれば） `->` の前で宣言されます（パラメータの型を省略してもかまいません）
- 本体が `->` に続きます（存在する場合）
- ラムダの引数が1つの場合、引数の宣言を省略できます。そのときの引数の名前は `it` となります。

今回の問題では、collectionの要素に偶数が含まれているか判定したい、という内容です。

collectionの中にひとつでも判定したい要素があるかどうかを調べるには、[Collections.any](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/any.html)を利用できそうです。

anyは、引数としてBooleanを返す条件式を希望しているようです。

ここでラムダの出番ですね。偶数を判定する式をanyに渡してあげることで今回の問題はクリアです。
```kotlin
fun containsEven(collection: Collection<Int>) =
    collection.any { it % 2 == 0 }
```



