## Some useful commands in Jupyter notebook

1. `%%time`: 用来计时。当然，更多情况下我们使用[tqdm](https://github.com/tqdm/tqdm)，因为`tqdm`是一个进度条，可以计时还可以估算运行时间。
2. `%prun`: 一个profiler，它会告诉你哪部分代码最耗时，从而你可以依此进行优化。
