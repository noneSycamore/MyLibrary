# Ubuntu_AWD
```shell
#!/bin/bash
act()
{
        echo -e "\033[33m$1\033[0m"
        eval $1
}
check(){
    eval $1
}
act "sudo apt-get update"
act "sudo apt install git"
echo -e "\033[33m(+) checking\033[0m for \033[36mdocker\033[0m env..."
act "bash -c \"\$(curl -fsSL https://github.com/noneSycamore/script_sh/releases/download/0.2/Ubuntu_Docker.sh)\""
act "sudo git clone https://github.com/zhl2008/awd-platform.git"
act "sudo cd awd-platform/"
act "sudo docker pull zhl2008/web_14.04"
```