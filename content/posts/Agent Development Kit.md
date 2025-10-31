---
title: Agent Development Kit
date: 2025-10-31
lead: ""
description: Example article description
categories:
  - 随筆
tags:
  - 徒然
  - ai
menu: main
comments: false
authorbox: false
pager: true
toc: true
mathjax: true
sidebar: right
widgets:
  - search
  - recent
  - taglist
---


Googleの **Agent Development Kit (ADK)** は、主に **Googleアシスタント (Google Assistant)** 上で動作するカスタムエージェント（またはアクション）を開発するためのSDK（ソフトウェア開発キット）を指します。

これは、ユーザーが「OK Google」と話しかけることで操作できる、スマートスピーカー（Google Home/Nest）、スマートフォン、スマートディスプレイなどのデバイス上で動作する独自の機能やサービスを作成するためのツールセットです。

### Agent Development Kit (ADK) の主な特徴と提供された時代背景

*   **Googleアシスタントの登場初期:** ADKという名称は、Googleアシスタントが普及し始めた初期の頃に、開発者がアシスタント向けのカスタム機能を開発する際に使われていました。当時は、主に「Actions on Google」というプラットフォーム上で、ユーザーと対話する「Agent (エージェント)」または「Action (アクション)」を構築するためのツールとして提供されていました。
*   **Dialogflowとの連携:** ADKの主要な部分は、Googleの自然言語理解（NLU）プラットフォームである **Dialogflow** と密接に連携していました。開発者はDialogflowを使って、ユーザーの発話意図（インテント）と情報の抽出（エンティティ）を定義し、エージェントの会話フローを設計しました。
*   **SDK/ライブラリの提供:** 特定のプログラミング言語（例えばNode.js用のクライアントライブラリなど）で、GoogleアシスタントAPIと連携するためのSDKやライブラリが提供され、開発者がエージェントのロジックを実装できるようになっていました。

### 現在の状況と進化

「Agent Development Kit (ADK)」という厳密な名称は、現在では公式ドキュメントで以前ほど強調されて使われることは少なくなっています。しかし、その機能と目的は、現代のGoogleアシスタント開発エコシステムに引き継がれています。

現在のGoogleアシスタント向け開発の主要なコンポーネントは以下の通りです。

1.  **Actions on Google (Actions Console):**
    *   Googleアシスタント向けのカスタム機能（アクション）を定義、設定、デプロイするためのプラットフォームです。このコンソールからDialogflowエージェントをアシスタントに接続したり、Webhookを設定してバックエンドロジックを実装したりします。これが、かつてのADKが対象としていた「エージェント開発」の中心的な場所です。

2.  **Dialogflow:**
    *   引き続き、Googleアシスタントの会話型インターフェースの核となるNLUエンジンとして機能します。ユーザーの発話を理解し、エージェントの会話フローを管理します。

3.  **Webhook (Cloud Functions, etc.):**
    *   エージェントがユーザーの意図を理解した後、実際のビジネスロジック（データベースからの情報取得、外部APIの呼び出しなど）を実行するためのバックエンドコードは、Webhookとして提供されます。Google Cloud Functionsのようなサーバーレス機能がよく利用されます。

4.  **Google Assistant SDK (for Devices):**
    *   これは少し異なる文脈で使われますが、Googleアシスタントの機能をカスタムハードウェアデバイスに組み込むためのSDKも存在します。これは、スマートスピーカーのようなデバイスを自作したい開発者向けです。

### まとめると

Googleの **Agent Development Kit (ADK)** は、Googleアシスタント向けのカスタムエージェント（アクション）を開発するための、かつての包括的な呼び名でした。現在では、その機能は主に **Actions on Google** と **Dialogflow** を中心としたツールとプラットフォームに引き継がれ、さらにバックエンドのWebhook実装と組み合わせて開発が進められています。

これは、AIエージェントの非常に具体的な一分野（Googleアシスタント上での会話型エージェント）に特化した開発キットだったと言えます。