# Things ToDo After Install Ubuntu

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
    --url 'https://github.com/jorgealbertojc/thinks-todo-after-install-ubuntu/raw/master/fonts/lato.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Monaco Monospaced Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/thinks-todo-after-install-ubuntu/raw/master/fonts/monaco.zip' \
    --output lato.zip --write-out '%{http_code}'
```

**Download Open Sans Font**

```bash
curl --location --show-error --silent --request GET \
    --url 'https://github.com/jorgealbertojc/thinks-todo-after-install-ubuntu/raw/master/fonts/open-sans.zip' \
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
sudo apt -y install python3-pip git-all jq \
    gparted macchanger solaar soundconverter httpie \
    meld filezilla cutecom tree htpop \
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

* Download smartgit from [`https://www.syntevo.com/smartgit/download/`](https://www.syntevo.com/smartgit/download/)
* Untar downloaded archive

    ```bash
    tar -xvmf smartgit-linux-${YOUR_FAVORITE_SMARTGIT_VERSION}.tar.gz
    ```

* Copy to OPT directory

    ```bash
    sudo mv smartgit /opt/
    ```

* Install using smartgit installation scripts

    ```bash
    cd /opt/smartgit/bin \
    && sudo ./add-menuitem.sh
    ```

**Telegram**

* Download from [`https://telegram.org/apps`](https://telegram.org/apps)
* Untar downloaded archive

    ```bash
    tar -xvmf tsetup.${YOUR_FAVORITE_TELEGRAM_VERSION}.tar.gz
    ```

* Copy to IPT directory

    ```bash
    sudo mv Telegram /opt/
    ```

* Run with terminal to install it

    ```bash
    /opt/telegram/Telegram
    ```

    After that a initial window will shown on your screen, just close it and the
    installation has finished, you can now find telegram desktop on the applications
    menu.

**Eclipse PHP IDE**

The Eclipse PHP IDE installation is similar to Postman instructions above.

* Download Eclipse PHP IDE from [`https://www.eclipse.org/downloads/packages`](https://www.eclipse.org/downloads/packages)
* Find the Eclipse IDE for PHP Developers and Download it
* Untar downloaded file

    ```bash
    tar -xvmf eclipse-php-${YOUR_FAVORITE_ECLIPSE_VERSION}.tar.gz
    ```

* Copy to OPT directory

    ```bash
    sudo mv eclipse /opt/eclipse-php
    ```

* Create desktop entry in `/opt/eclipse-php/eclipse-php.desktop`

    ```bash
    # sudo vi /opt/eclipse-php/eclipse-php.desktop
    [Desktop Entry]
    Name=Eclipse IDE for PHP Developers
    Comment=Eclipse IDE for PHP Developers
    GenericName=Eclipse
    Exec=/opt/eclipse-php/eclipse
    Icon=/opt/eclipse-php/icon.xpm
    Type=Application
    StartupNotify=true
    Categories=Utility;Development;IDE;Eclipse;
    Keywords=eclipse;ide;development;
    ```

* Link to applications to show it in applications menu

    ```bash
    sudo ln -s /opt/eclipse-php/eclipse-php.desktop \
        /usr/share/applications/eclipse-php.desktop
    ```

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
    && sudo ./configure \
    && sudo make \
    && sudo make install
    ```
    > _The `make` process will take a lot of time so be patient and drink a coffe_

**Bashtop**

* Download source code from [`https://github.com/aristocratos/bashtop`](https://github.com/aristocratos/bashtop)

```bash
git clone https://github.com/aristocratos/bashtop.git
```

* Copy to library directory

```bash
sudo mv bashtop /usr/local/lib/
```

* Install

```bash
cd /usr/local/lib/bashtop \
&& sudo make install
```

---

#### Installing NodeJS Global Dependencies

This dependencies are installed with the `npm` command:

```bash
sudo npm install -g \
    bower yarn grunt-cli markserv
```

---

#### Web Development

> _*NOTE*: For the current developments we need to install `php7.2`_

**Install PPA Repositories**

Install PHP PPA

```bash
sudo add-apt-repository ppa:ondrej/php -y
```

Install Apache2 PPA

```bash
sudo add-apt-repository ppa:ondrej/apache2 -y
```

**Install PHP + Apache + MySQL**

```bash
sudo apt -y update --fix-missing \
&& sudo apt -y install \
    apache2 libapache2-mod-php7.2 \
        php7.2 php7.2-cgi php7.2-cli php7.2-curl php7.2-common php7.2-dev \
        php7.2-fpm php7.2-gd php7.2-geoip php7.2-gnupg php7.2-grpc \
        php7.2-imagick php7.2-imap php7.2-json php7.2-ldap \
        php7.2-mbstring php7.2-mcrypt php7.2-memcache php7.2-mysql php7.2-oauth \
        php7.2-pgsql php7.2-smbclient php7.2-sqlite3 php7.2-tidy \
        php7.2-uploadprogress php7.2-uuid php7.2-xdebug php7.2-xml \
        php7.2-xmlrpc php7.2-xsl php7.2-yaml php7.2-zip \
    mysql-server
```

**Setup MySQL Username and Password**

In more recently MySQL server the things works something diferent, now needs the
sudo power to set the MySQL root password, so, just execute the following
command:

```bash
sudo mysqladmin -u root -h host_name password "${MYSQL_SERVER_PASSWORD}"
```

**Install Composer**

To install composer just need to use the following commands

> _NOTE: We recommend to continuously check for composer updates at [`https://getcomposer.org`](https://getcomposer.org)_

1. Download and compile

    ```bash
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    ```

    After that you will have a file ready to be installed in `$(pwd)/composer.phar`

2. Move to library directory

    - _Get composer version_

        To get the composer version you will install just execute the following line

        ```bash
        ./composer.phar --version
        ```

    - _Move file to library_

        ```bash
        sudo mkdir /usr/local/lib/composer/composer-${COMPOSER_VERSION} \
        && mv composer.phar /usr/local/lib/composer/composer-${COMPOSER_VERSION}
        ```

        > _NOTE: `COMPOSER_VERSION` is the version obtained in "Get composer version" section_

3. Link to system binaries

    ```bash
    ln -s /usr/local/lib/composer/composer-${COMPOSER_VERSION}/composer.phar \
        /usr/bin/composer
    ```

**Test it**
After all above steps the server has started working, to test just send the
following request:

```
curl --location --silent --show-error \
    --request GET \
    --url 'http://localhost'
```

or

```
http --follow 'http://localhost'
```

---

### Entertainment and Visual Design

#### Video and Image Manipulators

```
sudo apt -y install \
    pitivi gimp inkscape obs-studio cheese
    handbrake vlc parole shutter \
    --fix-missing --fix-broken
```

---

#### Music and Sound Manipulators

```bash
sudo apt -y install \
    audacity audacious banshee \
    --fix-missing --fix-broken
```

---

#### Gaming

```bash
sudo apt -y install \
    zsnes pcsxr pcsx2 mame \
    --fix-missing --fix-broken
```

> _NOTE: The BIOS will be uploaded in this repository in a future commit_

---

####  Office Suite

```bash
sudo apt -y install libreoffice texlive-full \
    --fix-missing --fix-broken
```

## Done

That's all folks :D
