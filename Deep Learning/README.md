1. `softmax`和`cross-entropy`是什么关系？  
`softmax`将一组输出结果转换成一个概率分布；然后`cross-entropy`用来衡量这个概率分布与理想概率分布之间的近似程度。
    > 从分类上来说，`softmax`是一个activation function，和`relu`是一类的，用于将神经网络的某一层的输出作非线性化处理。而`cross-entropy`是一个loss function，和`MSE`是一类的。
2. 为什么`cross-entropy`可以用来衡量两个概率分布之间的近似程度？  
[Click me](http://rdipietro.github.io/friendly-intro-to-cross-entropy-loss/)
3. 为什么分类问题用`cross-entropy`而回归问题用`mean squared error`？  
[讨论1](https://www.reddit.com/r/MachineLearning/comments/3ne2p7/crossentropy_vs_mean_square_error/)
[讨论2](https://jamesmccaffrey.wordpress.com/2013/11/05/why-you-should-use-cross-entropy-error-instead-of-classification-error-or-mean-squared-error-for-neural-network-classifier-training/)  
我的想法是，分类问题输出的是categorical data，而回归问题输出的是continuous data。离散型输出和连续型输出对问题的assumption不一样，这个assumption是包含了一定的先验知识的。而`cross-entropy`就是利用了这种assumption来达到更好的效果。
