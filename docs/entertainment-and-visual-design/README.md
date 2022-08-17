# Entertainment and Visual Design

## Install Video and Image Manipulators and Viewers

```bash
sudo apt -y install \
    pitivi gimp inkscape obs-studio cheese \
    handbrake vlc parole shutter smplayer \
    --fix-missing --fix-broken
```

## Install Music and Sound Manipulators

```bash
sudo apt -y install \
    audacity audacious \
    --fix-missing --fix-broken
```

## Install Gaming Emulators and Players

```bash
sudo apt -y install \
    zsnes pcsxr pcsx2 mame \
    --fix-missing --fix-broken
```
> _NOTE: package `zsnes` and `pcsx2` does not exists in ElementaryOS_

_Download BIOS files_

```bash
curl --location --show-error --silent --request GET \
    --url https://github.com/jorgealbertojc/things-todo-after-install-ubuntu/raw/master/binaries/games-bios-v1.0.1.rar \
    --output ${HOME}/Downloads/games-bios-v1.0.1.rar
```

_Install BIOS files by Emulator_

- **`zsnes`**

    Does not requires any bios file

- **`pcsxr`**

    Commonly requires BIOS file in the directory:

    ```bash
    ${HOME}/.pcsxr/bios
    ```

- **`pcsx2`**

    Commonly requires BIOS file in the directory:

    ```bash
    ${HOME}/.config/PCSX2/bios
    ```

- **`mame`**

    Requires BIOS file in the same games dierctory, standard directory is:

    ```bash
    ${HOME}/.mame/roms
    ```

> BIOS files stored in this repository are for review only you need to remove
> from your system after review it.


## Install Office Suite

```bash
sudo apt -y install texlive-full texlive-xetex \
    libreoffice libreoffice-l10n-es texmaker \
    --fix-missing --fix-broken
```
