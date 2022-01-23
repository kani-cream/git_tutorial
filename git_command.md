# Let's Git Command !

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
