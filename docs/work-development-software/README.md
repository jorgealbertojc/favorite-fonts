# Work/Development Software

## From Oficial Repositories

```bash
sudo apt -y install python3-pip git-all jq \
    gparted macchanger solaar soundconverter httpie \
    meld filezilla cutecom tree htop terminator \
    --fix-missing --fix-broken
```

## From Downloaded DEB Packages

All these packages can be installed by executing the following command

```bash
sudo apt -y install /path/to/package.deb \
    --fix-missing --fix-broken
```
**Recommended Browsers**

- Opera Browser ([`https://www.opera.com`](https://www.opera.com))
- Chromium Browser ([`https://www.chromium.org`](https://www.chromium.org/getting-involved/download-chromium/))
- Chrome Browser ([`https://www.google.com`](https://www.google.com/chrome/))
- Vivaldi Browser ([`https://vivaldi.com`](https://vivaldi.com/))

**Mail Application**

- Mailspring ([`https://getmailspring.com`](https://getmailspring.com))

**Text/Code Editors**

- VS Code ([`https://code.visualstudio.com`](https://code.visualstudio.com))
- Atom ([`https://atom.io`](https://atom.io))

    > _NOTE: Keep in mind that Atom will be archived on December 15, 2022_

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
    /usr/lib/jvm/jdk-${YOUR_FAVORITE_JAVA_VERSION}
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

## From Alternative PPA Repositories

* _**VS Codium**_

    Add GPG Key

    ```bash
    wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
        | gpg --dearmor \
        | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
    ```

    Add VSCodium source list

    ```bash
    echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
        | sudo tee /etc/apt/sources.list.d/vscodium.list
    ```

    Install it

    ```bash
    sudo apt -y update --fix-missing \
    && sudo apt install codium \
        --fix-missing --fix-broken
    ```

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
    sudo apt -y update --fix-missing \
    && sudo apt install sublime-text
    ```


* _**Docker CE**_

    Remove old versions

    ```bash
    sudo apt remove docker docker-engine docker.io containerd runc
    ```

    Install Docker dependencies

    ```
    sudo apt -y update --fix-missing \
    && sudo apt install ca-certificates curl \
        gnupg lsb-release
    ```

    Add Docker oficial GPG key

    ```bash
    sudo mkdir -p /etc/apt/keyrings \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
        | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

    Setup repository (_ubuntu only_)

    ```bash
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
        | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
    > _NOTE: for ElementaryOS is required to use the ubuntu code name instead of command `lsb_release -cs` or in the contrary a 404 error will shown on `apt update`_

    Install it

    ```bash
    sudo apt -y update --fix-missing \
    && sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

* _**Audio Recorder**_

    Add PPA Repository and install it

    ```bash
    sudo add-apt-repository ppa:audio-recorder/ppa -y \
    && sudo apt -y update --fix-missing \
    && sudo apt -y install audio-recorder \
        --fix-missing --fix-broken
    ```

* _**Brave Browser**_

    Install Brave Browser Dependencies

    ```bash
    sudo apt install apt-transport-https curl \
        --fix-missing --fix-broken
    ```

    Add Brave Browser Official GPG key

    ```bash
    sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg \
        https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
    ```

    Setup Repository

    ```bash
    echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" \
        | sudo tee /etc/apt/sources.list.d/brave-browser-release.list
    ```

    Install it

    ```bash
    sudo apt -y update --fix-missing \
    && sudo apt -y install brave-browser \
        --fix-missing --fix-broken
    ```

## From PIP3 Repositories

```bash
sudo pip3 install cqlsh ansible yq openshift docker-compose \
    openstacksdk python-openstackclient python-novaclient \
    python-neutronclient python-cinderclient \
    python-glanceclient
```

## From Downloaded Binaries

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
    /opt/Telegram/Telegram
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


## Building Stright From Sources

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

## NodeJS Global Dependencies

This dependencies are installed with the `npm` command:

```bash
sudo npm install --location=global \
    bower yarn grunt-cli markserv sass \
    --no-fund --no-audit
```

> _NOTE: `nodejs-v16.16-lts` is used in this installation_

## Web Development Software

> _*NOTE*: For the current developments we need to install `php7.2`_

**Install PPA Repositories**

_Install PHP PPA_

```bash
sudo add-apt-repository ppa:ondrej/php -y
```

_Install Apache2 PPA (<u>only for Ubuntu22.04 in ElementaryOS just install PHP PPA</u>)_

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
    mysql-server \
    --fix-missing --fix-broken
```

_Enable Apache2 Modules_

```bash
sudo a2enmod \
    access_compat actions alias allowmethods auth_basic autoindex \
    buffer cache cgi data dialup dir echo env headers include ldap \
    mime_magic proxy proxy_* request rewrite userdir vhost_alias xml2enc
```

After enabling apache modules is required to configure userdir.conf file, to do
this just update the module configuration with the following contents:

```apache
# sudo vi /etc/apache2/mods-available/userdir.conf
<IfModule mod_userdir.c>
    UserDir Public
    UserDir disabled root

    <Directory /home/*/Public>
        AllowOverride All
        Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
        allow from all
        Require all granted
    </Directory>
</IfModule>
```

Then add the user `www-data` to your own user group with the following command

```bash
sudo adduser www-data $(whoami)
```

Restart apache2 services and your installation will show you following answer:

```bash
sudo systemctl daemon-reload \
&& sudo systemctl reload apache2 \
&& sudo systemctl restart apache2
```

- Check your localhost to answer with status `200`

    ```bash
    curl --location --silent --show-error --request GET --url "http://localhost" \
        --output /dev/null --write-out '%{http_code}\n'
    ```

- Check your userdir to answer with status `200`

    ```bash
    curl --location --silent --show-error --request GET --url "http://localhost/~$(whoami)" \
        --output /dev/null --write-out '%{http_code}\n'
    ```

> _If you get a forbidden response repeat steps to activate modules, restart apache and setup permissions_

**MySQL Usernames and Passwords**

In more recently MySQL server the things works something diferent, now needs the
sudo power to set the MySQL root password, so, just execute the following
command:

```bash
sudo mysqladmin -h 127.0.0.1 -u root password <YOUR_PREFERRED_MYSQL_PASSWORD>
```

**Install Composer Package Manager**

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
        && sudo mv composer.phar /usr/local/lib/composer/composer-${COMPOSER_VERSION}
        ```

        > _NOTE: `COMPOSER_VERSION` is the version obtained in "Get composer version" section_
3. Link to system binaries

    ```bash
    sudo ln -s /usr/local/lib/composer/composer-${COMPOSER_VERSION}/composer.phar \
        /usr/bin/composer
    ```

## Install Ultimate VIM Configuration

1. Download

    ```bash
    git clone --depth=1 https://github.com/amix/vimrc.git ${HOME}/.vim_runtime
    ```

1. Install it

    ```bash
    sh ${HOME}/.vim_runtime/install_awesome_vimrc.sh
    ```

1. Configure Line Numbers

    ```bash
    echo -e "\nset number\n" >> ${HOME}/.vimrc
    ```
1. Install it on root user

    - First switch to root user account

        ```bash
        sudo su -
        ```

    - Download and install ultimate vim configuration

        ```bash
        git clone --depth=1 https://github.com/amix/vimrc.git ${HOME}/.vim_runtime \
        && sh ${HOME}/.vim_runtime/install_awesome_vimrc.sh \
        && echo -e "\nset number\n" >> ${HOME}/.vimrc
        ```
