# Table Of Contents
* Broadcasting Livestreams
    * Requirements
    * ffmpeg setup
        * webcam feed
        * local video feed
    * OBS setup
* Watching livestreams

# Broadcasting Livestreams
The Node Media server can take in livestreams in a few different ways,
from the Broadcasting program OBS or the linux command ffmpeg.

The broadcast that is sent to the server can be from the same machine running the
server, in that case the url would be localhost. If the broadcast comes from another
device on the same network it is most likely an ip address. In this documentation
it is simply marked as `YOUR_URL`. The name of the output stream is determined
by the name sent in as input. It is marked as `STREAM_NAME` in this documentation.

for the full documentation of the source please see [Node-Media-Server](https://github.com/illuspas/Node-Media-Server) repo

## Requirements
If you wish to recive broadcasts from outside the machine running you need to make
sure the port `1935` is open, the RTMP protocol uses it.

## ffmpeg setup

### Webcam feed
This has not been tested but should work in theory, please refer to the [ffmpeg documentation](https://www.ffmpeg.org/documentation.html)
for instructions on all flags and options.

```
ffmpeg -i /dev/video0 -framerate 30 -video_size 720x404 -vcodec libx264 -maxrate 768k -bufsize 8080k -vf "format=yuv420p" -g 60 -f flv rtmp://YOUR_URL/live/STREAM_NAME
```
if the above command does not work try the folloing instead:
```
ffmpeg -re -i /dev/video0 -c:v libx264 -preset superfast -tune zerolatency -c:a aac -ar 44100 -f flv rtmp://YOUR_URL/live/STREAM_NAME
```

### Local video file
If your videofile has H.264 video and AAC audio use this command:  
```
ffmpeg -re -i INPUT_FILE_NAME -c copy -f flv rtmp://YOUR_URL/live/STREAM_NAME
```
otherwise use this to convert it at the same time:  
```
ffmpeg -re -i INPUT_FILE_NAME -c:v libx264 -preset superfast -tune zerolatency -c:a aac -ar 44100 -f flv rtmp://YOUR_URL/live/STREAM_NAME
```
## OBS setup
Open the settings menu, locate stream settings.  
set the stream type to Custom Streaming Type  
set the url field to `rtmp://YOUR_URL/live`  
set the stream key to `STREAM_NAME`

# Watching Livestreams
Please note that this documentation is only for the direct access and does not
take the nginx reverse proxy into account. This is due to the fact that the config
might change and your config might not match the example config. Use this as a
reference when setting up the nginx reverse proxy config to your own liking.

### RTMP
`rtmp://YOUR_URL/live/STREAM_NAME`

### http-flv
`http://YOUR_URL:8000/live/STREAM_NAME.flv`

### websocket-flv
`ws://YOUR_URL:8000/live/STREAM_NAME.flv`

### HLS
`http://YOUR_URL:8000/live/STREAM_NAME/index.m3u8`

### DASH
`http://YOUR_URL:8000/live/STREAM_NAME/index.mpd`
