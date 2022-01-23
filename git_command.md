# <b> Let's Git Command !</b>

## $ git fetch [リモート名]
```
$ git fetch origin
```
リモートリポジトリからローカルリポジトリに情報を取ってくる。<br>
ワークツリーには、変更は反映されない。<br>
保存場所:remotes/remotes/[branch]<br>

## $ git pull
```
$ git pull [リモート名] [ブランチ名]
$ git pull origin main

# 省略
$ git pull

# 代用
$ git fetch origin main
$ git merge origin/master
```
リモートリポジトリからローカルリポジトリに情報を取ってきて、更新分をワークツリーに反映させる。<br>

#### <b> $ git pull の注意点</b><br>
ワークツリーにbranch master, hogeの2つが存在する。自分のワークツリーがmasterを向いているとき、hogeブランチの更新分を取得する「$ git pull origin hoge」を実行すると、ローカルリポジトリのremotes/origin/hogeに情報が格納され、現在のワークツリー「master」にhogeの更新分がマージされる。<br>
hogeブランチに更新分を取得しようとしているにもかかわらず、意図せずmasterブランチに反映される可能性があるので、注意！！<br>

## $ git remote show [リモート名]
$ git remote のより詳しい情報を見る。<br>
$ git remote show origin
* 表示される情報
  * FetchとPushのURL
  * リモートブランチ
  * git pullの挙動
  * git pushの挙動

## $ git remote rename / rm
$ git remote rename リモート名を変更する
```
$ git remote rename [旧リモート名] [新リモート名]
```
$ git remote rm リモートを削除する
```
$ git remote rm [リモート名]
```

## ブランチの役割と仕組み
* 分岐させて複数の機能・開発者が同時並行で開発するための仕組み
* ブランチとは、コミットを示すポインタ
* HEADは、作業しているブランチを示している
* コミットを示すポインタなので、ブランチの作成・切替・マージが他のバージョン管理ツールに比べて高速 (ポインタを切り替えるだけ)

## $ git branch ブランチの一覧/ブランチの作成
```
## ローカルリポジトリのブランチ一覧を表示
$ git branch

## remotesブランチも表示させる
$ git branch -a

## ブランチの作成 ( ローカルリポジトリにブランチを作成する、HEADは移動しない。 )
$ git branch [ブランチ名]

## リモートブランチからローカルブランチを作成する
$ git branch master origin/master

## 現在のHEADを知る方法
$ git log --oneline --decorate
87bf06c (HEAD -> main, origin/main, feature) add git remote show 追記
...
```

## $ git checkout ブランチ切替
```
## ブランチの切り替え
$ git checkout [ブランチ名]

## ブランチの新規作成と切替
$ git checkout -b [ブランチ名]
```

## $ git merge 変更履歴をマージする
```
$ git merge [ブランチ名]
$ git merge [リモート名/ブランチ名]
$ git merge origin/master
```
#### マージの３種類
* Fast Forward: 早送りマージ
  * 変更されていないmasterブランチから新しくhotfixブランチを作成してhotfixブランチの変更分をmasterブランチにマージするとき、masterのポインタが前に進むだけ。
* Auto Merge: 基本的なマージ
  * masterブランチとfeatureブランチでそれぞれコミットが存在するとき、git merge featureでmasterにfeatureブランチの変更分を取り込んだ時、masterブランチにマージコミットという新しいコミットファイルが作成される。<br>マージコミットファイルには、親を２つ持つことになる(masterコミットとfeatureコミット)。
* conflict:コンフリクト
  * 同じファイルの同じ行に対して異なる編集を行ったとき、<br>
  どちらの更新を優先すればいいのかGitがわからないときに発生する。

## コンフリクトが発生したとき
```
> git merge feature
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html

> cat index.html
...
<<<< HEAD
<p>git addについて学ぶ</p>
====
<p>gitcommitを知る</p>
>>>> feature
...
## HEADから====までが現在のブランチに記載されている内容
## ====からfeatureまでがfeatureブランチに記載されている内容
## HEADの内容をmasterとする場合は、HEADの内容のみを記載する。
## featureの内容を残す場合は、featureの内容のみを記載する。
## どちらも残す場合は、HEADの内容とfeatureの内容を記載する。
## 残す内容が決まったら、Gitが記載した<<<< HEADから>>>featureを削除して保存する。

> git add index.html
> git commit
## 変更分をコミットして完了
```

## コンフリクトを起きないようにするには
* 複数人で同じファイルを更新しない
* pull, mergeする前に変更中の状態をなくす（commitやstashをしておく）
* pullするときは、pullするブランチに移動してからpullする
* コンフリクトしても慌てない

## $ git branch -m/-d branchのリネームと削除
```
## ブランチ名の変更
$ git branch -m [ブランチ名]
$ git branch -m new_branch

## ブランチの削除
$ git branch -d [ブランチ名]
$ git branch -d feature

### 強制削除
$ git branch -D [ブランチ名]

## リモートブランチの削除
$ git push --delete origin [ブランチ名]
$ git push origin :[ブランチ名]
```

## $ git rebase [ブランチ名] 履歴を整えよう
$ git rebaseは、ブランチの起点となるコミットを別のコミットに移動すること<br>
ブランチがmaster, featureの2つ存在していて、featureにmasterの更新分を反映させたいとしたとき、
```
$ git checkout feature
$ git rebase master
```
さらに、featureの更新分をmasterにマージすることもできる
```
$ git checkout master
$ git merge feature
```
