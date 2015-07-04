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
