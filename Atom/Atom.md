Atomの設定 共通
===============

[本家 https://atom.io/](https://atom.io/)

導入したパッケージ
------------------
* file-icons
* highlight-line
* japanese-menu
* language-markdown
* markdown-pdf
* markdown-preview-opener
* markdown-scroll-sync
* markdown-writer
* nav-panel

未導入なパッケージ
------------------
* minimap
* minimap-autohide
* minimap-highlight-selected
* linter
* atom-beautify
* highlight-selected
* tree-view-finder
* symbols-tree-view
* show-ideographic-space

無効化したパッケージ
--------------------
* language-gfm
* spell-check

ネタパッケージ
--------------
* activate-power-mode
* activate-power-mode-delete

※`activate-power-mode-delete`はdelete時のみ動作するものであり、`activate-power-mode`が有効ならこちらは不要。

導入したテーマ
--------------
* atom-dark-ui-slim

設定
----

* 設定
  - `空になったウィンドウをタブと同様に閉じる`のチェックを外す
  - `ソフトラップ`にチェックを入れる
* markdown-preview
  - Use GitHub.com style にチェックを入れる
* language-markdown
  - `Disable language-gfm`のチェックを外す
  - `Soft Wrap`のチェックを外す
* whitespace
  - `Ignore Whitespace Only Lines`にチェックを入れる
  - `Remove Trailing Whitespace`のチェックを外す


Windowsでの設定
===============

パッケージインストール時のエラーを解消する
------------------------------------------
以下のコマンドをコマンドプロンプトにて実行する。

    setx ATOM_NODE_URL http://gh-contractor-zcbenz.s3.amazonaws.com/atom-shell/dist /M

設定
----

* 設定
  - フォントに`Migu 1M`、フォントサイズを15に設定する。  
    ※`Myrica M`だと、ソフトラップ時の行番号表示がずれる  
    ※`Source Han Code JP N`は全角と半角の幅が3:2なので違和感がある。
  - `不可視文字を表示`にチェックを入れたいのだが、表示が微妙に...
