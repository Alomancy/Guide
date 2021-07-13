# Terminal Customisation

## Oh my zsh

[https://github.com/ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)

#### Basic Installation

Oh My Zsh is installed by running one of the following commands in your terminal. You can install this via the command-line with either `curl`, `wget` or another similar tool.

| Method | Command |
| :--- | :--- |
| **curl** | `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |
| **wget** | `sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |
| **fetch** | `sh -c "$(fetch -o - https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |

## Powerlevel 10k

```text
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

[https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

## Install Fonts

### Nerd Fonts

Requirements

```text
sudo atp install bc
sudo apt-get install fontforge;
```

Download Fonts

```text
git clone --depth=1 https://github.com/ryanoasis/nerd-fonts
```

Patch Fonts

```text
cd nerd-fonts/bin/scripts/
./gotta-patch-em-all-font-patcher\!.sh 'Fira'
```

Install Font

```text
cd ../..
./install.sh FiraCode
```

Change Fonts

![](../.gitbook/assets/image%20%2842%29.png)

Test Fonts

```text
for i in {62208..62251}; do printf "\u$(printf %x $i) "; done
```

![](../.gitbook/assets/image%20%2837%29.png)

### Show VPN\_IP

![uncomment vpn\_ip in ~/.p10k.zsh](../.gitbook/assets/image%20%2835%29.png)

![Change vpn\_ip Section](../.gitbook/assets/image%20%2840%29.png)

## Terminal Search

### Fzf

{% embed url="https://github.com/junegunn/fzf" %}

Install FZF

```text
apt install fzf ripgrep
```

add FZF to ~/.zshrc config file

![](../.gitbook/assets/image%20%2836%29.png)

More Plugins

```text
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

## Restart Terminal

Close and reopen, or type:

```text
source ~/.zshrc
```

