# Welcome to Sycamore の Library

> A Library to store some Scrips...

Tree:

```
Math_modeling
├── Assignment 1.md
└── Starting.md

Scrips
├── CTF_quiz
│   ├── Crypto
│   │   └── Multiple_Chaos_Maps
│   │       ├── chaos.md
│   │       └── exp.md
│   └── Misc
│       └── Chaos_and_Pic
│           └── chaos.md
├── CTF_scrips
│   ├── Caser_爆破.md
│   ├── RSA_常见.md
│   ├── SHA256_验证码爆破.md
│   ├── base64_多行.md
│   ├── secret.md
│   ├── wave_音频处理.md
│   └── 手机键盘密码.md
├── Setup
│   ├── Docker_Ubuntu1804.md
│   ├── Library_readin.md
│   ├── Scrips_to_md.md
│   ├── Ubuntu_AWD.md
│   ├── Ubuntu_Docker.md
│   ├── Ubuntu_zsh.md
│   ├── filetree.md
│   └── git_Setup.md
└── Starting.md
```

## Every time before using
> Remember to pull the repo
```shell
git pull MyLibrary master
```

## Using Mkdocs
```shell
mkdocs serve    % create local service, whitch is lively uploading
mkdocs gh-deploy        % build a static page, and upload to github gh-pages branch
```
> Before using `mkdocs ghdeploy` to update gh-pages branch,
> **Remember to fetch** the repo:
```shell
git fetch
```

## Haw to upload
> uploading to Github master
```shell
python3 Scrips_to_md.py
python3 readin.py
python3 filetree.py
git add *
git commit -m 'update'
git push origin master
```

