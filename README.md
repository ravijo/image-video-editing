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
* Provide the height and width in pixel `convert input.png -resize 800x600 output.png`
* The above command preserves the aspect ratio. If you want to force the image to become exactly specific size, add exclamation mark like this `convert input.png -resize 800x600! output.png`
* By providing width only and keeping the aspect ratio preserve `convert input.png -resize 800 output.png`
* By providing height only and keeping the aspect ratio preserve `convert input.png -resize x600 output.png`
* By providing percentage such as `convert input.png -resize 50% output.png`

### Crop Image
```console
convert input.jpg -crop 640x620+0+0 output.jpg
```

### Convert PNG to JPG
* Convert `PNG` to `JPG` by specifing the compression level using following command
```console
convert input.png -quality 95 output.jpg
```

### Remove Image Metadata
```console
mogrify -strip *.jpg
```

### Convert HEIC image to JPG
```console
for file in *.HEIC; do heif-convert $file ${file%.HEIC}.jpg; done
```

### Add Text on Image
```console
convert -font helvetica -fill white -pointsize 40 -gravity north -draw "text 0,100 'TEXT TO BE DISPLAYED'" input.jpg output.jpg

convert -font helvetica -undercolor white -fill black -pointsize 40 -gravity northwest -draw "text 0,0 'TEXT TO BE DISPLAYED'" input.jpg output.jpg
```

### Increase Brightness on Image
```console
mogrify -brightness-contrast 10  *.JPG
```

## Video Editing
### Crop
* Command syntax `ffmpeg -i input.mp4 -filter:v "crop=out_w:out_h:x:y" output.mp4`. For example To crop a 80x60 section, starting from position (200, 100) use the following command:
```console
ffmpeg -i input.mp4 -filter:v "crop=80:60:200:100" -c:a copy output.mp4
```

#### Preview
It is better to check the preview before cropping a video. 
```console
ffplay -i input.mp4 -vf "crop=80:60:200:100"

ffmpeg.ffplay -i input.mp4 -vf "crop=80:60:200:100" # only if above command says "ffplay: command not found" 
```

### Cut
```console
ffmpeg -i input.MTS -ss 00:00:03 -to 00:00:16 -c copy output.mp4
ffmpeg -i input.mp4 -ss 00:00:03 -to 00:00:16 -c copy output.mp4
```

### Reduce Size
* By decreasing frame rate 30 frames/sec `ffmpeg -i input.mp4 -r 30 output.mp4`
* By resizing video `ffmpeg -i input.avi -vf scale=1024:-1 output.avi`
* By decreasing video bit rate use a bitrate of 64kb/sec `ffmpeg -i input.mp4 -b:v 64k output.mp4`

### Convert MOV to MP4
```console
ffmpeg -i input.mov -q:v 0 output.mp4
ffmpeg -i input.mov -vcodec h264 -acodec mp2 output.mp4
```

### Remove Audio from Video
```console
ffmpeg -i input.mp4 -c copy -an output.mp4 
```

### Add Text on Video
```console
ffmpeg -i input.mp4 -vf "drawtext=:text='Stack Overflow':fontcolor=white:fontsize=50:box=1:boxcolor=black@0.5:boxborderw=5:x=(w-text_w)/2:y=(h-text_h)/2" -codec:a copy output.mp4
```

## Convert PDF to JPEG
```console
convert -density 600 input.pdf -quality 90 -background white -alpha remove output.jpg
```

## Create EPS from Latex
```console
latex input.tex
dvips -o output.eps input.dvi 
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
* [Mov2Mp4](https://stackoverflow.com/a/12026739)
* [Mov2Mp4](https://mrcoles.com/convert-mov-mp4-ffmpeg/)
* [Remove Audio from Video](https://superuser.com/a/268986)
* [Convert Heic to Jpg](https://ubuntuhandbook.org/index.php/2021/06/open-heic-convert-jpg-png-ubuntu-20-04/)
* [Add Text on Video](https://stackoverflow.com/a/17624103)
* [Add Text on Image](https://stackoverflow.com/a/48966879)
* [Preview Video](https://video.stackexchange.com/a/4571)
* [Increase Brightness on Image](https://www.imagemagick.org/script/command-line-options.php#brightness-contrast)
* [Crop Image](https://superuser.com/a/1163824)
