---
title: "LubuntuでFcitx5"
date: 2025-10-21
lead: ""
description: Example article description
categories:
  - 随筆
tags:
  - 徒然
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


### LubuntuでFcitx5を導入する手順

以下に、LubuntuにFcitx5を導入する一般的な手順を示します。

1.  **システムを更新する:**
    まず、パッケージリストを更新し、システムを最新の状態に保ちます。
    ```bash
    sudo apt update
    sudo apt upgrade
    ```

2.  **Fcitx5と必要な入力メソッドをインストールする:**
    Fcitx5本体と、日本語入力に必要なエンジン（例: Mozc）をインストールします。
    ```bash
    sudo apt install fcitx5 fcitx5-mozc fcitx5-frontend-qt5 fcitx5-frontend-gtk3 fcitx5-frontend-gtk4
    ```
    *   `fcitx5`: Fcitx5本体
    *   `fcitx5-mozc`: 日本語入力エンジン（Google 日本語入力のオープンソース版）
    *   `fcitx5-frontend-qt5`, `fcitx5-frontend-gtk3`, `fcitx5-frontend-gtk4`: それぞれQt5、GTK3、GTK4アプリケーションでFcitx5が機能するためのモジュール。Lubuntu（LXQt）はQtベースですが、GTKアプリケーションも利用するため、これらもインストールしておくと良いでしょう。

    **他の入力メソッドが必要な場合:**
    *   Anthy: `fcitx5-anthy`
    *   rime: `fcitx5-xkb-extras-rime` など

3.  **環境変数を設定する:**
    Fcitx5をシステム全体の入力メソッドとして認識させるために、以下の環境変数を設定する必要があります。これは、ユーザーのホームディレクトリにある`.xprofile`ファイルに記述するのが一般的です。

    `.xprofile`ファイルを作成または編集します。
    ```bash
    nano ~/.xprofile
    ```
    以下の行を追加します（もし既存の設定があれば、それに合わせて調整してください）。
    ```
    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XMODIFIERS=@im=fcitx
    export INPUT_METHOD=fcitx
    export SDL_IM_MODULE=fcitx
    ```
    ファイルを保存して閉じます（Ctrl+O, Enter, Ctrl+X）。

4.  **Fcitx5を自動起動に設定する:**
    Fcitx5がLubuntuの起動時に自動的に開始されるように設定します。
    ```bash
    nano ~/.config/lxsession/Lubuntu/autostart
    ```
    以下の行を追加します（もし既存の設定でFcitx4などが起動している場合は、その行を削除またはコメントアウトしてから追加してください）。
    ```
    @fcitx5 -d
    ```
    `-d` はデーモンとして起動するオプションです。

5.  **設定を反映させるために再起動する:**
    上記の設定変更を適用するには、一度ログアウトして再度ログインするか、システムを再起動する必要があります。

6.  **Fcitx5を設定する:**
    システムが起動したら、Fcitx5の設定ツールを開いて、入力メソッド（Mozcなど）を追加します。
    *   アプリケーションメニューから「Fcitx5設定」のような項目を探して起動するか、ターミナルで `fcitx5-configtool` と入力して起動します。
    *   「入力メソッド」タブに移動し、左下の「+」ボタンをクリックします。
    *   「現在の入力メソッドのみ表示」のチェックを外し、「Mozc」を検索して選択し、「OK」をクリックして追加します。
    *   必要に応じて、キーボードレイアウト（例: 日本語キーボード）も追加します。

7.  **動作確認:**
    テキストエディタやウェブブラウザなどを開き、キーボードで日本語入力ができるか（通常は `半角/全角` キーで切り替え）確認します。Fcitx5のアイコンがシステムトレイに表示されているはずです。

### トラブルシューティング

*   **アイコンが表示されない、または日本語入力ができない場合:**
    *   上記の「Lubuntuで起動時にFcitxのキーボードアイコンがステータスバーに表示されない理由」で挙げた対処法（特に`.xprofile`と`autostart`の確認）を参考にしてください。
    *   `~/.xprofile` や `~/.bashrc` などのファイルに、以前のFcitx4やIBusなどの入力メソッドに関する環境変数設定が残っている場合、それらを削除またはコメントアウトしてください。
    *   LubuntuのLXQtパネルのシステムトレイ設定で、Fcitx5がブロックされていないか確認してください。

Fcitx5は現代的な入力メソッドフレームワークであり、LubuntuのQtベースのデスクトップ環境とも相性が良いことが多いです。ぜひお試しください。
