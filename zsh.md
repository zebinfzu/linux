# 配置高效zsh(不要oh-my-zsh)

## 给机器安装nerd字体

[官方链接](https://www.nerdfonts.com/font-downloads) 下载想要的字体安装的本机，终端选择该字体

## 下载zsh以及安装插件

```sh
apt-get install zsh
sudo apt-get install zsh-autosuggestions zsh-syntax-highlighting
# 添加到.zshrc
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# 主题插件
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/.powerlevel10k
echo 'source ~/.powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

