# Convolutional neural Networks for Direct Text Debluring

Text is a type of highly structured data, I hope reading this paper can help me to further combine structure representation and texture representation together.

[the paper](http://www.bmva.org/bmvc/2015/papers/paper006/paper006.pdf)

_Surprisingly, this paper also demonstrated the performance of the convolutional networks on a large set of text documents and on a combination of realistic __de-focus and camera shake blur kernels__ ._



## hight lights

the process of camera capturing images can't be seen as a simple linear convolution task because 

- the image can be saturated
- the camera apply color and gamma correction
- colors are interpolated from neighbor pixels due to Bayer maxk.



__analysis of research object: text__

Images of text are markedly different from images of natural scenes.



__Convolutional networks for blind deconvolution__

