# Docker_Ubuntu1804
```shell
#!/bin/bash
act()
{
        echo -e "\033[33m$1\033[0m"
        eval $1
}
if [ ! -f "install.sh" ]; then
	act "apt-get update && apt-get upgrade -y && apt install vim -y"
	act "apt install sudo" && echo -e "\033[32msudo\033[0m \033[33mis successfully installed\033[0m" || echo -e "\033[31mfail\033[0m to install \033[35msudo\033[0m"
	act "sudo apt install iputils-ping -y"
	act "sudo apt install net-tools"
	act "sudo apt install wget -y"
	act "sudo apt install python3 -y"
	act "sudo apt install python3-pip -y"
	act "sudo apt install curl -y"
	act "echo \"140.82.112.3 github.com\" >> /etc/hosts"
	act "echo \"199.232.68.133 raw.githubusercontent.com\" >> /etc/hosts"
	echo -e "\033[33m(+)\033[0m \033[32mrunning\033[0m \033[36mUbuntu_zsh.sh\033[0m..."
	bash -c "$(curl -fsSL https://github.com/noneSycamore/script_sh/releases/download/0.2/Ubuntu_zsh.sh)"
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