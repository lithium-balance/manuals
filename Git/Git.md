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
SVNのチェックアウトみたいなもん。  
SVNと違って、Gitはリポジトリの全てをコピーしてくる(一部だけではない)ので、名称が異なる。

    git clone <repository> <directory>

例

    git clone https://github.com/lithium-balance/manuals.git manuals


コミット
========
変更分をローカルにコミットする。  
あらかじめ変更したコミット対象をインデックスに登録しておく必要がある。

    git add <file>
    git commit -m "<コミットメッセージ>"


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
