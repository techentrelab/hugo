---
title: Lubuntu  日本語入力
date: 2025-10-20
lead: ""
description: Example article description
categories:
  - 随筆
tags:
  - 徒然
  - linux
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



---

## Lubuntu  日本語入力のセットアップガイド

###  日本語入力エンジン「Mozc」の導入

まず、日本語入力に必要な「fcitx-mozc」をインストールします。

1.  **システムを更新し、`fcitx-mozc`をインストールします。**

    ```bash
    sudo apt update
    sudo apt install fcitx-mozc
    ```
2.  **再ログイン後、設定を確認します。**
    ログアウトして再度ログインし、「入力メソッドの設定」を開いてください。以下の項目が表示されていれば、インストールは成功です。
    *   キーボード - 日本語
    *   Mozc

    



