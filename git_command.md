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
