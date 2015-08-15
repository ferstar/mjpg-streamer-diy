# mjpg-streamer-diy

## Sources:
1. forked from https://svn.code.sf.net/p/mjpg-streamer/code
2. patch from https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=109352

## Usage:

```
cd mjpg-streamer
make USE_LIBV4L2=true clean all
sudo make DESTDIR=/usr/local install
```

## My way:

`vi /usr/local/bin/streamer.sh`

```
#!/bin/bash
screen -dm /usr/local/bin/mjpg_streamer -i "/usr/local/lib/input_uvc.so -n -e 3 -f 30 -r 800x448" -o "/usr/local/lib/output_http.so -w /usr/local/www"
```

`chmod +x /usr/local/bin/streamer.sh` and run

the output info looks like this:

```
 i: Using V4L2 device.: /dev/video0
 i: Desired Resolution: 800 x 448
 i: Frames Per Second.: 30
 i: Format............: MJPEG
 i: Drop Frames Except: 3
 o: www-folder-path...: /usr/local/www/
 o: HTTP TCP port.....: 8080
 o: username:password.: disabled
 o: commands..........: enabled
```

## Addition

You could change the resolution with the parameters after `-r` but use `uvcdynctrl -f` to see which one is build-in

## C-270 logitech camera

`uvcdynctrl -f` output:

```
Listing available frame formats for device video0:
Pixel format: YUYV (YUV 4:2:2 (YUYV); MIME type: video/x-raw-yuv)
  Frame size: 640x480
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 160x120
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 176x144
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 320x176
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 320x240
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 352x288
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 432x240
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 544x288
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 640x360
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 752x416
    Frame rates: 25, 20, 15, 10, 5
  Frame size: 800x448
    Frame rates: 20, 15, 10, 5
  Frame size: 800x600
    Frame rates: 20, 15, 10, 5
  Frame size: 864x480
    Frame rates: 20, 15, 10, 5
  Frame size: 960x544
    Frame rates: 15, 10, 5
  Frame size: 960x720
    Frame rates: 10, 5
  Frame size: 1024x576
    Frame rates: 10, 5
  Frame size: 1184x656
    Frame rates: 10, 5
  Frame size: 1280x720
    Frame intervals: 2/15, 1/5
  Frame size: 1280x960
    Frame intervals: 2/15, 1/5
Pixel format: MJPG (MJPEG; MIME type: image/jpeg)
  Frame size: 640x480
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 160x120
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 176x144
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 320x176
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 320x240
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 352x288
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 432x240
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 544x288
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 640x360
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 752x416
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 800x448
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 800x600
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 864x480
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 960x544
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 960x720
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 1024x576
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 1184x656
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 1280x720
    Frame rates: 30, 25, 20, 15, 10, 5
  Frame size: 1280x960
    Frame rates: 30, 25, 20, 15, 10, 5
```
