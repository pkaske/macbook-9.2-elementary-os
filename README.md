# Macbook 9,2 elementary os installation fixes
Some hints how to run elementary os on a macbook pro 9,2 properly

## Make backlight control work
`sudo vim /usr/share/X11/xorg.conf.d/20-intel.conf`
Enter the following
```
Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
        BusID       "PCI:0:2:0"EndSection
```

## Get wireless working after kernel update
[https://github.com/longsleep/bcmwl-ubuntu](https://github.com/longsleep/bcmwl-ubuntu)

## Basic PPA's & Apps

```
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
sudo apt-get install menulibre gnome-disk-utility mysql-client p7zip-full shutter gimp gpick ffmulticonverter darktable libreoffice libreoffice-l10n-de libreoffice-help-de pidgin filezilla firefox vlc gparted google-chrome-stable htop backintime-gnome dconf timeshift 

URL='https://atom.io/download/deb'; FILE=`mktemp`; wget "$URL" -qO $FILE && sudo dpkg -i $FILE; rm $FILE
```
