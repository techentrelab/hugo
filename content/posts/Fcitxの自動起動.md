---
title: Fcitxの自動起動
date: 2025-10-21
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


Lubuntuのデスクトップ環境（LXQt）でFcitxの自動起動を設定する方法はいくつかあります。最も確実で推奨される方法をいくつかご紹介します。

### 1. LXQtの自動起動設定（推奨）

LubuntuのLXQt環境には、アプリケーションの自動起動を管理するためのGUIツールがあります。

1.  **スタートメニューを開く:** 画面左下のメニューアイコンをクリックします。
2.  **設定を開く:** 「設定」または「Preferences」を選択します。
3.  **LXQt設定センターを開く:** 「LXQt 設定センター」または「LXQt Settings Center」を選択します。
4.  **自動起動を選択:** 左側のリストから「自動起動」または「Autostart」を選択します。
5.  **「追加」をクリック:** 右上の「追加」ボタンをクリックします。
6.  **Fcitxのコマンドを入力:**
    *   **名前 (Name):** `Fcitx` （わかりやすい名前）
    *   **コマンド (Command):** `fcitx -d` （または `fcitx` のみでも動作することが多いですが、`-d` はデーモンとして起動するオプションです。）
    *   **説明 (Description):** `Fcitx Input Method` （オプション）
7.  **「OK」をクリック**して追加し、設定センターを閉じます。

これで次回ログイン時にFcitxが自動的に起動するはずです。

### 2. .desktopファイルを直接配置する

もしGUIツールが見つからない、または使いたくない場合は、手動で `.desktop` ファイルを作成して配置することもできます。

1.  **ファイルマネージャーを開く:** 「PCManFM-Qt」などのファイルマネージャーを開きます。
2.  **ホームディレクトリに移動:** 自分のホームディレクトリ (`/home/your_username/`) に移動します。
3.  **隠しファイルを表示:** `Ctrl + H` を押すか、メニューから「表示」→「隠しファイルを表示」を選択して、隠しファイルを表示させます。
4.  **`~/.config/autostart/` ディレクトリに移動:**
    このディレクトリがなければ作成してください。
    `mkdir -p ~/.config/autostart/`
5.  **新しいファイルを作成:** `fcitx.desktop` という名前の新しいファイルを作成し、以下の内容を貼り付けます。

    ```ini
    [Desktop Entry]
    Type=Application
    Name=Fcitx
    Comment=Fcitx Input Method
    Exec=fcitx -d
    Icon=fcitx
    Terminal=false
    Categories=System;
    StartupNotify=false
    ```
6.  ファイルを保存します。

これも次回ログイン時にFcitxを自動起動させる方法です。

### 3. 環境変数の設定

Fcitxは、適切な環境変数が設定されていないと、アプリケーションが入力メソッドを認識できないことがあります。多くの場合は自動で設定されますが、もしFcitxが起動しても入力できない場合は、以下の環境変数を設定する必要があるかもしれません。

以下の行を `~/.profile` または `~/.xprofile` に追加します。

```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

変更を適用するには、一度ログアウトして再度ログインするか、ターミナルで `source ~/.profile` (または `source ~/.xprofile`) を実行します。

### 確認

設定後、一度ログアウトし、再度ログインしてみてください。

*   Fcitxが起動しているか（タスクトレイにアイコンが表示されるか）
*   各アプリケーション（Firefox、LibreOfficeなど）で日本語入力が可能か

を試して確認してください。

これでLubuntu環境でFcitxを自動起動させ、日本語入力を使用できるようになるはずです。