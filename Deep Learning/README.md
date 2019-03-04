1. `softmax`和`cross-entropy`是什么关系？  
`softmax`将一组输出结果转换成一个概率分布；然后`cross-entropy`用来衡量这个概率分布与理想概率分布之间的近似程度。
    > 从分类上来说，`softmax`是一个activation function，和`relu`是一类的，用于将神经网络的某一层的输出作非线性化处理。而`cross-entropy`是一个loss function，和`MSE`是一类的。
2. 为什么`cross-entropy`可以用来衡量两个概率分布之间的近似程度？  
[Click me](http://rdipietro.github.io/friendly-intro-to-cross-entropy-loss/)
3. 为什么分类问题用`cross-entropy`而回归问题用`mean squared error`？  
[讨论1](https://www.reddit.com/r/MachineLearning/comments/3ne2p7/crossentropy_vs_mean_square_error/)
[讨论2](https://jamesmccaffrey.wordpress.com/2013/11/05/why-you-should-use-cross-entropy-error-instead-of-classification-error-or-mean-squared-error-for-neural-network-classifier-training/)  
我的想法是，分类问题输出的是categorical data，而回归问题输出的是continuous data。离散型输出和连续型输出对问题的assumption不一样，这个assumption是包含了一定的先验知识的。而`cross-entropy`就是利用了这种assumption来达到更好的效果。
4. 是否可以通过增大卷积操作的stride，来避免使用`pooling`操作？  
是的。可以看这篇paper: [Striving for Simplicity: The All Convolutional Net](https://arxiv.org/abs/1412.6806)  
5. 在使用`transposed convolution`进行upsampling的时候，往往会出现"Checkerboard Artifacts"，这是为什么呢？如何尽量避免这种现象？  
我们先说如何尽量避免，在设置transposed convolution layer的时候，一定要选择一个可以被stride整除的kernel size；或者说，只要`kernel size` % `stride` == 0即可。不过即使这样，也还是有可能存在artifacts。于是还有另一种方法，就是先利用Nearest-Neighbor Interpolation对图片进行resize，然后接一个卷积操作 (我们把这种先resize再卷积的组合操作称为`resize-convolution`)，来达到同样的目的，而且完全不会有artifacts。这样做，仅从减少artifacts的角度来说，`resize-convolution`完胜`transposed convolution`。  
至于为什么会出现这种现象，这里有一个很好的博客，还是可交互式的： [Deconvolution and Checkerboard Artifacts](https://distill.pub/2016/deconv-checkerboard/)  
