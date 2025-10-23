---
title: "Fcitxのキーボードアイコン"
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


Lubuntuで起動時にFcitxのキーボードアイコンがステータスバー（システムトレイ）に表示されない場合、いくつかの原因が考えられます。

考えられる原因と対処法をいくつかご紹介します。

### 1. Fcitxが正しく起動していない、または遅延して起動している

Fcitxが完全に起動する前にシステムトレイが描画されてしまうと、アイコンが表示されないことがあります。

*   **対処法:**
    *   **Fcitxの自動起動設定を確認する:**
        1.  `~/.config/lxsession/Lubuntu/autostart` または `~/.config/lxsession/LXDE/autostart` ファイルを開きます（なければ作成）。
        2.  以下の行を追加します（もしあれば、重複しないように注意してください）：
            ```
            @fcitx-autostart
            ```
        3.  または、グラフィカルなツールで設定します。Lubuntuのバージョンによって場所が異なりますが、「設定」>「セッションと起動」>「自動開始アプリケーション」のような項目を探し、Fcitxが有効になっていることを確認します。
    *   **遅延起動を試す:**
        Fcitxの起動を少し遅らせることで、システムトレイに表示されることがあります。
        `autostart` ファイルに以下のように記述することで、数秒後にFcitxを起動できます。
        ```
        @sh -c "sleep 5 && fcitx-autostart"
        ```
        `5` の部分は秒数で、必要に応じて調整してください。

### 2. システムトレイアプレットの設定

Lubuntuのシステムトレイ（LXQt PanelまたはLXDE Panel）の設定で、表示するアプレットが制限されている場合があります。

*   **対処法:**
    *   **パネル設定を確認する:**
        1.  システムトレイがあるパネル上で右クリックし、「パネルの設定」または「パネルのカスタマイズ」のような項目を選択します。
        2.  アプレットの一覧の中に「システムトレイ」または「通知領域」のようなものがあるはずです。その設定を開き、Fcitxがブロックされていないか、または表示が許可されているかを確認します。
        3.  **LXDEの場合:** `lxpanelctl restart` を試すか、`~/.config/lxpanel/LXDE/panels/panel` ファイルを編集して、`Plugin "systray"` セクションで `StatusNotifierHosts` に `fcitx` を追加する必要があるかもしれません。

### 3. Fcitxの設定の問題

Fcitx自体の設定で、アイコンの表示が抑制されている可能性は低いですが、念のため確認できます。

*   **対処法:**
    *   **Fcitx設定ツールを起動する:**
        1.  ターミナルで `fcitx-configtool` と入力するか、アプリケーションメニューから「Fcitx設定」のようなものを探して起動します。
        2.  特にアイコン表示に関する設定はあまりありませんが、全体の設定に問題がないか確認します。

### 4. 環境変数の設定

Fcitxが正しく動作するために必要な環境変数が、Lubuntuの起動時に適切に設定されていない場合があります。

*   **対処法:**
    *   **`~/.xprofile` または `~/.bashrc` に設定を追加する:**
        `~/.xprofile` ファイル（なければ作成）に以下の行を追加します。これはXセッション開始時に実行されます。
        ```
        export GTK_IM_MODULE=fcitx
        export QT_IM_MODULE=fcitx
        export XMODIFIERS=@im=fcitx
        ```
        `~/.bashrc` に追加することもできますが、`~/.xprofile` の方がより広範囲に適用されます。変更を適用するには、一度ログアウトして再度ログインするか、再起動が必要です。

### 5. Fcitxとデスクトップ環境の競合（まれ）

まれに、FcitxとLubuntuの特定のバージョン（LXQtまたはLXDE）の間で、システムトレイの描画に関する競合が発生することがあります。

*   **対処法:**
    *   **Fcitxの再インストール:**
        ```bash
        sudo apt update
        sudo apt remove --purge fcitx fcitx-*
        sudo apt install fcitx fcitx-mozc # または必要な入力メソッド
        ```
        これにより、設定ファイルを含めてFcitxを完全に削除し、再インストールします。
    *   **ログを確認する:**
        `~/.xsession-errors` や `journalctl -xe` などのログファイルに、Fcitx関連のエラーメッセージが出ていないか確認します。

### 6. アップデート後の問題

LubuntuやFcitxのアップデート後に問題が発生した場合は、一時的なバグである可能性もあります。

*   **対処法:**
    *   **システムを最新の状態に保つ:**
        ```bash
        sudo apt update
        sudo apt upgrade
        sudo apt autoremove
        sudo apt clean
        ```
    *   **オンラインで同様の報告がないか検索する:**
        LubuntuのバージョンとFcitxのバージョンを明記して、フォーラムやバグレポートを検索してみるのも有効です。

---

**試す際のポイント:**

1.  **一度に1つの変更を試す:** 複数の設定を同時に変更すると、何が原因で解決したのか、または問題が悪化したのかが分かりにくくなります。
2.  **ログアウト・ログインまたは再起動:** 多くの設定変更は、セッションを再開しないと反映されません。
3.  **Fcitxが実際に動作しているか確認する:** アイコンは表示されなくても、実際に日本語入力ができればFcitx自体は起動しています。その場合は、アイコン表示の問題に絞って対処します。
4.  **ターミナルからFcitxを起動してみる:** `fcitx -d` でFcitxをデバッグモードで起動し、エラーメッセージが出ないか確認します。

上記の対処法を順番に試してみて、Fcitxのアイコンが表示されるか確認してください。