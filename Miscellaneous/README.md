1. 问：
   在Keras中，SGD和RMSprop，Adam处在同一个level上，都属于optimizer的一种，但是我记得，SGD强调的是batch size为1，也就是说，这个算法是在限制batch size，而batch size是在model.fit函数里设置的一个参数，那么为什么还要把SGD单独拿出来做一个optimizer呢？想用SGD的话，直接在model.fit函数里设置batch size为1不就可以了吗？SGD为什么会和RMSprop，Adam这种算法处在一个level上呢？

   答：
   > SGD全称是Stochastic gradient descent，与之对应的是BGD，Batch gradient descent，而这个BGD就是我们平时所说的梯度下降 (当我们在说gradient descent时，我们指的其实是BGD而不包含SGD)。

   > SGD的思想核心其实是，**每次只采取一小部分输入数据的计算结果来更新梯度**，而BGD则是采取全部的输入数据。

   > 当我们只谈及SGD和BGD时，我们说的SGD其实是一个广义的概念，如果狭义地说，这个SGD其实还要分成真·SGD (即batch size为1) 和 mini-batch (即batch size介于1和全部输入数据的个数之间)

   > SGD以及RMSprop，Adam，都是采用了“**只采取一小部分输入数据来更新梯度**”这个思想研发出来的算法。只不过SGD是Naive版本，而RMSprop和Adam则是Advanced版本。

2. 问：
   SGD是随机梯度下降，那么，“**随机**”二字体现在哪里？

   答：
   > **随机**体现在训练最开始，要把所有输入数据都打乱。然后才开始一个一个迭代然后更新梯度。如下图：
   ![](/Miscellaneous/SGD.png)
   >>图片来自维基百科SGD的词条。
