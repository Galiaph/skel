```
# Во FreeBSD можно установить все из пакетов (шрифты нужны только на десктопе):
pkg install py36-powerline-status  powerline-fonts py36-psutil

# В Ubuntu тоже есть пакет...
sudo apt install powerline


# Это нужно на любой из систем:
cd

sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" 
sed -i.bak -E 's/ZSH_THEME="robbyrussell"/#ZSH_THEME="robbyrussell"\nZSH_THEME="dieter"/' ./.zshrc && . ./.zshrc

sed -Ei.bak 's/# DISABLE_AUTO_TITLE="true"/# DISABLE_AUTO_TITLE="true"\nDISABLE_AUTO_TITLE="true"/;s/^plugins=\(git\)/plugins=(git screen tmux)/' ~/.zshrc

# Тема для oh-my-zsh:
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
#You then need to select this theme in your ~/.zshrc:
#ZSH_THEME="powerlevel9k/powerlevel9k"

# Еще одна, только значительно быстрее:
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
#ZSH_THEME="powerlevel10k/powerlevel10k"
#POWERLEVEL9K_DIR_DEFAULT_BACKGROUND="steelblue"
#POWERLEVEL9K_DIR_HOME_BACKGROUND="steelblue"
#POWERLEVEL9K_DIR_HOME_SUBFOLDER_BACKGROUND="steelblue"
#POWERLEVEL9K_DIR_ETC_BACKGROUND="steelblue"
#POWERLEVEL9K_VCS_BACKENDS=(git hg)
#POWERLEVEL9K_DIR_PATH_HIGHLIGHT_BOLD="true"
##POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(context dir vcs)
##POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs history)

# Полезно выключит лессу очистку после выхода:
#LESS="$LESS -X"

# Это нужно только на десктопе с терминалами, на серверах шрифты не нужны!
git clone https://github.com/powerline/fonts.git --depth=1 && cd fonts && ./install.sh

# Для wsl можно переопределить скриндир
mkdir ~/.screen && chmod 700 ~/.screen
echo 'export SCREENDIR=$HOME/.screen' >> ~/.zshrc

# Репа с конфигами:
git clone https://github.com/Galiaph/skel.git
ln -s ~/skel/.screenrc ~/
ln -s ~/skel/.tmux.conf ~/

# zsh completions for cbsd
mkdir ~/.oh-my-zsh/completions
ln -sf /usr/local/cbsd/share/autocompletion/zsh/_cbsd ~/.oh-my-zsh/completions/_cbsd
autoload -U compinit\n
compinit

# Все облегчается, если использовать playbook ansible и antigen
ansible-galaxy install gantsign.oh-my-zsh
ansible-galaxy install gantsign.antigen
ansible-galaxy install gantsign.antigen_bundles
ansible-playbook --ask-pass -b -K --limit="host1,host2" ./skel.yml
```
