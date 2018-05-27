# Image-Video-Editing
This repository contains commands for beginner level image and video editing in Ubuntu OS.

## Image Editing
### Resizing images
1. Install ImageMagick, if not installed already. Use following command `sudo apt-get install imagemagick`
2. Resizing can be done in following ways-
 1. Provide the height and width in pixel `convert in.png -resize 800×600 out.png`
 2. The above command preserves the aspect ratio. If you want to force the image to become exactly specific size, add exclamation mark like this `convert in.png -resize 800×600! out.png`
 3. By providing width only and keeping the aspect ratio preserve `convert in.png -resize 800 out.png`
 4. By providing height only and keeping the aspect ratio preserve `convert in.png -resize ×600 out.png`
 5. By providing percentage such as `convert in.png -resize 50% out.png`

### Changing image file type
1. Convert png to jpg by specifing the compression level using following command `convert in.png -quality 95 out.jpg`

## Video Editing
### Crop video [src](http://video.stackexchange.com/a/4571)
1. `ffmpeg -i in.mp4 -filter:v "crop=out_w:out_h:x:y" out.mp4` for example To crop a 80×60 section, starting from position (200, 100) `ffmpeg -i in.mp4 -filter:v "crop=80:60:200:100" -c:a copy out.mp4`

### Cut video
1. `ffmpeg -i ~/video/dmp_2.MTS -ss 00:00:03 -to 00:00:16 -c copy dmp_2cut.mp4`
 
### Reduce size
1. By decreasing frame rate [src](http://stackoverflow.com/a/28073732) 30 frames/sec `ffmpeg -i teach1.mp4 -r 30 teach1_out.mp4`
2. By resizing video [src](https://trac.ffmpeg.org/wiki/Scaling%20(resizing)%20with%20ffmpeg) `ffmpeg -i input.avi -vf scale=1024:-1 output.avi`
3. By decreasing bit rate [src](http://unix.stackexchange.com/a/38380) use a bitrate of 64kb/sec `ffmpeg -i input.mp4 -b 64k output.mp4`
