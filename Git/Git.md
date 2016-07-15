Git操作メモ
===========
必要最小限なGitの操作方法(個人利用)


初期設定
========
gitの設定は、ユーザのホームディレクトリに作成される`.gitconfig`ファイルに記録される。
直接ファイルを編集することもできるが、以下のconfigコマンドを使って設定できる。

    git config --global user.name "<ユーザ名>"
    git config --global user.email "<メールアドレス>"

次のコマンドで出力をカラー表示することができる。

    git config --global color.ui auto


Gitとsvnとのコマンド対比
========================

|              |              svn               |         git         |
|--------------|--------------------------------|---------------------|
|更新          |svn update                      |git pull             |
|コミット      |svn commit                      |git add → git commit or git commit -a → git push <url>|
|追加          |svn add <file or dir>           |git add              |
|削除          |svn rm <file or dir>            |git rm <file>        |
|移動          |svn mv <file or dir>            |git mv <file>        |
|変更取り消し  |svn revert <file>               |git checkout <file>  |
|ログ          |svn log                         |git log              |
|差分          |svn diff                        |git diff             |
|スイッチ      |svn switch <url>                |git checkout <branch>|
|チェックアウト|svn checkout <url> .            |git clone <url> .    |
|状態          |svn status                      |git status           |
|ブランチ作成  |svn copy <url> <url>            |git branch <branch>  |
|タグ作成      |svn copy <url> <url>            |git tag <tag>        |
|マージ        |svn merge -r <rev1>:<rev2> <url>|git merge <branch>   |

参考: http://qiita.com/sugarshin/items/0394e9ad867951dd74fe


クローン
========
SVNのチェックアウトみたいなもの。
SVNと違って、Gitはリポジトリの全てをコピーしてくる(一部だけではない)ので、SVNとは名称が異なる。

    git clone <repository> <directory>

例

    git clone https://github.com/lithium-balance/manuals.git manuals

あるいは、以下のようにすれば`<directory>`の指定は不要。

    cd <directory>
    git clone <repository>


コミット
========
変更分をローカルにコミットする。
あらかじめ変更したコミット対象をインデックスに登録しておく必要がある。

    git add <file>
    git commit -m "<コミットメッセージ>"

git add の使い方
----------------
- `git add .`       ： 全てのファイルやディレクトリを追加
- `git add -n`      ： 追加されるファイルを調べる
- `git add -u`      ： 変更されたファイルを追加する
- `git rm --cached` ： addしたファイルを除外する

git commit の使い方
-------------------
- `git commit -a`      ： 変更のあったファイル全てをコミットする
- `git commit --amend` ： 直前のコミットを取り消す
- `git commit -v`      ： 変更点を表示してコミット

コミットの取り消し方
--------------------
- `git reset --soft HEAD~2` ： 最新のコミットから2件分をワークディレクトリの内容を保持し取り消す
- `git reset --hard HEAD~2` ： 最新のコミットから2件分のワークディレクトリの内容とコミットを取り消す

コミットメッセージの修正
------------------------
1. 以下のコマンドを実行すると、HEADから2件のコミットメッセージがエディタ上に表示される。
   `git rebase -i HEAD~2`
2. コミットメッセージは以下のように表示されるので、コミットメッセージを修正し、`pick`の部分を`edit`あるいは`e`へ変更し、ファイル保存する。
   `pick {<commit_id>} {<commit_meessage>}` // 2件目
   `pick {<commit_id>} {<commit_meessage>}` // 1件目(最新コミット)
3. 以下のコマンドにてコミットする。
   `git commit --amend`
4. 以下のコマンドを実行すれば完了。
   `git rebase --continue`


プッシュ
========
ローカルリポジトリの変更分をリモートリポジトリに反映する。

    git remote add <name> <url>
    git push origin master

例
    git remote add origin https://github.com/lithium-balance/manuals.git
    git push origin master

フェッチ
========
リモートリポジトリの変更分をローカルリポジトリに反映する。
ローカルのファイルに反映されるわけではない。

    git fetch

プル
====


差分表示
========
- `git diff` ： ローカルリポジトリとの差分を表示
- `git diff HEAD^` ： 最後のコミットからの差分を表示
- `git diff --name-only HEAD^` ： 差分のあるファイルを表示
- `git diff file1.txt file2.txt` ： 特定ファイルの差分
- `git diff commit1 commit2` ： コミットの差分


ログ
====
コミットログを表示する。

    git log
