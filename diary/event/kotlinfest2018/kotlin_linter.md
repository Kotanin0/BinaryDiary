# Kotlin Linter

釘宮愼之介さん

## linter とは


## ktlint
インストールなどはREADMEにしたがう。
基本的に各ルールについて、enable/disableの設定はできない
インデント文字数とファイル末尾改行の有無のみ指定できる

カスタムルールのつくりかた
コンパイルしたときのツリー構造について把握する
-> PsiViewerプラグインを利用する

visitメソッド
自作するはなし

## detekt
標準で用意されているルールはktlintより多い
./gradler detectgeneratehoge
個別にルールの設定が可能
ktlintと異なり、複数のルールがある

detekt-formatting

## android-lint
androidプロジェクトを作ってlintタスクを実行するだけ

## まとめ
写真とった














