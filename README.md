# Auto-ML

#Paper list:

    ---
    
    Efficient and Robust Automated Machine Learning
    
    Auto-WEKA- Combined Selection and Hyperparameter Optimization of Classification Algorithms
    
    Sequential Model-Based Optimization for General Algorithm Configuration
    
    ParamILS- An Automatic Algorithm Configuration Framework
    
    Algorithms for Hyper-Parameter Optimization
    
    Initializing Bayesian Hyperparameter Optimization via Meta-Learning
    
    ---
    
    
#贝叶斯优化

     贝叶斯优化其实就是在函数方程不知的情况下根据已有的采样点预估函数最大值的一个算法。该算法假设函数符合高斯过程(GP). GP是多变量高斯分布（Multivariate Gaussian Distribution）的一个延伸(我应该会抽空写一章节讲解多变量高斯分布在Bayesian Optimization里的应用). 我们都清楚一个随机变量符合正态分布时它的方差，均值，分布函数等概念。当两个即以上变量仍服从正态分布，并且这些个随机变量之间有一定影响时，我们称这是多变量高斯分布。当无穷多变量他们之间的任意都符合多变量高斯分布时，可以看作是高斯过程。而这些变量都可以看作是某个函数上的采样点，所以我们说整个函数符合高斯过程。
     
     贝叶斯优化会选取未知函数的中数个已知点，作为先验(prior)，假设这些点是GP中的一部分，即他们服从多变量高斯分布。根据多变量高斯分布的一些性质，可以计算出这些点中每一个点的均值(mean)和方差(variance) 。我们不知道函数是什么，但是我们可以获得函数不同自变量下的因变量。举个栗子，假设我们有y=-x*x函数，然而我们并不知道它是这个样子，我们知道的是x=1,2,3..10所对应的y的值。如果我们想要的话，我们也可以找到x=1.5,2.5..时对应的y的值。我们取x=1,2,3..10作为prior, 获得对应的y值。 同样，如果我们能决定下一个采样点，与前面已经有的点“拼接”成更高维度的一个多变量高斯分布，我们也能计算出这个点的均值和方差。我们通过最大化收获函数(Acquisition Function，我并没有发现谁翻译这个Acquisition Function,自己随意译的，以后简称AF)来获得哪个采样点作为下一个采样点。
     
    我们为什么要找下一个采样点呢？贝叶斯优化的目的是找到当x等于某个值的时候y得到最大. 我们随机选取的10个点x=1..10里很可能没有包含那个值(对y=x*x来说就是0)，那么我们需要找下一个点x, 获得其对应的采样点y. 这“下一个x”,是基于我们对前面10个点的多变量高斯分布的假设以及最大化AF而得到的，现目前为止我们认为的y的最大值最可能出现的位置(恩，，个人认为这句话我还是总结得比较好的，，)。比如现在我们找到x=0.8为“下一个x”， 那么现在我们就有11个采样点，x=0.8,1,2...10 和他们对应的y值。这时候这11个点服从多变量高斯分布，我们再次最大化AF(每一次最大化AF，都需要多变量高斯分布的信息)，得到"下一个x"，如x=0.5,经过一定数量的迭代，我们可能可以得到最大点在x=0.1之类。

    
