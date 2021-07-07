# 【Kotlin Koans】解いてみるぞ！ 第1章 -はじまりはじまり- 前編

[前回の記事：【Kotlin Koans】はじめるぞ！ 第0章 -準備-](https://tech.askul.co.jp/entry/2018/10/24/195654)

ー挨拶ー

さて、今回からKotlin Koansを実際に解いていきます。  
Kotlin Koansは大きく6つの章に分かれています。  

- Introduction
- Conventions
- Collections
- Properties
- Builders
- Generics

今回は第1章、 `Introduction` を解いていきましょう。  
Introductionは全部で12問ありますので、今回はそのうち前半6問を進めます。  
　  
本記事ではIntelliJ IDEAでEduToolsを使用して解説します。  
Try Kotlinやリポジトリ落とすなど、別の環境でも問題はほぼ同じです。  
　  
なんとしても自力で解きたい方、ごめんなさい。  
解答を含む記事ですので、自己判断でご覧ください。  
また、英語力はそこまで高くないので、独断と偏見のエモい意訳が多々ありますがご容赦ください。

## Hello, world! 

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

## Java to Kotlin conversion

#### 問題
.java内の関数をコピってKotlinに貼り付けてみましょう。

#### 解答と解説
コピペするだけなので省略。  
これはKotlinと親和性の高い IntelliJ IDEA (或いはAndroid Studio) のステマ問題。  
Javaから持ってきたコードをKotlinファイル内にペーストするだけで、コードを変換してくれるという便利機能の紹介でした。  

## Named arguments

#### 問題
[Collectionクラスの関数joinToString](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html)を利用してみましょう。  
その関数にある、prefix, postfixという引数を、名前付き引数として使ってみましょう。  

#### 解答と解説
[名前付き引数](http://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E5%90%8D%E5%89%8D%E4%BB%98%E3%81%8D%E5%BC%95%E6%95%B0)とは、関数の引数を名前付きで定義しておくことで、関数を利用する側にとても利用しやすくする書き方です。  
今回利用した [Collection.joinToString](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/join-to-string.html) には、名前付き引数が6つ用意されています。  
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

## Default arguments
#### 問題
Javaで書かれたオーバーロードだらけの関数fooがあります。

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

Kotlinでは1つの関数に置き換えられるのでやってみましょう。

#### 解答と解説
[デフォルト引数](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/functions.html#%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%81%AE%E5%BC%95%E6%95%B0)とは、関数の引数に初期値を定義しておくことで、同名複数のオーバーライドを減らすことができる書き方です。

今回は引数違いで4つあるJavaのfoo関数を、Kotlinのデフォルト引数を利用して1つにしちゃいましょう。

- `name` は使ってそう
- `number` はデフォルト `42` でよさそう
- `toUpperCase` はデフォルト `false` でよさそう
```kotlin
fun foo(name: String, number: Int = 42, toUpperCase: Boolean = false) =
    (if (toUpperCase) name.toUpperCase() else name) + number
```
1行で素敵。また単一式関数でスッキリと。

## Lambdas

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

## Strings

#### 問題
日付を表現した文字列 `13.06.1992` に対応する正規表現パターンは `"""\d{2}\.\d{2}\.\d{4}"""` です。  
では、`13 JUN 1992`（日、スペース、月の省略形、スペース、年）を正規表現を用いて表現しましょう。  

#### 解答と解説

[文字列リテラル](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/basic-types.html#%E6%96%87%E5%AD%97%E5%88%97%E3%83%AA%E3%83%86%E3%83%A9%E3%83%AB)は、ダブルクォート3連発 `"""` で囲むことで、エスケープが不要になります。  
正規表現で `¥d` 使いたいときに `¥¥d` にしなくていいし、改行などもそのまま表現することができます。  
　  
[文字列テンプレート](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/basic-types.html#%E6%96%87%E5%AD%97%E5%88%97%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88)は、文字列内で変数を利用できる記法です。  
文字列内でドル記号(`$`)はじまりで変数名を指定することで、可読性高い文字列のコードが書けます。  
  
名前と年齢を出力したいようなときに、従来の書き方だとこんなかんじ。  
`"名前＝" + member.name + ", 年齢＝" + member.age`

文字列テンプレートを利用するとこんなかんじ。  
`"名前＝$member.name, 年齢＝$member.age"`

かなり可読性が上がりますね、すごくわかりやすい。

今回の問題は、文字列リテラルと文字列テンプレートを併用するかたちが解答になります。

```kotlin
fun getPattern() = """\d{2}\ $month \d{4}"""
```

## Data classes

#### 問題
Javaで書かれているPersonクラスがあります。
```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

Kotlinのdata classを使って置き換えてみましょう。

#### 解答と解説

[データクラス](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/classes.html#%E3%82%B3%E3%83%B3%E3%82%B9%E3%83%88%E3%83%A9%E3%82%AF%E3%82%BF)は、シンプルにデータを扱うことに特化した修飾子です。  
プライマリコンストラクタとして、classの[コンストラクタ](https://dogwood008.github.io/kotlin-web-site-ja/docs/reference/classes.html#%E3%82%B3%E3%83%B3%E3%82%B9%E3%83%88%E3%83%A9%E3%82%AF%E3%82%BF)を明示します。  
冗長なコンストラクタを書いたり、フィールド宣言したり、といったコードを不要としてスッキリさせることができます。
  
今回は、問題に記載のあるJavaコードをコピペすることで、classへの変換は行ってくれます。  
（ちょっと前に習ったJava to Kotlinで、一瞬で）  
それに `data` を付けてあげることでクリアです。  

```kotlin
data class Person(val name: String, val age: Int)
```

