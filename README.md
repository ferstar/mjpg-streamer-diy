# mjpg-streamer-diy

## Sources:
1. forked from https://svn.code.sf.net/p/mjpg-streamer/code
2. patch from https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=109352
3. usage of `screen` command https://www.ibm.com/developerworks/cn/linux/l-cn-screen/

## Usage:

```
cd mjpg-streamer
make USE_LIBV4L2=true clean all
sudo make DESTDIR=/usr/local install
```

## My way:

The YUV format ate too much memory and cpu time, so I chose MJPEG with `-e` parameter instead.

```
screen -dmS videocap /usr/local/bin/mjpg_streamer \
    -i "/usr/local/lib/input_uvc.so -n -e 4 -f 60 -r 1024x576" \
    -o "/usr/local/lib/output_http.so -w /usr/local/www"
```

the output info looks like this:

```
 i: Using V4L2 device.: /dev/video0
 i: Desired Resolution: 1024 x 576
 i: Frames Per Second.: 60
 i: Format............: MJPEG
 i: Drop Frames Except: 4
 o: www-folder-path...: /usr/local/www/
 o: HTTP TCP port.....: 8080
 o: username:password.: disabled
 o: commands..........: enabled
```

at this capture setting, the bitrate of output mjpg stream is `2000kbps` or above(less than `3000kbps`)

works very well on my rspi2.

> load average: 0.00, 0.01, 0.05

> CPU load: < 2% (1.3±0.3)%

## Addition

You could change the resolution with the parameters after `-r` but use `uvcdynctrl -f` to see which one is build-in

here are my C-270 logitech camera‘s build-in resolution and fps value:

`uvcdynctrl -f` output:

```
Listing available frame formats for device video0:
Pixel format: YUYV (YUV 4:2:2 (YUYV); MIME type: video/x-raw-yuv)
  Frame size: 640x480
    Frame rates: 30, 25, 20, 15, 10, 5
  ...
    ...
  Frame size: 1280x960
    Frame intervals: 2/15, 1/5
Pixel format: MJPG (MJPEG; MIME type: image/jpeg)
  Frame size: 640x480
    Frame rates: 30, 25, 20, 15, 10, 5
  ...
    ...
  Frame size: 1280x960
    Frame rates: 30, 25, 20, 15, 10, 5
```
`lsusb` output:

```
...
Bus 001 Device 006: ID 046d:0825 Logitech, Inc. Webcam C270
...
```

make mjpg-streamer auto start if USB camera is in:
`vi /etc/rc.local` add this before `exit 0`
```
lsusb | grep 046d:0825 > /dev/null
if [ $?==0 ]; then
    screen -dmS videocap /usr/local/bin/mjpg_streamer \
    -i "/usr/local/lib/input_uvc.so -n -e 4 -f 60 -r 1024x576" \
    -o "/usr/local/lib/output_http.so -w /usr/local/www"
fi
```
