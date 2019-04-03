## Some useful commands in Jupyter notebook

> 注意：`%`表示对应行的命令；`%%`表示对应单元格的命令。(一个单元格可以包含多行命令)

1. `%time`: 用来计时。当然，更多情况下我们使用[tqdm](https://github.com/tqdm/tqdm)，因为`tqdm`是一个进度条，可以计时还可以估算运行时间。
2. `%prun`: 一个profiler，它会告诉你哪部分代码最耗时，从而你可以依此进行优化。
3. `%debug`: 一个debugger，当你的某段代码出了bug，在它的下面一个空白的单元格里敲这个命令，程序就会自动跳转到你出错的位置，供你进行debug操作。其操作方式和`pdb.set_trace()`是一样的。
