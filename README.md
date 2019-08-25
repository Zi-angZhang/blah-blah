## This repository hodes my thoughts
#### 20190825

#####[Denoise and Super Resolution](archive/20190824/README.md)
Denoise networks looks similar to super resolution networks, Where is the node that I can bond them together?

---

#### 20190824

##### [Motherboard B7 Error](archive/20190824/b7Error.md)
My computer failed in booting and failed me.

---

#### 20190823

##### [A game of optimizers](archive/20190823/README.md)
What's momentum in optimizers? Where is the difference between optimizers?

##### [Where the time is costed in TPUs and GPUs](archive/20190823/TPUcompareGPU.md)
Huawei launched its Ascend 910, which claims to outperform by twice V100, Here I investigate the GPU and TPU again, understood how memory is allocated by the memory. Wow, padding may lead to a waste of memory.

##### [Crush has some sweet meanings](archive/20190823/crush.md)
Chen Li's <crush> was beautiful!

##### [Word list](archive/20190823/wordlist.md)

---

##### 20190822

##### [Understanding CNNs inspired by pattern matching](archive/20190822/README.md)
I think CNN is nothing but pattern matching.

##### [Understanding cards in our wallet](archive/20190822/cardsSimulation.md)    
I brought a Mi 4 smart band, confused about its "card simulation" function. Till now, the mechanism of RTID card is understood while getting my card to simulate my pass card is waiting for my spare time.

---

####20190821

##### [Speed data loading (Where do the time go in training?)](https://zi-angzhang.github.io/pytorch-load-faster/)
Training with x2 `batchSize` lead to fastering training, that observation never goes beyond expection because one-shot loading is faster twice smaller loading. However, when training with `batchSize = 64` takes 3 minutes to finish an epoch while `batchSize = 8` acquires 16 minutes, I feel shocked and decide to investigate. Till Now, I found `lmdb` is slightly faster when loading and is safe with multiprocess. 
