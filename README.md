# Image and Video Editing
This repository contains commands for beginner level image and video editing in Ubuntu OS.

# Tools Required
1. [ImageMagick](https://www.imagemagick.org/)
1. [ffmpeg](https://www.ffmpeg.org/)

## Install ImageMagick on Ubuntu 14.04
1. Open the terminal or press <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd>
1. Run following command `sudo apt-get install imagemagick`

## Install FFmpeg on Ubuntu 14.04
1. Use PPA. Open the terminal or press <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd>
1. Run following commands-
    ```console
    sudo add-apt-repository ppa:mc3man/trusty-media
    sudo apt-get update
    sudo apt-get install ffmpeg gstreamer0.10-ffmpeg
    ```

## Image Editing
### Resizing
Resizing can be done in following ways-
* Provide the height and width in pixel `convert in.png -resize 800×600 out.png`
* The above command preserves the aspect ratio. If you want to force the image to become exactly specific size, add exclamation mark like this `convert in.png -resize 800×600! out.png`
* By providing width only and keeping the aspect ratio preserve `convert in.png -resize 800 out.png`
* By providing height only and keeping the aspect ratio preserve `convert in.png -resize ×600 out.png`
* By providing percentage such as `convert in.png -resize 50% out.png`

### Changing File Type
* Convert `png` to `jpg` by specifing the compression level using following command `convert in.png -quality 95 out.jpg`

## Video Editing
### Crop
* Command syntax `ffmpeg -i in.mp4 -filter:v "crop=out_w:out_h:x:y" out.mp4` for example To crop a 80×60 section, starting from position (200, 100) `ffmpeg -i in.mp4 -filter:v "crop=80:60:200:100" -c:a copy out.mp4`

### Cut
* `ffmpeg -i ~/video/dmp_2.MTS -ss 00:00:03 -to 00:00:16 -c copy dmp_2cut.mp4`

### Reduce Size
* By decreasing frame rate 30 frames/sec `ffmpeg -i teach1.mp4 -r 30 teach1_out.mp4`
* By resizing video `ffmpeg -i input.avi -vf scale=1024:-1 output.avi`
* By decreasing video bit rate use a bitrate of 64kb/sec `ffmpeg -i input.mp4 -b:v 64k output.mp4`

## Covert PDF to JPEG (high quality)
```console
convert -density 600 page.pdf -quality 90 -background white -alpha remove page.jpg
```

## Create EPS from Latex
```console
latex main.tex
dvips -o main.eps main.dvi 
```

## Gif from Video
* Normal mode:
    ```console
    ffmpeg -i input.mp4 output.gif
    ```
* Advance mode:
    ```console
    ffmpeg -y -i input.mp4 -vf palettegen palette.png
    ffmpeg -y -i input.mp4 -i palette.png -filter_complex paletteuse -r 10 -s 320x480 output.gif
    ```

### Reduce Gif Size
```console
mogrify -layers 'optimize' -fuzz 7% file.gif
```

## References
The above information is taken from various sources such as following-
* [Video Stackexchange](http://video.stackexchange.com/a/4571)
* [Unix Stackexchange](http://unix.stackexchange.com/a/38380)
* [Stackoverflow](http://stackoverflow.com/a/28073732)
* [FFmpeg](https://trac.ffmpeg.org/wiki/Scaling%20(resizing)%20with%20ffmpeg)
* [Reduce Gif Size](https://stackoverflow.com/a/47343340)
* [FFmpeg with Palette](https://superuser.com/a/1049820)
 
