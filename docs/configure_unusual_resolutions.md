### How to configure unusual display resolutions in Linux

I have a 4k monitor Phillips Monitor connected to my Macbook. This can be split
into either 2 virtual screens running to 1920x2100 or 4 virtual screens running at 1920x1080

I use Parallels to run a Linux Virtual Machine (Fedora 36). 
How do I get the Virtual Machine to run at a resolution of 1920x2100?

1) Use the cvt command to calculate the settings for xrandr ( width height frequency)
2) Use xrandr to detemrine the current display being used
3) Use xrandr to create the new mode
4) Use xrandr to add the new mode to the current display
5) Use xradnr to switch to the new mode

```
$ /bin/cvt 1920 2100 59.988
# 1920x2100 59.95 Hz (CVT) hsync: 130.40 kHz; pclk: 344.25 MHz
Modeline "1920x2100_59.99"  344.25  1920 2072 2280 2640  2100 2103 2113 2175 -hsync +vsync

$ /bin/xrandr
Screen 0: minimum 320 x 200, current 1920 x 2100, maximum 8192 x 8192
Virtual-1 connected primary 1920x2100+0+0 (normal left inverted right x axis y axis) 0mm x 0mm
   1024x768      59.95 +  60.00  
   4096x2160     60.00    59.94  
   2560x1600     59.99    59.97  
...
Virtual-2 disconnected (normal left inverted right x axis y axis)
...

$ /bin/xrandr --newmode "1920x2100" 344.25  1920 2072 2280 2640  2100 2103 2113 2175 -hsync +vsync
$ /bin/xrandr --addmode Virtual-1 1920x2100
$ /bin/xrandr --output Virtual-1 --mode 1920x2100

```