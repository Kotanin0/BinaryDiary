# How to Test Server-side Kotlin

鈴木健太・前原秀徳

## 自己紹介
## 会社紹介

今日のおはなし
10年前のレガシーシステムをKotlinでリプレイスしたときに培ったKotlinのテストに関する話

## テスティングフレームワーク

### Junit4
基本的の問題なく使える

@RuleをKotlinのプロパティにそのまま付けるとダメ
対策：@JvmField をつけると、privateでなくpublicなフィールドが生成されるからOK
対策：@get:Rule とすると、getterへのアノテーションであると明示できるからOK

@JvmStaticも似た話

### Junit5
SpringFramework5から

### Spek
v2.0待った方がいいらしい

### KotlinTest

## アサーションライブラリ

### Hamcrest

### AssertJ

### KotlinTest

## Mockito のはまりどころ


### final問題
- 愚直にopen
- interface
- allopenプラグイン
- mock-maker-inline 

mockito-kotlin というラッパーを使うといい。

## DBTest

### DBUnit
xml,cssなどから外部ファイルを作る方法もある

## How do we test server-side Kotlin

テストは基本的にアプリケーション層より上
DBは結局利用した

## JSON APIのテスト
json unit

### カバレッジ
Jacoco

DBSetup * AssertJ-DB











