<p align="center">
  <a href="https://youtu.be/WXDTsJ4cqO4"><img src="screenshot.png"></a>
</p>

</br>

<div align="center">
  <img height="80px" src="header.png" >
</div>

<h2 align="center">A scriptable scratchpad for developers</h2>
<p align="center">Port of <a href="https://github.com/IvanMathy"><b>@IvanMathy</b></a>'s <a href="https://github.com/IvanMathy/Boop">Boop</a> to GTK</p>

![Continuous integration](https://github.com/zoeyfyi/Boop-GTK/workflows/Continuous%20integration/badge.svg)
![Release](https://github.com/zoeyfyi/Boop-GTK/workflows/Release/badge.svg?branch=release)
[![Crates.io](https://img.shields.io/crates/v/boop-gtk)](https://crates.io/crates/boop-gtk)
[![boop-gtk](https://snapcraft.io//boop-gtk/badge.svg)](https://snapcraft.io/boop-gtk)
[![Flathub](https://img.shields.io/flathub/v/fyi.zoey.Boop-GTK)](https://flathub.org/apps/details/fyi.zoey.Boop-GTK)

### What is Boop-GTK?

[Boop](https://github.com/IvanMathy) is a simple editor that allows you to execute scripts on the buffer. The idea is that you don’t have to paste potentially secret information into shady websites to do some simple transforms, like format json and decoding query strings.

Boop-GTK is a port of Boop to GTK, so users on Linux and Windows can Boop it!

### Features

- 50+ builtin scripts including "Base64 Encode", "Format JSON", "Hex to RGB" and more
- 100% script compatibility with [Boop](https://github.com/IvanMathy/Boop)
- Completely crossplatform!

### Screenshots

| Linux | Windows |
| :---: | :---: |
| ![linux](screenshot.png) | ![windows](windows-screenshot.png) |

There is also a quick demo on [youtube](https://youtu.be/WXDTsJ4cqO4).

### Get Boop-GTK

| Platform | Format | Link |
| -------- | ------ | ---- |
| Linux | Binary | <a href="https://github.com/zoeyfyi/Boop-GTK/releases/latest/download/boop-gtk.linux.amd64">boop-gtk.linux.amd64</a> |
| | Flatpak | <a href="https://github.com/zoeyfyi/Boop-GTK/releases/latest/download/boop-gtk.flatpak">boop-gtk.flatpak</a> |
|  | Snap | <a href="https://github.com/zoeyfyi/Boop-GTK/releases/latest/download/boop-gtk.snap">boop-gtk.snap</a> |
|  | AUR | <a href="https://aur.archlinux.org/packages/boop-gtk/"><code>boop-gtk</code></a> (thanks to qcasey), <a href="https://aur.archlinux.org/packages/boop-gtk-bin/"><code>boop-gtk-bin</code></a> (thanks to hvksmr1996) |
|  | Snap Store | <a href="https://snapcraft.io/boop-gtk"><img src="https://snapcraft.io/static/images/badges/en/snap-store-black.svg" alt="Get it from the Snap Store"></a> |
|  | Flathub | <a href="https://flathub.org/apps/details/fyi.zoey.Boop-GTK"><img width='190' alt='Download on Flathub' src='https://flathub.org/assets/badges/flathub-badge-en.png'></a> |
| Windows | Installer | <a href="https://github.com/zoeyfyi/Boop-GTK/releases/latest/download/boop-gtk.windows.msi">boop-gtk.windows.msi</a> |
| MacOS | Binary | You should really use <a href="https://github.com/IvanMathy/Boop">Boop</a>, but if you <i>really</i> want to: <a href="https://github.com/zoeyfyi/Boop-GTK/releases/latest/download/boop-gtk.macos">boop-gtk.macos</a> |

### Usage

More documentation can be found in [Boop's docs](https://github.com/IvanMathy/Boop/blob/main/Boop/Documentation/Readme.md).

Boop-GTK is easy to use: open it, paste some text, run some scripts, optionally copy the text out.

- [Custom Scripts](https://github.com/IvanMathy/Boop/blob/main/Boop/Documentation/CustomScripts.md)
- [Modules](https://github.com/IvanMathy/Boop/blob/main/Boop/Documentation/Modules.md)
- [Converting Node Modules](https://github.com/IvanMathy/Boop/blob/main/Boop/Documentation/ConvertingNodeModules.md)
- [Global Scripts](docs/GlobalScripts.md) (unique to Boop-GTK)

### Additional Scripts

More scripts can be found in the [Boop repo](https://github.com/IvanMathy/Boop/tree/main/Scripts).

### Building

#### Linux

```shell
sudo apt-get install -y libgtk-3-dev libgtksourceview-3.0-dev
cargo build
```

#### Linux Snap

```shell
sudo apt-get install snap snapcraft
snapcraft snap
sudo snap install boop-gtk_1.5.0_amd64.snap
```

#### Linux Flatpak

```shell
sudo add-apt-repository ppa:alexlarsson/flatpak 
sudo apt-get update 
sudo apt-get install flatpak
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
sudo flatpak install -y flathub org.freedesktop.Platform//20.08 org.freedesktop.Sdk//20.08 org.freedesktop.Sdk.Extension.rust-stable//20.08
wget https://github.com/flatpak/flatpak-builder/releases/download/1.0.10/flatpak-builder-1.0.10.tar.xz && tar -xvf flatpak-builder-1.0.10.tar.xz && cd flatpak-builder-1.0.10 && ./configure --disable-documentation && make && sudo make install
sudo apt-get install python3-toml
bash flatpak/gen-sources.sh
flatpak-builder --repo=repo build-dir flatpak/fyi.zoey.Boop-GTK.json
flatpak build-bundle ./repo boop-gtk.flatpak fyi.zoey.Boop-GTK
```

#### MacOS

```shell
brew install gtk+3 gtksourceview3
cargo build
```

#### Windows

I don't really understand why sourceview isn't picked up automatically by system-deps but [if you are curious](https://github.com/gdesmott/system-deps/issues/10).

```powershell
git clone https://github.com/wingtk/gvsbuild.git C:\gtk-build\github\gvsbuild
cd C:\gtk-build\github\gvsbuild; python .\build.py build -p=x64 --vs-ver=16 --msys-dir=C:\msys64 -k --enable-gi --py-wheel --py-egg gtk3 gdk-pixbuf gtksourceview3
${Env:GTKSOURCEVIEW_3.0_NO_PKG_CONFIG}=1; ${Env:SYSTEM_DEPS_GTKSOURCEVIEW_3.0_LIB}="gtksourceview-3.0"; cargo build
```

#### Windows Installer

```powershell
# follow build steps above, then:
cargo install cargo-wix 
${Env:GTKSOURCEVIEW_3.0_NO_PKG_CONFIG}=1; ${Env:SYSTEM_DEPS_GTKSOURCEVIEW_3.0_LIB}="gtksourceview-3.0"; cargo wix -v
```
