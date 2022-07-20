### Required OS Software

#### Before you install anything:

First of all, update `sources.list` with the following command:

```bash
sudo sed 's/# deb/deb/g' /etc/apt/sources.list -i
```

The command above will update `sources.list` file to activate `deb-src` repositories

---

#### Then update/upgrade pre-installed packages

After `sources.list` update, just install the pre-installed packages updates.

```bash
sudo apt -y update --fix-missing \
&& echo ">>>>>>>>>>>>>>>>>>>>>>>>>>>" \
&& apt list --upgradable \
&& echo ">>>>>>>>>>>>>>>>>>>>>>>>>>>" \
&& sudo apt -y upgrade --fix-missing --fix-broken --allow-downgrades \
&& sudo apt -y autoremove
```

---

#### Set Root Password

```bash
sudo passwd root
```

---

#### Install OS Requirements

This will install `make`, `gcc`, `g++` and other required software to compile and build binaries/packages

```bash
sudo apt -y install vim ubuntu-restricted-* build-essential \
    net-tools network-manager \
    linux-headers-$(uname -r) \
    gconf2 dconf-editor macchanger pavucontrol pulseaudio \
    libdvdread8 p7zip-full unace unzip file-roller atool
```

---

#### Install Gnome Shell Extensions and Tweaks

```bash
sudo apt -y install gnome-shell-extensions gnome-shell-extension-prefs gnome-tweaks
```

---

#### Install Favorite Fonts

**Download Lato Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/lato.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Monaco Monospaced Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/monaco.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Open Sans Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/fonts/open-sans.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Decompress ZIP Files**

```bash
unzip lato.zip -d lato \
&& unzip monaco.zip -d monaco \
&& unzip open-sans.zip -d open-sans
```

**Install Favorite Fonts**

```bash
sudo cp -rv lato monaco open-sans /usr/share/fonts/truetype/
```
