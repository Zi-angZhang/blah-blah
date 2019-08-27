U-net is widely used in image segmentation and super resolution, the upscale and downscale modules serves as image resolution change. higher resolution features maps spatial information and lower-resolution feature maps cares for features. However, the upscale module and downscale are open in real implementation. For instance, some use pixel-shuffle and reverse-pixel-shuffle pairs to compress feature maps and restore images. However. In this implementation, We would compare the following methods:

1. pixel-shuffle and reverse-pixel shuffle
2. strided convolution and strided deconvolution
3. max pooling and reverse max pooling
4. max pooling and strided convolution

