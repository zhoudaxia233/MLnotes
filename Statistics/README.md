## Data Preprocessing

1. Data normalization is very important.
   > 不同的属性(对应于表格中的“列”)具有不同范围的变化尺度，例如年龄和收入，年龄的区间从0到100，而收入的区间则可以从0到1000000，后者是前者的10000倍。如果在进行数据分析之前不进行normalization的话，那么“收入”这个变量对最终结果的影响能力就会远远大于“年龄”。为了消除每个属性由于自身变化范围的不同而对最终结果造成的不良影响，我们就需要进行Data normalization。
2. Three methods of data normalization:
   > Simple Feature Scaling: x<sub>new</sub> = x<sub>old</sub> / x<sub>max</sub>  
   > Min-Max: x<sub>new</sub> = (x<sub>old</sub> - x<sub>min</sub>) / (x<sub>max</sub> - x<sub>min</sub>)  
   > Z-score: x<sub>new</sub> = (x<sub>old</sub> - &mu;) / &sigma;
   >> 当我们在度量两个变量的相关性的时候，会遇到一个概念叫“皮尔逊相关度(Pearson Correlation Coefficient)”。在我们使用皮尔逊相关度来度量两个变量的相关性的时候，并不需要事先进行Data normalization处理，因为皮尔逊相关度的计算方法中已经包含了这样的处理，具体来说，包含了Z-score这种方式，使得处理后的数据服从标准正态分布。

针对于**线性回归问题**：  
数据预处理的过程中，有一个很重要的问题，“到底数据集中的哪些属性对于我们预测target的值是更加重要，更有影响的？”  
我们需要逐个属性进行考察，第一步就是查看它们的数据类型，需要转换数据类型的就转换，然后，分成如下两个类别来进一步考察：  

对于**Categorical variables**：
> 1. 通过boxplot看一下该属性不同值的数据分布，如果这一步没啥问题，则进入步骤2
> 2. 通过value_counts()看数据量是否足够，能否有代表性和说服力，如果这一步没啥问题，则进入步骤3
> 3. 通过groupby看一下这个属性同target属性之间的关系，然后转换成pivot表格以便于更好地观察，还可以进一步画出heatmap。最后再应用ANOVA方法，便可以最终确定某个属性是否对最终的预测有较大的作用。

对于**Numerical variables**：
> 利用scipy中的stats类，调用其pearsonr方法，然后传入需要考察的属性以及target属性，该函数将会返回两个值，第一个值是皮尔逊相关度，第二个是p-value。p-value告诉你这两个属性是不是有关系，皮尔逊相关度告诉你这两个属性的关系有多强烈。

举个例子，假设我们要考察color这个属性对售价price的影响，则有以下代码：
```
from scipy import stats
pearson_coef, p_value = stats.pearsonr(df['color'], df['price'])
```
如果要可视化的话，可以使用seaborn这个库的regplot方法：
```
import seaborn as sns
sns.regplot(x="color", y="price", data=df)
```

一般来说，当p-value:
- < 0.001 we say there is strong evidence that the correlation is significant,
- < 0.05; there is moderate evidence that the correlation is significant,
- < 0.1; there is weak evidence that the correlation is significant, and
- is >  0.1; there is no evidence that the correlation is significant.

而对于皮尔逊相关度，其值的区间在[-1,1]:
> 皮尔逊常用来表征两个变量之间的线性相关关系，用于线性回归。
- **1**: total positive linear correlation,
- **0**: no linear correlation, the two variables most likely do not affect each other
- **-1**: total negative linear correlation.


## Regression

1. What is **unbiased model**?
   > If the difference between this model's expected value and the true value of the parameter being estimated is nearly zero, then it's called a unbiased model.
2. What is **residual**?
    > **Residuals = Observed value – Fitted value**  
    > A residual is the difference between the observed value and the mean value that the model predicts for that observation.

线性回归，线性指的是关于**系数**是线性的，至于自变量的幂是无所谓的，二次也好三次也罢；非线性回归和线性回归都是可以拟合曲线的。  
一般来说，先试一下线性回归，*如果观察到了明显的bias*，即便R<sup>2</sup>接近1也不要用，换一下非线性试试。  

**如何观察到明显的bias**?   

我们可以利用残差图(residual plots)，如果观察到明显的非随机的pattern，那就说明有bias。要注意，R<sup>2</sup>不适用于非线性回归问题。

R<sup>2</sup>之所以不适用于非线性回归问题，是因为：在线性回归模型中，Explained variance + Error variance = Total variance，R<sup>2</sup>就是基于这个等式假设得出的公式。而在非线性回归模型中，Explained variance + Error variance != Total variance，因此便不能使用R<sup>2</sup>。

Residual plots are important. If you observe a pattern in the residual plots, it means you need to adjust your model.

Residual plots ([详细请查看](http://statisticsbyjim.com/regression/check-residual-plots-regression-analysis/)): x轴是fitted value，也就是模型预测的值，y轴是residual value，也就是对应的残差。一个良好的model，其residual plot应该无规律地分布在0的附近。
