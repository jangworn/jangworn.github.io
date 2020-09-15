---
title: git修改已commit的name和email
date: 2020-06-03 23:40:58
tags: git 
---

1. 拉取要修改的仓库  
   git clone https://xxx/xxxx.git
2. 进入本地目录  
   cd xxxx

3) 拉取远程所有分支  
   git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done  
   git fetch --all  
   git pull --all

4. 执行修改命令

```
git filter-branch --env-filter '

OLD_EMAIL="xxx@163.com"
OLD_NAME="xxx@163.com"
CORRECT_NAME="bbbbb"
CORRECT_EMAIL="bbbbb@qq.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_NAME" = "$OLD_NAME" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

5. 把修改 commit 信息提交  
   git push --force --tags origin 'refs/heads/\*'
