---
title: Braveブラウザ
date: 2025-10-28
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


UbuntuにBraveブラウザをインストールする方法はいくつかありますが、公式のリポジトリを追加してAPTパッケージマネージャーからインストールするのが最も推奨される方法です。これにより、今後も簡単にアップデートを受け取ることができます。

以下の手順でインストールできます。

**ステップ1: 必要なパッケージのインストール**
まず、Braveのリポジトリを追加するために必要な`curl`と`apt-transport-https`パッケージがシステムにインストールされていることを確認します。通常は既にインストールされていますが、念のため実行しておきましょう。

```bash
sudo apt update
sudo apt install curl apt-transport-https
```

**ステップ2: BraveのGPGキーの追加**
Braveのリポジトリのパッケージが正規のものであることをシステムが確認できるように、GPGキーを追加します。

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

**ステップ3: Braveのリポジトリを追加**
次に、BraveブラウザのAPTリポジトリをシステムのソースリストに追加します。

```bash
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```

**ステップ4: パッケージリストの更新**
新しいリポジトリが追加されたので、パッケージリストを更新します。

```bash
sudo apt update
```

**ステップ5: Braveブラウザのインストール**
最後に、Braveブラウザをインストールします。

```bash
sudo apt install brave-browser
```

これでBraveブラウザがインストールされました。

**インストール後の起動方法:**
アプリケーションメニューから「Brave」または「Brave Browser」と検索して起動できます。
ターミナルから起動する場合は、以下のコマンドを実行します。
```bash
brave-browser
```

**アンインストールしたい場合:**
もしBraveブラウザをアンインストールしたい場合は、以下のコマンドを実行します。
```bash
sudo apt remove brave-browser
sudo apt autoremove
```

この方法でインストールすれば、今後のシステムアップデートでBraveも自動的に最新の状態に保たれるので便利です。