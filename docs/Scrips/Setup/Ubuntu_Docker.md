# Ubuntu_Docker
```shell
#!/bin/bash
check(){
    eval $1
}
act()
{
        echo -e "\033[33m$1\033[0m"
        eval $1
}
act "check \"docker -v\""
tmp=$?
if [ $tmp -eq 0 ];then
    echo -e "\033[33m(+)\033[0m \033[36mDocker\033[0m has \033[32malready\033[0m been installed"
    exit
fi
echo -e "\033[33m(+)\033[0m \033[36mDocker\033[0m is \033[31mnot\033[0m installed"
echo -e "\033[33m(+) continuing\033[0m..."
act "sudo apt update -y"
act "sudo apt install apt-transport-https ca-certificates curl software-properties-common"
act "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -"
act "sudo add-apt-repository \"deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable\""
act "sudo apt update"
act "sudo apt-cache policy docker-ce"
act "sudo apt install docker-ce -y"
echo -e "\033[33m" && docker -v && echo -e "\033[0m"
act "check \"sudo systemctl start docker\"" 
tmp=$?
if [ $tmp -eq 0 ];then
    echo -e "\033[33m(+) using\033[0m \033[36msystemctl\033[0m..."
    act "sudo systemctl enable docker"
    act "sudo systemctl status docker"
else
	echo -e "\033[33m(+) using\033[0m \033[36mservice\033[0m..."
    act "service docker start"
    act "sudo systemctl enable docker"
    act "service docker status"
fi
```