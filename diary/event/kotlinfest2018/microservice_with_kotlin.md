# Kotlinで愛でるMicroservices

stormcat24
speciak thanks nozawaさん

## ワイとKotlin

## FRESHLIVEの紹介
- Microservices Architecture
- AmazonECS -> Kubernetes on AWS

### Microservicesの理由
- 可用性の工場と障害の局所化
- Serviceごとに違う言語・技術を利用できる
- もちろん大変なこともある

### 現在のFRESHLIVE
- Golang, Kotlinのハイブリッド
-- 配信システム、低レイヤーはGo
-- 新規APIは基本Kotlin
- REST+gRPC

## Kotlin採用の背景
- 最初はGo一辺倒だった
- APIをGoでいっぱい書くのはつらい
- Microservicesだし言語自由でいいじゃん

### メンバーの心の叫び
Javaを活かした言語だからいい叫びがある

### 開発方針
- APIは基本Kotlin

### 採用しているFramework
- Spring Boot 2
- Spark Framework 2.7

### Stack
- Spring Boot 2 / Spark 2.7
- grpc-java
- Jackson
- Doma2
- REST+gRPC
- kotlinx.coroutine

### RESTful API
- Router Function DSL
- Spring5のKotlinサポートで登場

WebTestClient

### gRPCとSpring
- grpc-spring-boot-startar で連携
- Springの資産を活かしながらgRPCができる

### Spring BootとKotlinの所感
写真とった


## Spark Framework

### build.gradle
dependenciesの書き方。Anubisでやってるから省略。

### DI
SparkにはDIに対する機能が豊富ではない、ので愚直にDIしていく。
か、Kodein というDIライブラリを使う。

### 薄いから拡張関数が大活躍する
軽量で機能の少ないフレームワークなので、Kotlinの拡張関数をどんどん定義していける。

### 所感
- 構成、ライブラリの組み合わせの自由さ
- DIの愚直さはあるが、はまりポイント少ない
- Kotlinでより簡素にかけるし、拡張関数を使えばより強力になる


## 運用

### grpc-java CPUが突然跳ねる問題
- 原因はNettyのObjectCleanerThread（解決済み）
- grpc-java 1.12.0 以降を使いましょう

### .proto管理の方法
- リポジトリごとのproto群から、依存するprotoをServiceに配置
- protodepというツールを作成し、protoの配置・管理を簡素化

### packaging / deploy
写真とった

### Monitoring
- JVM Micrometer + Prometheus 
- 各ServiceにMicrometerのエンドポイントを仕込んで、Prometheusからスクレイピング

## まとめ
写真とった



