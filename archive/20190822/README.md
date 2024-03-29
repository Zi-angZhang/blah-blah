# Convolution is just pattern matching?

Convolution is the base technique of Convolutional Neural Networks and it settles in the central position of image processing technologies. But I am thinking of the real work done by convolution and I would dive into the mechanisms trying to understand convolution.

![img](https://developer.nvidia.com/sites/default/files/pictures/2018/convolution-1.png)

Image Source :[nvidia](https://developer.nvidia.com/discover/convolution)
$$
y(t) = f \circledast x = \int^\infin_{-\infin} f(k) \cdot x(t-k)\ dk
$$
where $\circledast$ stands for convolution operation.

Sad! GitHub doesn't support MathJax in rendering equation. I just leave the wrack above and not prepared to do any workaround with it. Following posts would contain no equation, which sounds cheerful for one who hate math LOL.



###  What do nvidia interpretation of Convolution?

According to their [understanding](https://developer.nvidia.com/discover/convolution), convolution describes the __diffusion__ of information i.e. pixels diffuse towards contours in an image.

> In quantum mechanics, it describes the probability of a quantum particle being in a certain place when you measure the particle’s position (average probability for a pixel’s position is highest at contours). In probability theory, it describes cross-correlation, which is the amount of overlap or degree of similarity for two sequences (similarity high if the pixels of a feature (e.g. nose) overlap in an image (e.g. face)). In statistics, it describes a weighted moving average over a normalized sequence of input (large weights for contours, small weights for everything else). 

## Convolution layer in CNNs

Sure I am familiar with convolution layers, especially its form in PyTorch. I would simply some graphs and codes for a personal hint.... I have a poor memory, leaks and overwritten happens everywhere in my head, reboot, the most powerful tool of a computer engineer, does not apply to my brain.... Look, I am blahing....



### [Convolution arithmetic animate](https://github.com/vdumoulin/conv_arithmetic)

Here I just refer some nice drawing by [vdumoulin](https://github.com/vdumoulin), the original repository is hyperlinked as the above subtitle.


##### Convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._

<table style="width:100%; table-layout:fixed;">
  <tr>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/no_padding_no_strides.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/arbitrary_padding_no_strides.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/same_padding_no_strides.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/full_padding_no_strides.gif"></td>
  </tr>
  <tr>
    <td>No padding, no strides</td>
    <td>Arbitrary padding, no strides</td>
    <td>Half padding, no strides</td>
    <td>Full padding, no strides</td>
  </tr>
  <tr>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/no_padding_strides.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/padding_strides.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/padding_strides_odd.gif"></td>
    <td></td>
  </tr>
  <tr>
    <td>No padding, strides</td>
    <td>Padding, strides</td>
    <td>Padding, strides (odd)</td>
    <td></td>
  </tr>
</table>

##### Transposed convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._

<table style="width:100%; table-layout:fixed;">
  <tr>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/no_padding_no_strides_transposed.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/arbitrary_padding_no_strides_transposed.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/same_padding_no_strides_transposed.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/full_padding_no_strides_transposed.gif"></td>
  </tr>
  <tr>
    <td>No padding, no strides, transposed</td>
    <td>Arbitrary padding, no strides, transposed</td>
    <td>Half padding, no strides, transposed</td>
    <td>Full padding, no strides, transposed</td>
  </tr>
  <tr>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/no_padding_strides_transposed.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/padding_strides_transposed.gif"></td>
    <td><img width="150px" src="https://github.com/vdumoulin/conv_arithmetic/raw/master/gif/padding_strides_odd_transposed.gif"></td>
    <td></td>
  </tr>
  <tr>
    <td>No padding, strides, transposed</td>
    <td>Padding, strides, transposed</td>
    <td>Padding, strides, transposed (odd)</td>
    <td></td>
  </tr>
</table>

### Convolution Layer Math

This part is inspiring, years of making friend with computer taught me one thing: logic and device are related but completely different. When we are curious about how the algorithms are implemented, we have to read the source code, sadly `.cu` codes.

Well, before going that deep, we still have some stains in the logic surface, let's sweep them out..... blah!

###### turning convolution into matrix multiplies

Nowadays convolutional operations are mapped into matrix multiply operations which can directed be processed by GPUs and CPUs.

Suggested in [this paper](http://cas.ee.ic.ac.uk/people/btc00/index_files/Convolution_filter.pdf), GPUs are optimal when processing data in matrices or as vectors. Further information are given in [this post](https://stackoverflow.com/questions/46213531/how-is-using-im2col-operation-in-convolutional-nets-more-efficient) which listed some developed GEMM (general matrix to matrix multiplication)

> Scientific programmers, have spent decades optimizing code to perform large matrix to matrix multiplications, and the benefits from the very regular patterns of memory access outweigh any other losses. We have an optimized CUDA GEMM API in cuBLAS library, Intel MKL has an optimized CPU GEMM while ciBLAS's GEMM API can be used for devices supporting OpenCL.





