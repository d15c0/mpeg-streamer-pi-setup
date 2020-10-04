mjpeg-streamer:
Another streaming software that I tried was mjpeg-streamer, which is not as features complete as motion, but it is perfect if you just need a video stream. It also provides a web interface to display the stream. I couldn't find a binary version of mjpeg-streamer for arm processor, so I had to compile it myself as follows.

First off we need mjpg-streamer source code from > here < and save it in your folder of choice. I usually save and extract the source packages under /usr/local/src.
Position yourself whichever folder the archive has been saved into, and extract the archive with the command:

```tar xvzf mjpg-streamer-r63.tar.gz```

In order to compile mjpg-streamer, we need the libjpeg8-dev libraries, so let's install them first:

```apt-get install libjpeg8-dev```

I also needed to create a symbolic link of one header file which, to me, resulted missing:

```ln -s /usr/include/linux/videodev2.h /usr/include/linux/videodev.h```

Now everything should be set to proceed with the compilation process. Switch to mjpg-streamer newly created folder and compile it with:

```cd mjpg-streamer-r63```
```CFLAGS+="-O2 -march=armv6 -mfpu=vfp -mfloat-abi=hard" make```

And that's it. To run mpjg-streamer type the following command:

```export LD_LIBRARY_PATH=.```
```./mjpg_streamer -i './input_uvc.so -d /dev/video0 -r 640x480 -f 15' -o './output_http.so -w ./www -p 8080'```

switches:
```-i:``` configure the input section
```-d:``` device selection, in case of multiple webcams
`-r:` frame resolution width*height
`-f:` frame per seconds
`-o:` configure the output section
`-w:` website folder
`-p:` port

It's now possible to get access to the web interface at the address:

`http://RPI-IP:8080`

