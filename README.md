# Macbook 9,2 elementary os installation fixes
Some hints how to run elementary os on a macbook pro 9,2 properly.
Be aware that this guide is heavily influenced by my own preferences.

## Install with EFI (rEFInd) support (no grub)
See this document: [https://github.com/aroman/freya-on-a-mac](https://github.com/aroman/freya-on-a-mac)

## Make backlight control work
This is only necessary if elementary os is installed with grub bootloader.
EFI (via rEFInd in my case) seems to make this work out of the box.

`sudo vim /usr/share/X11/xorg.conf.d/20-intel.conf`
Enter the following
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
        BusID       "PCI:0:2:0"EndSection
```

## Get wireless working (but seems to work out of the box with original kernel)
[https://github.com/longsleep/bcmwl-ubuntu](https://github.com/longsleep/bcmwl-ubuntu)

## Fix Apple aluminum keyboard
`sudo vi /etc/modprobe.d/hid_apple.conf`

Add the following lines:

```
options hid_apple fnmode=2
options hid_apple iso_layout=0
```

Then update:
`sudo update-initramfs -u -k all`

## Fix Chrome double blurry icon in plank
Add `StartupWMClass=Google-chrome-stable` to __each sektion__ of `/usr/share/applications/google-chrome.desktop`

## Fix Mad Catz R.A.T 3 Mouse
Create `50-madcatzRat3.conf` in `/usr/share/X11/xorg.conf.d/` with the following content:

```
Section "InputClass"
    Identifier  "Mouse Remap"
    MatchProduct    "Madcatz Mad Catz R.A.T.3 Mouse"
    MatchDevicePath "/dev/input/event*"
    Option      "ButtonMapping" "1 2 3 4 5 0 0 8 9 0 0 0 0 0"
EndSection
```

## Basic PPA's & Apps

```
sudo add-apt-repository -y ppa:inkscape.dev/stable
sudo add-apt-repository -y ppa:otto-kesselgulasch/gimp
sudo add-apt-repository -y ppa:ffmulticonverter/stable
sudo add-apt-repository -y ppa:pmjdebruijn/darktable-release
sudo add-apt-repository -y ppa:ubuntu-mozilla-security/ppa
sudo add-apt-repository -y ppa:videolan/stable-daily
sudo add-apt-repository -y ppa:bit-team/stable
sudo apt-add-repository -y ppa:teejee2008/ppa
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'

sudo apt-get update
sudo apt-get install menulibre gnome-disk-utility mysql-client p7zip-full shutter gimp gpick ffmulticonverter darktable libreoffice libreoffice-l10n-de libreoffice-help-de pidgin filezilla firefox vlc gparted google-chrome-stable htop backintime-gnome dconf-tools timeshift git vim exfat-fuse exfat-utils inkscape

URL='https://atom.io/download/deb'; FILE=`mktemp`; wget "$URL" -qO $FILE && sudo dpkg -i $FILE; rm $FILE
```
