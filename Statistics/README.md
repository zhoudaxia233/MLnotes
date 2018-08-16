## Regression

1. What is **unbiased model**?
   > If the difference between this model's expected value and the true value of the parameter being estimated is nearly zero, then it's called a unbiased model.
2. What is **residual**?
    > **Residuals = Observed value – Fitted value**  
    > A residual is the difference between the observed value and the mean value that the model predicts for that observation.

线性回归，线性指的是关于**系数**是线性的，至于自变量的幂是无所谓的，二次也好三次也罢；非线性回归和线性回归都是可以拟合曲线的。  
一般来说，先试一下线性回归，*如果观察到了明显的bias*，即便R^2接近1也不要用，换一下非线性试试。  

**如何观察到明显的bias**?   

我们可以利用残差图(residual plots)，如果观察到明显的非随机的pattern，那就说明有bias。要注意，R^2不适用于非线性回归问题。

R^2之所以不适用于非线性回归问题，是因为：在线性回归模型中，Explained variance + Error variance = Total variance，R^2就是基于这个等式假设得出的公式。而在非线性回归模型中，Explained variance + Error variance != Total variance，因此便不能使用R^2。

Residual plots are important. If you observe a pattern in the residual plots, it means you need to adjust your model.

Residual plots ([详细请查看](http://statisticsbyjim.com/regression/check-residual-plots-regression-analysis/)): x轴是fitted value，也就是模型预测的值，y轴是residual value，也就是对应的残差。一个良好的model，其residual plot应该无规律地分布在0的附近。
