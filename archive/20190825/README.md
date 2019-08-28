# Denoising and super resolution in one-shot

This post consists the following parts:

1. review of novel denoising papers
2. the combination of denoising and super resolution



## Introduction

I found [this repo](https://github.com/titu1994/Image-Super-Resolution) consists two implementation of denoising an image as well as super resolution:

> __Denoising (Auto Encoder) Super Resolution CNN__
>
> This model uses bridge connections between the convolutional layers of the same level in order to speed up convergence and improve output results. The bridges are averaged to be more robust.



About the reason why "denoising", the author stats:

> Since the training images are passed through a Gaussian filter (sigma = 0.5), then downscaled to 1/3 the size, then upscaled to the original `33x33` size images. the images can be considered noisy. 

So basically, this implementations just referred the ideology of the denoising encoder.

![img](https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/architectures/Denoise.png)

__DCGANs__ seems a better idea for all-in-one implementation that solves _super resolution, deblurring and denosing._

the paper is available at [here](http://stanford.edu/class/ee367/Winter2017/yan_wang_ee367_win17_report.pdf)



