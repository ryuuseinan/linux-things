# linux-things

# Refresh rate change

```
cvt 1920 1080 143
xrandr --newmode "1920x1080_143.00"  449.00  1920 2088 2296 2672  1080 1083 1088 1176 -hsync +vsync
xrandr --addmode HDMI-A-0 1920x1080_143.00
xrandr -r 143
```
+ Dual monitors
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
