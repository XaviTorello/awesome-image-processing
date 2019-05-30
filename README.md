# Image Processing FLOSS

Just some hints to deal with image processing using Free Libre OpenSource Software



## Stacking

The idea is to achieve one unique image that stacks a set of the same picture over different exposures.

In this example we're going to stack 16 images:

```
convert DSC0133[7-9].ARW DSC0134* DSC0135[0-3].ARW -evaluate-sequence median stack_bracket_16.tiff
```
, this will provide the stacked image `stack_bracket_16.tiff` averaging the requested source images.
