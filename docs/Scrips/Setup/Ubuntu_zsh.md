# Ubuntu_zsh
```shell
#!/bin/bash
act()
{
    echo -e "\033[33m$1\033[0m"
    eval $1
}
ohmyzsh(){
    curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh > install.sh
}
act "sudo apt upgrade -y"
act "sudo apt install git -y"
echo -e "\033[33m(+)\033[0m \033[36mzsh\033[0m install \033[32mstarting...\033[0m"
act "sudo apt install zsh -y" && echo -e "\033[33m(+)\033[0m \033[36mzsh\033[0m install \033[32msuccessful\033[0m"
act "sudo chsh -s /bin/zsh"
echo -e "\033[33m(+)\033[0m \033[36moh-my-zsh\033[0m install & configure \033[32mstarting...\033[0m"
act "apt-get -y install build-essential nghttp2 libnghttp2-dev libssl-dev"
if [ ! -f "install.sh" ]; then
    echo -e "\033[33m(+)\033[0m \033[36moh-my-zsh\033[0m hasn't installed"
    echo -e "\033[33m(+) try to download\033[0m \033[36minstall.sh\033[0m..."
    ohmyzsh
    tmp=$?
    until [ $tmp -eq 0 ]
    do
        echo -e "\033[33m(+)\033[0m \033[31mfail\033[0m to download \033[36minstall.sh\033[0m"
        echo -e "\033[33mretrying...\033[0m"
        ohmyzsh
        tmp=$?
    done
    echo -e "\033[33m(+)\033[0m install.sh for \033[36moh-my-zsh\033[0m download \033[32msucceed\033[0m"
    act "chmod +x install.sh"
    act "rm -rf ~/.oh-my-zsh"
    echo -e "\033[33m(+)\033[0m \033[32mrunning\033[0m \033[36minstall.sh\033[0m..."
    until sh install.sh
    do
        echo -e "\033[33m(+)\033[0m \033[31mfail\033[0m to install \033[36moh-my-zsh\033[0m"
        act "rm -rf ~/.oh-my-zsh"
        echo -e "\033[33mrunning again...\033[0m"
    done
else
    echo -e "\033[33m(+)\033[0m \033[36minstall.sh\033[0m has \033[32malready\033[0m been download"
    act "git clone --depth=1 https://github.com/zsh-users/zsh-completions \${ZSH_CUSTOM:-\${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions"
    act "fpath+=\${ZSH_CUSTOM:-\${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions/src"
    act "git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions.git \${ZSH_CUSTOM:-\${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-autosuggestions"
    act "git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git \${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting"
    act "sed -i '/^plugins=(.*/c plugins=(git zsh-autosuggestions zsh-syntax-highlighting)' ~/.zshrc"
    echo -e "\033[33m(+)\033[0m \033[36moh-my-zsh\033[0m install & configure \033[32msucceed\033[0m"
    echo -e "\033[33m(+)\033[0m \033[36mzsh theme\033[0m \033[35mpowerlevel10k\033[0m install \033[32mstarting...\033[0m"
    act "git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \${ZSH_CUSTOM:-\$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
    act "sed -i '/^ZSH_THEME=.*/c ZSH_THEME=\"powerlevel10k/powerlevel10k\"' ~/.zshrc"
    act "rm install.sh"
    act "exec zsh"
fi
echo -e "\033[33m(+)\033[0m \033[36mzsh\033[0m install & configure \033[32msucceed\033[0m"
exit

```