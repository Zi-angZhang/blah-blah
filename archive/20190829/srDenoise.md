​	

# 大批次训练

在[Speed data loading (Where do the time go in training?)](https://zi-angzhang.github.io/pytorch-load-faster/)中我发现增大`batch_size`确实能提高机器的运算效率，但是从实践和别人的论文中，都能发现fine-tuning的时候小批次更有利于实现更小的loss。

__核心内容：提高通信占比，使用large batch训练__

- 
  《[ON LARGE-BATCH TRAINING FOR DEEP LEARNING: GENERALIZATION GAP AND SHARP MINIMA](https://openreview.net/pdf?id=H1oyRlYgg)》：这篇论文解释了Large Batch Training使收敛性变差的原因：使用Large Batch更容易落入Sharp Minima，而Sharp Minima属于过拟合，所以其泛化性比较差。

- 《[Accurate, Large Minibatch SGD:Training ImageNet in 1 Hour](https://arxiv.org/pdf/1706.02677.pdf)》：这是FaceBook提出的一篇极具争议性的论文，从实践上来说它的的复现难度也是比较大的。该论文从实践的角度出发，在ResNet上提出了一种针对Large batch training的训练方法，即learning rate scaling rule。当batch size相对于baseline增加N倍时，learning rate也要相应的增加N倍，但也指出batch size的提升有一个upper bound，超过这个值，泛化性依然会变得很差。这篇论文对learning rate scaling rule有一些公式推导，但并不本质，更多的是做了较强的假设。总体来说，这是一篇实验做得比较solid，但理论基础并不丰满的实践论文。

- 《[A BAYESIAN PERSPECTIVE ON GENERALIZATION AND STOCHASTIC GRADIENT DESCENT](https://arxiv.org/pdf/1710.06451.pdf)》：这是Google发在ICLR 2018上的一篇理论和实验都比较完善的论文。因为在ResNet上已经有了Learning Rate Scaling Rule的成功经验，因此该论文从贝叶斯的角度解释了泛化性和SGD。论文的核心观点是指出了Batch Training相对于Full Batch Training来说引入了Noise，而Noise具有波动的效果，这在论文里被称为Flucturate，它可以在更新时在一定程度上偏离Sharp Minima，从而进入Broad Minima，进而有了较好的泛化性，所以Noise起了较大的作用。进一步的，论文中将SGD的更新公式进行进行分析，等价为一个微分方程的定积分结果，通过将SGD更新公式与微分方程进行等价，导出了Flucturate的表达式，确定了影响其值的变动因素，即和Learning Rate与Batch size有关。若把Flucturate看做常量，那么Learning Rate与Batch Size可以近似看做是线性关系，这与论文2中的Learning Rate Scaling Rule一致。总体来说，这篇论文数学理论相对丰满的解释了Learning Rate Scaling Rule。

- 《[Don't Decay the Learning Rate, Increase the Batch Size](https://arxiv.org/pdf/1711.00489.pdf)》：这是Google发在ICLR 2018上的第二篇论文，这篇论文的实验和结论非常简单，但是理论基础依然来自于论文3，所以阅读此篇论文之前一定要精度论文3。该论文从推导出的Mini Batch SGD的Flucturate公式出发，提出了一种使用Large Batch Training的加速方法。因为在一个完整的模型训练过程中，通常会随着轮数的增加而适当对Learning Rate做Decay。通过论文3中给出的公式，即Flucturate固定时，Learning Rate与Batch Size成正比关系，引发了思考：究竟是Learning Rate本身需要Decay才能使训练过程继续，还是Learning Rate的Decay间接影响了Noise的Flucturate才能使训练过程继续？通过实验验证，真正影响训练过程的本质是Noise的Flucturate。因此我们考虑到Learning Rate与Batch Size的正比例关系，我们可以固定Learning Rate不变，而将Batch Size增加N倍来缩小Noise的Flucturate。定时增加Batch Size不但可以维持原有方式的Flucturate，还可以加速训练过程，减少Update的更新频次，增加计算通信占比，提高加速比。总体来说，该论文基于论文3为理论基础，提出了一种逐渐增加Batch Size提高计算加速比和收敛加速比的方法

这次我