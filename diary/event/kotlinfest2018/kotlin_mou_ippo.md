# Kotlin もう一歩

森洋之さん

## タイプシステム

### タイプとはなにか

型ごとに、変数や式のとりうる値の範囲が決まる
型によって、行える操作や演算が決まる
nullableはいろいろできない、メソッドコールまわり
String?.hashCode() はできない

だから安全！

### タイプとサブタイプ

クイズ

Kotlinのタイプシステムでは、Int型はInt型の...
A.サブタイプ、B.スーパータイプ、C.どちらでもない、D.どちらでもある

どちらでもある

### Any

すべてのスーパータイプ

### Nothing

あらゆるタイプのサブタイプ

## nullable と non-null

## generics

上限境界
ジェネリクスで、サブタイプを決めたい。あるタイプのメソッドを利用したい
fun <T:Number> toDouble(t:T) = t.toDouble()

### Type Erasure
val list : List<String> = listOf();

invariant:不変

convariant:共変
class Covariant<out T>(val value: T)
val num : Covariant<Number> = Covariant<Int>(100)

contravariant:反変
class Contravariant<in T>(value: T)


### in と out
変位アノテーション

out:戻り値にしか使われない
in:引数にしか使われない

### Star projection

class Foo<out T:Number>(val value : T)
val foo : Foo<*> = Foo(1)









