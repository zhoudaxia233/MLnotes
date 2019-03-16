在一些Python的深度学习相关的库中，例如`fastai`，它的文档和源码中都大量使用了[type annotation](https://www.python.org/dev/peps/pep-0484/)，因此如果我们要读懂源码，先要了解一下常用的annotation，以下是一个cheatsheet：(全部采用举例子的方式来说明)

1. 
```Python
def hello(e: Union[A, B, C]): pass
```
解释：参数e的类型为A, B, C之中的一个。

