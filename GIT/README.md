# GIT相关

## git fetch 与 pull 的区别
* git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。
* git pull 则是将远程主机的最新内容拉下来后直接合并，即：git pull = git fetch + git merge。

## git reset --soft 与 --hard 的区别

* git reset –-soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可；
* git reset -–hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容，撤销的commit中所包含的更改被冲掉