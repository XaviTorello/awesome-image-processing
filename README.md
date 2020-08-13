# Image Processing FLOSS

Just some hints to deal with image processing using Free Libre OpenSource Software

## Image processing

Image processing can be performed using [`Darktable`](https://github.com/darktable-org/darktable), as a FLOSS alternative to `Adobe Lightroom`.

Another interesting alternative is [`RawTherapee`](https://rawtherapee.com/).

## Image manipulation

Image can be manipulated (also processed) using [`GIMP`](https://github.com/GNOME/gimp) as an alternative to `Adobe Photoshop`.

Some interesting plugins:
- [gimp-plugin-astronomy](https://github.com/gimp-plugins-justice/gimp-plugin-astronomy)
- [gimp-plugin-beautify](https://github.com/hejiann/beautify)
- [gimp-plugin-bimp](https://github.com/alessandrofrancesconi/gimp-plugin-bimp)
- [gimp-plugin-dcamnoise2](https://github.com/pld-linux/gimp-plugin-dcamnoise2)
- [gimp-plugin-pandora](https://shallowsky.com/software/pandora)
- [gimp-plugin-reflection](https://www.gimphelp.org/effects_water-reflection.html)
- [gimp-plugin-resynthesizer](https://github.com/bootchk/resynthesizer)
- [gimp-plugin-refocusit](http://refocus-it.sourceforge.net/)
- [gimp-plugin-saveforweb](https://github.com/auris/gimp-save-for-web)
- [gimp-plugin-separate+](https://osdn.net/projects/separate-plus/)
- [gimp-plugin-wavelet-sharpen](https://github.com/mrossini-ethz/gimp-wavelet-sharpen)

## Stacking

The idea is to achieve one unique image that stacks a set of the same picture over different exposures.

In this example we're going to stack 16 `RAW` files (of course you can use your processed files instead of the raw ones):

```
convert DSC0133[7-9].ARW DSC0134* DSC0135[0-3].ARW -evaluate-sequence median stack_bracket_16.tif
```
, this will provide the stacked image `stack_bracket_16.tiff` averaging the requested source images.


## Panorama

Panos can be created using [`hugin`](https://sourceforge.net/projects/hugin/).

Just start it, load source files and start "composing".

Of course, the same tool can be used for Vertoramas.


## Timelapse

There are some options, but one of the simplest flows is to chain `ffmpeg` and `mencoder`.

In this example we'll use our processed `TIFF` files to create an animation, and 

```
ffmpeg -r 24 -pattern_type glob -i '*.tif'  -s hd1080 -vcodec libx264 timelapse.mp4

mencoder -speed 0.5 -ofps 24 -ovc copy timelapse.mp4 timelapse_slow.mp4
```
, those parameters can be adapted to your needs, in this case we're
- 1) creating the `timelapse.mp4` video at 24fps
- 2) reducing the speed of the final video to increase the length and provide smoother transitions in `timelapse_slow.mp4`
