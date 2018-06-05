
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
最大似然估计（MLE）和最大后验概率（MAP）都是用于估计概率分布。它们之所以相似，因为它们得到的都是一个单一逼近，而不是一个完整的概率分布。
在机器学习里面，MLE很常见，有时候，我们甚至在不知情的情况下使用它。例如，当我们用数据集拟合高斯分布时，把数据集样本均值和样本方差，用作高斯分布的参数，这就是MLE。
因为如果我们对高斯函数的均值和方差求偏导数，并优化使其最大（即求导数为零的点），那么我们得到的是计算样本均值和样本方差的函数。
另一个例子，机器学习和深度学习（神经网络等）中的大多数优化可以解释为MLE——softmax cross entropy loss。

我们仔细展开来看看：   
现在我们有一个关于θ的似然函数L(Θ|X)=P(X|θ)   
&theta;<sub>MLE</sub> = argmax<sub>&theta;</sub>    
<img src="/mle_vs_map/tex/bdda3f3059ed66076be293a727592952.svg?invert_in_darkmode&sanitize=true" align=middle width=98.61308324999997pt height=24.65753399999998pt/>
