# A compare of TPUs and GPUs for transformers

Just read news saying Ascend 910 by Huawei just be lunched which promised 2 times faster as V100 by nvidia when dealing with `float16` or `int8`. So I just want to review something about TPUs and GPUs. 

I have read lots of information about TPUs and GPUs, but they leaked from my brain with nearly nothing left. With further and deeper understanding of Deep Learning, I hope the information I collected today can company me for a longer time.



Wow, I said __collected__, here is where I found the information. Finding information costs times as well. LOL

https://timdettmers.com/2018/10/17/tpus-vs-gpus-for-transformers-bert/



The post was based on BERT tasks which I was not familiar with. But Tim the author has clarified the operations:

> A common operation in BERT is matrix multiplication A*B=C where A is 256×1024 and B is 1024×1024 in dimension. 

__TPU__ split the matrix into 128×128 smaller matrix, 16 small matrix tiles from matrix A and we should load 64 tiles (matrix B) for each tile of A. So there is a total of `16*64 = 1024` loads of matrix tiles. At float16 there is a total of `32 MB` of data.

 If we look at the bandwidth of the TPU we find that we have 600 GB/s, so we need 5.2e-05 seconds to transfer the 32 MB of data.

__GPU__ bares smaller tiles with more processors. Tesla V100 bears 96 × 86 matrix tile for 16-bit data. if we take a V100 Tesla GPU, then we can run 160 of these in parallel at a full bandwidth with low memory latency. __Compared with TPU__, instead of 2 matrix units which can hold 128 × 128 matrices, the GPU has 160 units (80 SMs, 160 thread blocks, each thread block has two 96 × 96 matrices) , for matrix A we have 96 tiles and 121 for matrix B. In total we need to do `33*121` loads for a total of `70MB`

Note that both TPU and GPUs with Tensor Cores compute the respective matrix multiplication tile in one cycle. Thus the computation is about equally fast — the difference is only in how the memory is loaded.





### Comments

this post inspires me that the fee may be collected by transferring data in the real deep learning tasks. While I am currently using gtx 1080 ti for my training work, this rule also applies.

| GPU Engine Specs          |
| ------------------------- |
| CUDA Cores                |
| 3584                      |
| Graphics Clock (MHz)      |
| 1480                      |
| Processor Clock (MHz)     |
| 1582                      |
| __Memory Specs__          |
| Standard Memory Config    |
| 11 GB GDDR5X              |
| Memory Interface Width    |
| 352-bit                   |
| Memory Bandwidth (GB/sec) |
| 11 Gbps                   |

How to interpret CUDA cores and 