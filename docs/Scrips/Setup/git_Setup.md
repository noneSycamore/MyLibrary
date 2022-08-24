# Git Seting up

## init github repo

```shell
git init
git config --global user.name "nonesycamore"
git config --global user.email "sycamore.none@gmail.com"
```
（Private）获取 Personal access tokens
```shell
git remote add <repo_name> https://<token>@github.com/noneSycamore/<repo_name>.git
```
更改 **branch**: main --> master

将仓库的文件先pull到本地:
```shell
git pull <repo_name> master
```
## update repo

When pushing files: 

Windows:

```bat
@ECHO OFF
git add *
git commit -m 'update'
git push script_sh master
PAUSE
```

Linux:

```shell
git add *
git commit -m 'update'
git push transfer master
```