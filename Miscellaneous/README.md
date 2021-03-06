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

3. 问：
   准确率和召回率是怎么回事？F1 score又是啥？ROC和AUC又是什么？

   答：
   > 准确率(precision)就是你猜了一堆答案，其中正确的答案在你所有猜测结果中所占的百分比。召回率(recall)就是你猜了一堆答案，其中你猜对的答案在所有正确答案中所占的百分比。
   > 举个例子，假如你女票让你说一下她这一周里面分别涂了哪几个色号的口红，并且给你10次猜测的机会。假设她一共涂了7个色号，然后你用完了10次机会，也只猜到了其中6个，那么你这个猜测过程的准确率就是6/10，即60%；召回率就是6/7，即85.7%。

   > 至于F1 score (又叫Dice)，是为了解决“当我们有两个模型，一个召回率更高，一个准确率更高的时候，应该选哪个”的问题。F1 score就是准确率和召回率的调和平均数。那么为什么要使用调和平均数而非算术平均数呢？因为调和平均数相对于算术平均数，更强调较小值的重要性。假设准确率和召回率一个非常高一个非常低，那么算术平均数会处在中间，而调和平均数会偏低，而我们在选择模型的时候要注重类似于木桶理论中最短的那块板，因此我们选择调和平均数。

   > 关于ROC和AUC，请看[这个](https://www.zhihu.com/question/39840928/answer/241440370)链接。

4. 问：
   关于data normalization (aka. feature normalization, feature scaling)，我们是应该在划分训练集和测试集之前来进行，还是应该在划分训练集和测试集之后进行？为什么？

   答：
   > 应该在划分训练集和测试集**之后**来进行，也就是说，我们需要先划分好训练集，测试集，然后再进行data normalization操作。  
   > 我们之所以要有测试集，其实就是为了模拟日后在使用这个模型时要用到的真实数据。那么，如果我们在划分之前就进行了normalization，就相当于包含了“未来”的信息 (因为我们既用到了训练数据，又用到了真实数据，而真实数据在没有输入模型之前我们是无法获知的)，从而这个模型也就没有了说服力。  
   > 进一步解释一下什么叫**包含了未来的信息呢**：当我们实际使用一个模型的时候，我们对于即将要处理的数据是一无所知的，而如果我们选择先normalization再划分数据集的话，我们进行normalization操作所用到的均值和方差实际上是包含了测试集，训练集这个整体的均值和方差。在我们实际使用的时候，只有训练好的模型，也就是说我们只有训练集的均值和方差，而我们并不知道系统将会用于处理哪些数据，因此，我们就无法提前得知数据整体的均值和方差。所以，要谨记，先划分数据集，再进行normalization操作。

5. 问：
   data normalization (aka. feature normalization, feature scaling)应该只应用于input，还是应该应用在input以及output上？

   答：
   > 应该只应用在input上。具体讨论见：[click me](https://stats.stackexchange.com/questions/111467/is-it-necessary-to-scale-the-target-value-in-addition-to-scaling-features-for-re)

6. 问：
   Dice score和IOU (Intersection over Union)都是用来度量segmentation的好坏的评判标准，他们有什么区别？

   答：
   > IOU = TP / (TP + FP + FN)  
   Dice = **2**TP / (**2**TP + FP + FN)  

   > IOU <= Dice  
   相比之下，Dice倾向于平均情况，IOU倾向于最坏情况。

    补充说明：Dice score的原始定义其实是`2|X`&#8745;`Y|` / `(|X|+|Y|)`，而上面的定义则是Dice在二分类情况下的特殊形式。

7. 问：
   在划分training set和validation set的时候，一定要先把数据打乱然后再随机划分吗？

   答：
   > 看情况。多数时候都要打乱，但有些时候是一定不能打乱的。比如，时序数据。假设我们的训练数据是从2018年到2019年的数据。最好的划分就是按照时间的顺序来划分。例如，把2018年1月到2019年6月的数据划分到training set中，把2019年7月到2019年12月的数据划分到validation set中。因为我们的模型是为了预测之后的时间，比如2020年的情况，倘若我们划分数据集的时候打乱了顺序，training set中包含了2019年8月的数据，而如果validation set中也包含了2019年8月的数据，尽管可能不是一天的，但对于我们的模型来说这样也不是好事。因为我们引入了“未来”的信息。

   > 除了这种时序数据一般我们不要打乱随机抽取之外，还有一些特殊的情况也是。比如，当我们的样本空间是一个一个的聚类的时候，假设有三个聚类A，B和C，如果我们不打乱，将A聚类和B聚类作为training set，而C聚类作为validation set，这样的话，这个模型训练的准确率就比较有说服力。因为如果新来了一个样本点，这个样本点很可能不在训练时的两个聚类中；而我们在验证的时候，用到的验证集数据(C)恰恰也不在训练集(A, B)的分布中。但如果我们打乱并随机划分数据集之后，训练数据中可能既包含A聚类的数据点，又包含了B聚类的数据点，还包括了C聚类的数据点，这样在validation的过程中，准确率肯定远远高于没有打乱随机采样的模型，但是这个准确率高并没有什么说服力。因为我们要预测的东西的分布相当于已经在训练过程中提前被“剧透”了，即：我们可能要预测C这个分布中的某一个数据点，但由于训练时候我们就用到了C这个分布中的其他数据点作为训练数据，所以求C中其他数据点对于我们这个模型来说就是一个trivial的任务。所以这样validate得到的准确率并没什么说服力。
