# thinks-todo-after-install-ubuntu

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
    libdvdread8 p7zip-full unace unzip file-roller atool
```

---

#### Install Gnome Shell

```bash
sudo apt -y install gnome-shell-extensions gnome-shell-extension-prefs \
    gnome-tweaks gconf2 dconf-editor macchanger pavucontrol pulseaudio
```

---

#### Install Favorite Fonts

**Download Lato Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/favorite-fonts/raw/master/lato.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Monaco Monospaced Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/favorite-fonts/raw/master/monaco.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Open Sans Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/favorite-fonts/raw/master/open-sans.zip' \
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

### Required Work/Development Software

#### From Ubuntu Software Repositories

```bash
sudo apt -y install python3-pip git-all jq shutter vlc parole \
    gparted macchanger solaar soundconverter \
    meld smplayer libreoffice filezilla cutecom \
    --fix-missing --fix-broken
```

---

#### From Downloaded DEB Packages

All these packages can be installed by executing the following command

```bash
sudo apt -y install /path/to/package.deb --fix-missing --fix-broken
```

**Recommended Browsers**

- Opera Browser ([`https://www.opera.com`](https://www.opera.com))
- Chromium Browser ([`https://www.chromium.org`](https://www.chromium.org/getting-involved/download-chromium/))
- Chrome Browser ([`https://www.google.com`](https://www.google.com/chrome/))
- Vivaldi Browser ([`https://vivaldi.com`](https://vivaldi.com/))

**Mail Application**

- Mailspring ([`https://getmailspring.com`](https://getmailspring.com))

**Text Editors**

- VS Code ([`https://code.visualstudio.com`](https://code.visualstudio.com))
- VS Codium ([`https://vscodium.com`](https://vscodium.com))

**MySQL**

- Workbench ([`https://www.mysql.com/workbench/`](https://www.mysql.com/products/workbench/))

**Communication**

- Zoom ([`https://zoom.us/download`](https://zoom.us/download))

**Java**

- Java DEB ([`https://www.oracle.com/java`](https://www.oracle.com/java/technologies/downloads/))

    To install it's required to configure `JAVA_HOME` environment variable, add the
    following code to the end of file `/etc/bash.bashrc`.

    ```bash
    # vi /etc/bash.bashrc

    export JAVA_HOME=/path/to/your/java/installation
    export PATH=${PATH}:${JAVA_HOME}/bin
    ```

    Commonly java installation is in the directory

    ```bash
    /usr/lib/jvm/jdk-${YOUR_JAVA_VERSION}
    ```

    Finally just load the updates in your console (_you can reboot your computer for better results_):

    ```bash
    source /etc/bash.bashrc \
    && source ${HOME}/.bashrc
    ```

    Test it

    ```bash
    java --version
    ```

---

#### From Alternative Repositories

* _**SublimeText**_

    Add GPG key

    ```bash
    wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg \
        | gpg --dearmor \
        | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg
    ```

    Add SublimeText source list

    ```bash
    echo "deb https://download.sublimetext.com/ apt/stable/" \
        | sudo tee /etc/apt/sources.list.d/sublime-text.list
    ```

    Install it

    ```bash
    sudo apt-get update \
    && sudo apt-get install sublime-text
    ```


* _**Docker CE**_

    Remove old versions

    ```bash
    sudo apt-get remove docker docker-engine docker.io containerd runc
    ```

    Install Docker dependencies

    ```
    sudo apt-get update \
    && sudo apt-get install ca-certificates curl \
        gnupg lsb-release
    ```

    Add Docker oficial GPG key

    ```bash
    sudo mkdir -p /etc/apt/keyrings \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
        | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

    Setup repository

    ```bash
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
        | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

    Install it

    ```bash
    sudo apt-get update \
    && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

* _**Audio Recorder**_

    Add PPA Repository and install it

    ```bash
    sudo add-apt-repository ppa:audio-recorder/ppa -y \
    && sudo apt update \
    && sudo apt -y install audio-recorder
    ```

---

#### From PIP Repositories

```bash
pip3 install cqlsh ansible yq \
    openshift openstack \
    docker-compose
```

---

#### From Downloaded Binaries

**GoLang**

* Download GoLang from [`https://go.dev/dl/`](https://go.dev/dl/)
* Untar downloaded archive

    ```bash
    tar -xvmf go${YOUR_FAVORITE_GOLANG_VERSION}.linux_amd64.tar.gz
    ```

* Copy to library directory

    ```bash
    sudo mkdir -p /usr/local/lib/golang \
    && sudo mv go /usr/local/lib/golang/go${YOUR_FAVORITE_GOLANG_VERSION}
    ```

* Create link to recommended golang path

    ```
    sudo ln -s /usr/local/lib/golang/go${YOUR_FAVORITE_GOLANG_VERSION} /usr/local/go
    ```

* Create work directory

    ```bash
    mkdir -p ${HOME}/Work/{src,bin}
    ```

* Configure golang environment variables in `/etc/bash.bashrc`

    ```bash
    # vi /etc/bash.bashrc
    export GOROOT=/usr/local/go
    export GOPATH=${HOME}/Work
    export GOBIN=${GOPATH}/bin

    export PATH=${PATH}:${GOROOT}/bin:${GOBIN}
    ```

* Load to your environment (_reboot your computer for better results_)

    ```
    source /etc/bash.bashrc \
    && source ${HOME}/.bashrc
    ```

**Postman**

* Download postman from [`https://www.postman.com/downloads`](https://www.postman.com/downloads)
* Untar downloaded archive

```bash
tar -xvmf postman-${YOUR_FAVORITE_POSTMAN_VERSION}.tar.gz
```

* Copy to OPT directory

```
sudo mv Postman /opt/
```

* Create desktop entry in `/opt/Postman/Postman.desktop`

```bash
# sudo vi /opt/Postman/Postman.desktop
[Desktop Entry]
Name=Postman
Comment=REST API Client
GenericName=API Rest Client
Exec=/opt/Postman/Postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Type=Application
StartupNotify=true
Categories=Utility;Development;IDE;
Keywords=postman;api;rest;
```

* Link to applications to show it in applications menu

```bash
sudo ln -s /opt/Postman/Postman.desktop \
    /usr/share/applications/Postman.desktop
```

**SmartGIT**


**Telegram**


**Eclipse PHP IDE**

---

#### Building From Sources

**NodeJS**

* Download source code from [`https://nodejs.org/en/download/`](https://nodejs.org/en/download/)
* Untar downloaded archive

    ```bash
    tar -xvmf node-${YOUR_FAVORITE_NODEJS_VERSION}.tar.gz
    ```

* Copy to library directory

    ```bash
    sudo mkdir -p /usr/local/lib/nodejs \
    && sudo mv node-${YOUR_FAVORITE_NODEJS_VERSION} /usr/local/lib/nodejs/node-${YOUR_FAVORITE_NODEJS_VERSION}
    ```

* Build and install

    ```bash
    cd /usr/local/lib/nodejs/node-${YOUR_FAVORITE_NODEJS_VERSION} \
    && ./configure \
    && make \
    && make install
    ```
    > _The `make` process will take a lot of time so be patient and drink a coffe_

---

#### Installing with NodeJS

- bower
- yarn
- grunt-cli
- markserv

---

#### Web Development

- Install PHP and Apache2 PPA's
- Install LAMP

---

### Entertainment and Visual Design

#### Video and Image Manipulators

* Pitivi
* gimp
* Inkscape
* obs studio
* cheese
* handBrake+

#### Music and Sound Manipulators

- Audacity
- Audacious
- Banshee

#### Gaming

* Zsnes
* PCSXr
* PCSX2
* MAME
*
