# Required OS Software

## Set ROOT User Password

```bash
sudo passwd root
```

## Before Install Anything Else (only ubuntu)

> _NOTE: This step is only for Ubuntu 22.04, if you try this on ElementaryOS you
> will uncomment the DEB files from CD but you'll not have never the eos CD_

```bash
sudo sed 's/# deb/deb/g' /etc/apt/sources.list -i
```

## Update/Upgrade Pre-Installed Packages

```bash
sudo apt -y update --fix-missing \
&& echo ">>>>>>>>>>>>>>>>>>>>>>>>>>>" \
&& apt list --upgradable \
&& echo ">>>>>>>>>>>>>>>>>>>>>>>>>>>" \
&& sudo apt -y upgrade --fix-missing --fix-broken --allow-downgrades \
&& sudo apt -y autoremove
```

## Install OS Base Software

```bash
sudo apt -y install vim ubuntu-restricted-* build-essential \
    net-tools network-manager lm-sensors nmap curl \
    linux-headers-$(uname -r) software-properties-common \
    gconf2 dconf-editor macchanger pavucontrol pulseaudio \
    libdvdread8 p7zip-full unace unzip file-roller atool rar \
    openssh-server \
    --fix-missing --fix-broken
```

## Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "$(hostname)/$(whoami)"
```

> _NOTE: This command does not require `sudo` because generate a key for the current user_

## Configure PS1 Terminal Prompt Design

On file `${HOME}/.bashrc`

```bash
# generated on https://bashrcgenerator.com/
export PS1="\[\e[00;37m\]\n\[\e[0m\]\[\e[00;33m\][\[\e[0m\]\[\e[00;34m\]\w\[\e[0m\]\[\e[00;33m\]]\[\e[0m\]\[\e[00;37m\]\n\[\e[0m\]\[\e[01;32m\]\u\[\e[0m\]\[\e[01;33m\]@\[\e[0m\]\[\e[01;32m\]\h\[\e[0m\]\[\e[00;34m\]:\[\e[0m\]\[\e[00;31m\]\\$\[\e[0m\]\[\e[00;37m\] \[\e[0m\]"
```

## Install Tweaks

### For Ubuntu

```bash
sudo apt -y install \
    gnome-shell-extensions gnome-shell-extension-prefs gnome-tweaks \
    --fix-missing --fix-broken
```

### For ElementaryOS

```bash
sudo add-apt-repository -y ppa:philip.scott/pantheon-tweaks \
&& sudo apt -y update --fix-msising \
&& sudo apt install pantheon-tweaks \
    --fix-missing --fix-broken
```

## Install Favorite Fonts

### Download Fonts

**Lato Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/lato.zip' \
    --write-out '%{http_code}' --output lato.zip
```

**Monaco Monospaced Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/monaco.zip' \
    --write-out '%{http_code}' --output monaco.zip
```

**Open Sans Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/open-sans.zip' \
    --write-out '%{http_code}' --output open-sans.zip
```

### Decompress and Install it

**Decompres**

```bash
unzip lato.zip -d lato \
&& unzip monaco.zip -d monaco \
&& unzip open-sans.zip -d open-sans
```

**Install**

```bash
sudo mv lato monaco open-sans /usr/share/fonts/truetype/
```
