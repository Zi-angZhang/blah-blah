# Learn from mmsr

mmsr项目地址：https://github.com/open-mmlab/mmsr





## Tensorboard

mmsr使用tensorboard作为可视化工具，在以下方面优于网页缓存的visdom：

- 数据回看、下载、储存

  visdom数据通过手动设置env、title进行区分，tensorboard可以通过yaml配置文件直接区分，便于整理。下载和储存数据是visdom没有的特点。

- 自带更复杂的显示功能，例如数据拟合

- 记录更多信息，例如时间

在上述功能之外，Tensorboard支持显示compute graph

Note are distributed into [Tensorboard](archive/20190829/tfboard.md)



## SResNet