# GIT相关

1. [git config](#git-config)
2. [git remote](#git-remote)
3. [git sync](#git-sync)
4. [git submit](#git-submit)
5. [git undo](#git-undo)
6. [git branch](#git-branch)

## git config
全局配置 git 用户名与邮箱
```bash
git config --global user.name "yourname"
git config --global user.email "your_email@youremail.com"
```

## git remote
与远程仓库相关的 git 命令
```bash
git remote add <origin> git@github.com:qqwqqk/PreparationDocument.git
git remote -v
git remote rm <origin>
```

## git sync
远程同步相关的 git 命令
```bash
git fetch origin <originbranch>
git pull origin <originbranch>:<localbranch>
```

## git submit
提交与推送相关的 git 命令
```bash
git add .
git commit -m 'message'
git push origin <localbranch>:<originbranch>
```

## git undo
撤消相关的 git 命令
```bash
git log

git reset --hard <commit_id>
git reset --hard HEAD^
git reset --soft HEAD^

git revert HEAD
```

## git branch
分支相关的 git 命令
```bash
git branch
git branch <branchname>
git branch -d <branchname>
git branch -m <oldbranch> <newbranch>

git push <origin> --delete <originbranch>

git checkout <branchname>
git checkout -b <branchname>

git merge <targetbranch>
```
