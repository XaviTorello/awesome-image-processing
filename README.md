# Image Processing FLOSS

Just some hints to deal with image processing using Free Libre OpenSource Software



## Stacking

The idea is to achieve one unique image that stacks a set of the same picture over different exposures.

In this example we're going to stack 16 images:

```
convert DSC0133[7-9].ARW DSC0134* DSC0135[0-3].ARW -evaluate-sequence median stack_bracket_16.tif
```
, this will provide the stacked image `stack_bracket_16.tiff` averaging the requested source images.


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
