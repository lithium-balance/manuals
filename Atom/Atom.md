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
* linter-textlint  (Timecopをみると時間がかかっているようだが...)

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
* project-manager

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

### 共通の設定

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


### Windowsでの設定

#### パッケージインストール時のエラーを解消する
以下のコマンドをコマンドプロンプトにて実行する。

    setx ATOM_NODE_URL http://gh-contractor-zcbenz.s3.amazonaws.com/atom-shell/dist /M

#### 設定
Windows7環境にて、以下の設定を行っている。

* 設定
  - フォントの指定は`設定(Settings)`では実施しない。
  - `不可視文字を表示`にチェックを入れたいのだが、表示が微妙に...

* styles.less
  - 以下の設定を追加している。  
  ※`Source Han Code JP N`は全角と半角の幅が3:2なので、エディタ内での使用には違和感がある。  
  ※Markdown Preview内で`Source Han Code JP N`を使用する分には違和感がない。

~~~~css
// Styles for the markdown preview.
@editor-fonts: "Myrica M", "Migu 1M", "TakaoGothic", monospace;
@line-number-fonts:        "Migu 1M", "TakaoGothic", monospace;
@preview-fonts: "Source Han Code JP N", Meiryo, 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif;

// `設定`の`エディタ設定`にある`フォント`の設定を行うと、Markdownをhtml出力した際に`code`タグにて、その設定したフォントが個別に指定されてしまう。(非常に煩わしい)
// よって、styles.lessにてフォントの設定を行う。
atom-text-editor {
  font-family: @editor-fonts;
  font-size: 15px;
}
// "Myrica M"を用いると、行番号の表示がずれてしまうので、行番号には"Myrica M"を用いない
atom-text-editor::shadow {
    .line-number {
        font-family: @line-number-fonts;
    }
}
// Markdown Previewのスタイル設定
.markdown-preview {
   font-family: @preview-fonts;
   // インラインコードの類はフォントサイズを小さくしない
   code, tt, kbd, samp, blockquote {
       font-family: @editor-fonts;
       font-size: 1em;
   }
   // コードブロックはフォントサイズ小さめ
   atom-text-editor {
       font-family: @editor-fonts;
   }
}
// html出力時にはフォント指定をブラウザの設定にまかせる
.markdown-preview[data-use-github-style] {
   font-family: sans-serif;
}
// GitHubのスタイルだとシンタックスハイライトが見づらかったので変更
.markdown-preview[data-use-github-style] .highlight pre, .markdown-preview[data-use-github-style] pre {
    background-color: #1d1f21;
}
~~~~

#### atom.exeの置き場所
Windowsでは、`C:\Users\<ユーザ名>\AppData\Local\atom\app-<バージョン>` に置いてあった。


### Lubuntuでの設定

#### 設定

* 設定
  - フォントを`TakaoGothic`に設定する。
