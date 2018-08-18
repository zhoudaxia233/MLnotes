## Data Preprocessing

1. Data normalization is very important.
   > 不同的属性(对应于表格中的“列”)具有不同范围的变化尺度，例如年龄和收入，年龄的区间从0到100，而收入的区间则可以从0到1000000，后者是前者的10000倍。如果在进行数据分析之前不进行normalization的话，那么“收入”这个变量对最终结果的影响能力就会远远大于“年龄”。为了消除每个属性由于自身变化范围的不同而对最终结果造成的不良影响，我们就需要进行Data normalization。
2. Three methods of data normalization:
   > Simple Feature Scaling: x<sub>new</sub> = x<sub>old</sub> / x<sub>max</sub>  
   > Min-Max: x<sub>new</sub> = (x<sub>old</sub> - x<sub>min</sub>) / (x<sub>max</sub> - x<sub>min</sub>)  
   > Z-score: x<sub>new</sub> = (x<sub>old</sub> - &mu;) / &sigma;
   >> 当我们在度量两个变量的相关性的时候，会遇到一个概念叫“皮尔逊相关度(Pearson Correlation Coefficient)”。在我们使用皮尔逊相关度来度量两个变量的相关性的时候，并不需要事先进行Data normalization处理，因为皮尔逊相关度的计算方法中已经包含了这样的处理，具体来说，包含了Z-score这种方式，使得处理后的数据服从标准正态分布。


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
