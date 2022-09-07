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
│   │   ├── Decrypt_Chaos
│   │   │   ├── chaos.md
│   │   │   └── exp.md
│   │   └── Random_predict
│   │       ├── exp.md
│   │       ├── msg.txt
│   │       └── task.md
│   └── Misc
│       └── Chaotic_pic
│           ├── exp.md
│           ├── prepare
│           │   ├── desktop.ini
│           │   ├── make1
│           │   │   ├── LSB隐写.md
│           │   │   ├── flag.txt
│           │   │   ├── origin.png
│           │   │   └── with_flag.png
│           │   ├── make2
│           │   │   ├── chaos.md
│           │   │   ├── flag_encrypt.png
│           │   │   └── with_flag.png
│           │   └── make3
│           │       ├── LSB2.png
│           │       ├── LSB隐写.md
│           │       ├── flag_encrypt.png
│           │       ├── lsb_clear.md
│           │       ├── pic.txt
│           │       ├── read16.md
│           │       └── zaiti.png
│           ├── solve
│           │   ├── 1.png
│           │   ├── 2.png
│           │   ├── exp.md
│           │   └── task.png
│           └── task.png
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
│   ├── git_Setup.md
│   └── vimrc.md
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

