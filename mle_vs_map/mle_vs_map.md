
## MLE与MAP之间的关系    
最大似然估计（MLE）和最大后验概率（MAP）都是用于估计概率分布。它们之所以相似，因为它们得到的都是一个单一逼近，而不是一个完整的概率分布。
在机器学习里面，MLE很常见，有时候，我们甚至在不知情的情况下用到它。例如，当我们用数据集拟合高斯分布时，把数据集样本均值和样本方差，用作高斯分布的参数，这就是MLE。
因为如果我们对高斯函数的均值和方差求偏导数，并优化使其最大（即求导数为零的点），那么我们得到的是计算样本均值和样本方差的函数。
另一个例子，机器学习和深度学习（神经网络等）中的大多数分类问题，都可以解释为MLE——softmax cross entropy loss。

## Maximum Likelihood Estimation or MLE
我们先看看MLE，现在我们有一个关于θ的似然函数：
<p align="center">
L(θ|X)=P(X|θ)
</p>
那么MLE就是：  
<p align="center">
&theta;<sub>MLE</sub> = argmax<sub>&theta;</sub>P(X|θ) = argmax<sub>&theta;</sub>&prod;<sub>i</sub>P(x<sub>i</sub>|θ)
</p>
在这里，P(x<sub>i</sub>|θ)&le;1，相乘的结果由于取数值小于1的乘积会随着这些项数量的增加而逼近0，特别在计算机上，很容易产生计算下溢。因此，我们对原有函数做一下变换，取对数log，使其每一项相乘变换为每一项相加。因为对数函数仍然是单调增加，所以最大化原有的函数与最大化取对数之后的函数是等价的。变换后，我们得到如下函数：
<p align="center">
&theta;<sub>MLE</sub> = argmax<sub>&theta;</sub>logP(X|θ) = argmax<sub>&theta;</sub>&sum;<sub>i</sub>logP(x<sub>i</sub>|θ)
</p>
通过梯度下降(上升)方法对θ优化，求出上述函数最大值，这就是最大似然逼近(MLE)。

## Maximum A Posteriori Estimation or MAP
我们再来看MAP，根据贝叶斯公式，后验概率定义如下：
<p align="center">
P(θ|X) = (P(X|θ)P(θ))/P(X)
</p>
我们可以把分母拿掉，因为P(X)不受θ影响，得到：
<p align="center">
P(θ|X) ∝ P(X|θ)P(θ)
</p>
因此
<p align="center">
&theta;<sub>MAP</sub> = argmax<sub>&theta;</sub>P(X|θ)P(θ)
</p>
同样，取对数，得到
<p align="center">
&theta;<sub>MAP</sub> = argmax<sub>&theta;</sub>log&prod;<sub>i</sub>P(x<sub>i</sub>|θ)P(θ) = argmax<sub>&theta;</sub>&sum;<sub>i</sub>logP(x<sub>i</sub>|θ)P(θ)
</p>
对比MLE，MAP只是多了一项P(θ)，就是说，最大化似然函数加权先验θ概率，就是MAP。

## MLE is a special case of MAP
来看一个特殊例子，假如P(θ)是一个均匀分布，MAP函数如下：
<p align="center">
&theta;<sub>MAP</sub> = argmax<sub>&theta;</sub>log&prod;<sub>i</sub>P(x<sub>i</sub>|θ)P(θ) = argmax<sub>&theta;</sub>&sum;<sub>i</sub>logP(x<sub>i</sub>|θ)const = argmax<sub>&theta;</sub>&prod;<sub>i</sub>P(x<sub>i</sub>|θ) = &theta;<sub>MLE</sub>
</p>
可见，MLE是MAP的一个特例。

<p align="center"><img src="https://raw.githubusercontent.com/DeepAIExpert/Articles/master/mle_vs_map/7fda39033b3b0eb36569da9f1e6723eb.gif" /></p>
