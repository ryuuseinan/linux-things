# linux-things

# 20-amdgpu.conf

```
Section "Device"
        Identifier "AMD"
        Driver  "amdgpu"
	Option "DRI" "3" 
        Option "TearFree" "true"
	Option "VariableRefresh" "true"
	Option "AccelMethod" "glamor"
	Option "SwapBuffersWait" "false"
EndSection
```

# yay

```
sudo pacman -S yay base-devel
```

# osu!
+ Video drivers, wine, winetricks
```
sudo pacman -S wine-staging winetricks giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader -y
```
+ For enable ACO
```
sudo nano /etc/environment
RADV_PERFTEST=aco
```
+ Install osu-wine

Download [this](https://drive.google.com/file/d/1iXIhJ20fe97A8xerU2aJGUe73p73V0iQ/view) file, for install:
```
cd Download
yay -U wine-osu-5.14-2-x86_64.pkg.tar.zst
```
+ Creating osu-wine prefix
```
export WINEPREFIX="$HOME/.wine_osu"
export WINEARCH=win32
export PATH=/opt/wine-osu/bin:$PATH
winetricks --force dotnet40 # do not install mono or gecko
winetricks gdiplus
```
+ osu! installation
```
wget https://m1.ppy.sh/r/osu/!install.exe # you can skip this step if you want use an older instalation
wine osu\!install.exe
```
+ Low latency

Copy and paste these files with `sudo` in `/etc/pulse` : [daemon.conf](https://cdn.discordapp.com/attachments/787140086151774248/798790395537784855/daemon.conf), [default.pa](https://cdn.discordapp.com/attachments/787140086151774248/798790398126063636/default.pa), later put `pulseaudio -k` in terminal for restart pulse.

+ osu! Script
```
#!/bin/sh
export WINEPREFIX="$HOME/.wine_osu" 
export PATH=/opt/wine-osu/bin:$PATH 
export STAGING_AUDIO_DURATION=100000 # value will depend of your cpu, lower value is lower latency, I recommend 150000 for a low-end cpu like pentium from 2015
cd /your/osu/directory/xd/
wine osu!.exe "$@"
```
If you cannot execute osu!, try enabling AudioCompatibility in `osu!/osu!.<user>.cfg` and search AudioCompatibility, it will be in 0, change it to 1
```
AudioCompatibility = 1
```

# Refresh rate change (use ```xrandr``` for show proprieties)

```
cvt <horizontal resolution> <vertical resolution> <refresh rate>
xrandr --newmode <copypaste for cvt> 
xrandr --addmode <output video> <resolution_hertz>
xrandr --output <output video> --mode <resolution_hertz>
```
+ 143Hz example
```
cvt 1920 1080 143
xrandr --newmode "1920x1080_143.00"  449.00  1920 2088 2296 2672  1080 1083 1088 1176 -hsync +vsync
xrandr --addmode HDMI-A-0 1920x1080_143.00
xrandr --output HDMI-A-0 --mode 1920x1080_143.00 
```
+ Dual monitors example
```
#!/bin/bash
xrandr --newmode "1920x1080_143.00"  449.00  1920 2088 2296 2672  1080 1083 1088 1176 -hsync +vsync
xrandr --addmode HDMI-A-0 1920x1080_143.00
xrandr --newmode "1024x768_75.00"   82.00  1024 1088 1192 1360  768 771 775 805 -hsync +vsync   
xrandr --addmode DisplayPort-1 1024x768_75.00
xrandr --output HDMI-A-0 --mode 1920x1080_143.00 --right-of DisplayPort-1
xrandr --output DisplayPort-1 --mode 1024x768_75.00
```

# osr2mp4
```
sudo pacman -S python-pip
git clone https://github.com/uyitroa/osr2mp4-app
cd osr2mp4-app
pip install -r requirements.txt
python install.py
python main.py
```
+ Script
```
#!/bin/bash

export PYENV_VERSION=3.6.8
python '/home/<user>/osr2mp4-app/main.py'

# Reset version
unset PYENV_VERSION
```
