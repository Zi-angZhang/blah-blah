# Striving for Simplicity: The All Convolutional Net



This paper was published in 2015 in ICLR, I read this paper again to dig some inspiration for my work -- resolution.



How the paper was conducted:

> The pooling layer can be seen as performing a feature-wise convolution in which the activation function is replaced by the _p-norm_. One can therefore ask the question whether and why such special layers need to be introduced into the network. While a complete answer of this question is not easy to give, we assume that in general there exist three possible explanations why pooling can help in CNNs:
>
> 1. the p-norm makes the representation in a CNN more invariant;
> 2. the spatial dimensionality reduction performed by pooling makes covering larger parts of the input in higher layers possible;
> 3. the feature-wise nature of the pooling operation could make optimization easier.
>
> Assuming that only the second part - the dimensionality reduction performed by pooling - is crucial for achieving good performance with CNNs, one can .....

The author find a module, which is pooling, is crucial in CNNs and some assumptions were proposed to explain the effectiveness of the targeted module. One assumption was highly promising, experiments were done.

Two experiment plans were proposed then:

> 1. We can remove each pooling layer and increase the stride of the convolutional layer that preceded it accordingly.
> 2. We can replace the pooling layer by a normal convolution with stride larger than one (i.e. for a pooling layer with k = 3 and  = 2 we replace it with a convolutional layer with corresponding stride and kernel size and number of output channels equal to the number of input channels)

Plans got analyzed.

> The first option has the downside that we significantly reduce the overlap of the convolutional layer
> that preceded the pooling layer. It is equivalent to a pooling operation in which only the top-left
> feature response is considered and can result in less accurate recognition. The second option does
> not suffer from this problem, since all existing convolutional layers stay unchanged, but results in
> an increase of overall network parameters.

Both plans would be adopted in the experiments and discussions. 

__Appendix__:

Pooling layer are rare in super-resolution, reverse-pixels-shuffle and convolution-with-strides are dominant in downsampling, especially in U-Nets.

Here I append some codes of pooling in torch:

``` python
MaxPool2d(kernel_size, stride = kernel_size, padding, dilation, return_indices=False)
MaxUnpool2d(MaxPool2d indices)
```



### Experiments

> ​	In order to quantify the effect of simplifying the model architecture we perform experiments on three datasets: __CIFAR-10, CIFAR-199 and ILSVRC-2012 ImageNet__.

The author choose the most simple  dataset mentioned, i.e. CIFAR-10, to perform an in-depth study of different models, in order to give the demonstration of their concept in a short time. 

> simply removing the max-pooling layer and just increasing the stride of the previous layer results in diminished performance in all settings.

Why not write a paper to compare reverse pixel shuffle, strided convolution, pooling? Interesting and suitable for practice !!!





