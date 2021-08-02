# zsh

```bash
zsh --version

cat /etc/shells

yum -y install zsh		# install zsh

chsh -s /bin/zsh		# change shell to zsh
```

## oh my zsh

https://ohmyz.sh/#install

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# or

sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## Plugins

### autojump

```bash
# Mac
brew install autojump

# Linux
git clone git://github.com/joelthelion/autojump.git
./install.py
```

Add the following code to the end of `~/.zshrc`:

```bash
# brew
[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh
source $ZSH/oh-my-zsh.sh

# git
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
```

Use:

```bash
j $WORKDIR
```

### zsh-autosuggestion

```bash
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

### zsh-syntax-highlighting

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

## Last

Add the following code to  `~/.zshrc`:

```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

```bash
source ~/.zshrc
```