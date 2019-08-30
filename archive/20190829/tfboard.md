# Tensorboard for pytorch

PyTorch support tensorboard since 1.1.0. I have tried tensorboard weeks ago, but due to the failure of building graph, I continued using [visdom](https://github.com/facebookresearch/visdom) which is built by facebook.



Today I tried mmsr from CUHK mmlab, they adopted tensorboard in their work. There are so much advances for tensorboard so I decided to review the `torch.utils.tensorboard` again.



## Summary Writer

`torch.utils.tensorboard.SummaryWriter`



``__init__(log_dir=None, comment='', purge_step=None, max_queue=10, flush_secs=120, filename_suffix='')`

- `log_dir(string)` - Save directory location. __Default__: "runs/current+datatime+hostname". __However__ I think using the setting of trainer or model can be more explicit. 

  How to achieve a 'meta folder name':

  Here is the implementation of mmsr:

  `'{}_{}_{}_{}'.format(order, modelName, upscaleFactor, trainingDataset)`

  ``` python
  log_dir = '{}-{}-epoch{}-{}'.format(name, epoches, upscaleFactor, order)
  ```

  __Note the mmsr's source code don't contain a existing tb-log sensor module__ We have to add a scanning module before setting the tensorboard dir. the log folder should be `Desktop/tb-log`

  __move the `.yaml` file and `model.pth` into the log folder !!__ easy resume the training

- `comment(string)` - deprecated when logdir was specified.

- `purge_step(int)` - when logging crashed at step T+X and restarts at step T, any whose global_step larger or equal to T will be purged and hidded from Tensorboard. Thus __resume training__ can be more smooth!

- `max_queue(int)` - Size of the queue for pending events, when queue if full, flush them to disks.

- `flush_secs(int)`- how often to flush to disks.

- `filename_suffix(string)` - suffix added to all event filenames in the log-dir

## Methods of Summary Writer

### `add_scalar(tag, scalar_value, global_step, walltime)`

`scalar(float)`

### `addscalars(main_tag, tag_scalar_dict, global_step, walltime)`

###  `add_histogram(tag, values, global_step, bins='tensorflow')`

```python
from torch.utils.tensorboard import SummaryWriter
import numpy as np
writer = SummaryWriter()
for i in range(10):
    x = np.random.random(1000)
    writer.add_histogram('distribution centers', x + i, i)
writer.close()
```

![_images/add_histogram.png](https://pytorch.org/docs/stable/_images/add_histogram.png)



### `add_image(tag, img_tensor, global_step, dataformats='CHW')`

__Note that one can use `torchvision.utils.make_grad()` to convert a batch of tensor to a image tensor__



### `add_images(tag, img_tensor, global_step, walltime, dataformats='NCHW')`

### `add_graph(model, input_to_model=None, verbose=False)`

- `model(torch.nn.Module)` - model to draw
- `input_to_model(torh.Tensor)`



