# Building an Intrusion Detection System Using a Filter-Based Feature Selection Algorithm 
# 使用基于过滤器的特征选择算法构建入侵检测系统

Pushp Raj1, Sana Ansari1, Narendra Varude1, Ashwini Sagade2 
B. E Student, Department of Computer Engineering, Dr D Y Patil School of Engineering Computer Science,  Pune, India1 Professor, Department of Computer Engineering, Dr D Y Patil School of Engineering Computer Science, Pune, India2 

## 摘要：

随着互联网的发展，网络攻击的数量也与日俱增，入侵检测系统（IDS）也越来越多，入侵检测系统（IDS）的数据中不重要的部分已经在行为采集框架中形成了一个完整的问题。这些片段可以从动作的过程中恢复，此外，还可以屏蔽一个分类器，使其不依赖于精确的决策，尤其是在调整庞大的数据时。在本文中，我们提出了一种常见的基于信息的计算方法，即系统地挑选出最适合于游戏计划的部分。这种基于互信息的段保证计算可以直接和非线性地管理数据特征。在框架入侵信息披露的情况下，对其进行了研究。一种入侵检测系统(IDS)，是利用我们所建议的包含保证估计的组件来制造的。使用两个入侵可识别的证明评估数据集来调查入侵检测的执行情况，特别是KDD Cup 99和NSL KDD。结果表明，我们的组件决策为入侵检测提供了更基本的组成部分，实现了更高的精度和较低的计算成本，并在类方法中得到了最好的结果。

## 关键词：

入侵检测，特征选择，互信息，线性相关系数，最小二乘支持向量机，朴素贝叶斯分类器。

## 一、导言

 随着网络安全意识的不断提高，现有的解决方案还无法完全保护互联网应用程序和计算机网络免受DoS攻击和恶意软件等持续发展的网络攻击技术的威胁。因此，开发有效和自适应性的安全方法已成为比以往更关键。传统的安全技术，作为安全防御的第一道防线，如用户认证、防火墙和数据加密等，同时面临着不断发展的入侵技能和技术的挑战[1]。因此，强烈建议采用另一种安全防御措施，如异常检测系统（IDS）。最近，ODS以及反病毒软件已成为大多数组织的安全基础架构的重要补充。这两条线路的组合为防范这些威胁提供了更全面的防御并增强了网络安全。为了实现更好的网络安全，已经进行了大量的研究，开发了智能异常检测技术。基于C5决策树[2]和Kernel Miner [3]的Bagged boosting是构建异常值检测方案的两个最早尝试。 [4]和[5]中提出的方法已经成功应用机器学习技术，例如支持向量机（SVM），对不符合正常网络流量的网络流量模式进行分类。两个系统都配备了五个不同的分类器来检测正常流量和四种不同类型的攻击（即DoS，探测，U2R和R2L）。实验结果表明了SVM在ODS中的有效性和鲁棒性。 Mukkamala等人[6]研究了组装各种学习方法的可能性，包括人工神经网络（ANN），支持向量机和多元自适应回归样条曲线（MARS）来检测入侵。他们训练了五种不同的分类器，以区分正常流量和四种不同类型的攻击。他们将每种学习方法的表现与他们的模型进行比较，发现人工神经网络，支持向量机和MARS的集合在所有五个类别的分类准确性方面取得了最好的表现。 Toosi等人文献[7]将一组神经模糊分类器应用于检测系统的设计中，其中应用遗传算法优化分类器中使用的神经模糊系统的结构。基于预定的模糊推理系统（即分类器），对输入业务进行检测决定。最近，我们提出了一种基于异常的检测DoS攻击的方案[8]。该系统已经在KDD Cup 99和ISCX 2012数据集上进行过评估，并且分别获得了99.95％和90.12％的有希望的检测精度。然而，目前的网络流量数据往往很庞大，这对ODSs是一个重大挑战[9]。这些“大数据”会减慢整个检测过程，由于处理这些数据的计算困难，可能导致分类精度不理想。对大量数据进行分类通常会导致许多数学难题，从而导致更高的计算复杂度。作为一个著名的异常评估数据集，KDD Cup 99数据集是一个典型的大规模数据集的例子。
这个数据集包含了超过500万的训练样本和200万的测试样本。如此大规模的数据集阻碍了分类器的构建和测试过程，或者使分类器由于内存不足而导致的系统故障无法执行。此外，大型数据集通常包含有噪声、冗余或无信息的特性，这些特性对知识发现和数据建模提出了严峻的挑战。
## 二、文献调查

1] F. Amiri, M. RezaeiYousefi, C. Lucas, A. Shakery, N. Yazdani, Mutual information-based feature selection for intrusion detection systems, Journal of Network and Computer Applications 34 (4) (2011) 1184–1199. 

参考点：

本文提出了一种利用互信息法来度量特征间关系的正向特征选择算法。然后使用最优特性集训练LS-SVM分类器并构建IDS。特征选择是一种消除不相关和冗余特征并选择最佳特征子集的技术，可以更好地表征属于不同类别的模式。特征选择的方法通常分为过滤器和包装器方法。

2] A. Abraham，R. Jain，J. Thomas，S. Y. Han，D-scids：Distributed soft computing intrusion detection system，Journal of Network and Computer Applications 30（1）（2007）81-98。

参考点:

过滤算法利用独立的度量（例如信息度量，距离度量或一致性度量）作为估计一组特征关系的标准，而包装器算法利用特定的学习算法来评估特性的价值。与筛选方法相比，包装器方法在处理高维数据或大规模数据时通常要花费更多的计算成本。在本研究中，我们主要关注IDS的筛选方法。由于数据维数的不断增长，作为预处理步骤的特征选择已经成为构建入侵检测系统的重要组成部分。 

3] S. Mukkamala, A. H. Sung, Significant feature selection using computational intelligent techniques for intrusion detection, in: Advanced Methods for Knowledge Discovery from Complex Data, Springer, 2005, pp. 285–306.

参考点：

本文提出了一种新的特征选择算法，将KDD Cup 99数据集的特征空间从41维减少到6维，并使用基于支持向量机的入侵检测系统对6个特征进行评估。结果显示，使用所选功能时，分类精度提高1％。


4] S. Chebrolu, A. Abraham, J. P. Thomas, Feature deduction and ensemble design of intrusion detection systems, Computers & Security 24 (4) (2005) 295–307. 

参考点:

本文调查了使用Markov覆盖模型和决策树分析进行特征选择的性能，该性能显示了其将KDD Cup 99中的特征数量从41个减少到12个特征的能力。

5] Y. Chen, A. Abraham, B. Yang, Feature selection and classification flexible neural tree, Neurocomputing 70 (1) (2006) 305–313. [7] S.-J. Horng, M.-Y.Su, Y.-H.Chen, T.-W.Kao, R.-J.Chen, J.-L. Lai, C. D. Perkasa, A novel intrusion detection system based on hierarchical clustering and support vector machines, Expert systems with Applications 38 (1) (2011) 306– 313. 

参考点:

本文提出了一种基于柔性神经树(FNT)的检测方法。该模型应用了预处理特征选择阶段来提高检测性能。使用KDD Cup 99，FNT型号只有4个特征，检测精度达到了99.19％。

6] S.-J. Horng, M.-Y.Su, Y.-H.Chen, T.-W.Kao, R.-J.Chen, J.-L. Lai, C. D. Perkasa, A novel intrusion detection system based on hierarchical clustering and support vector machines, Expert systems with Applications 38 (1) (2011) 306–313.

参考点：

本文提出了一种基于SVM的IDS，它结合了层次聚类和SVM。采用分层聚类算法为分类器提供更少、更高质量的训练数据，以减少平均训练和测试时间，提高分类器的分类性能。在修正的标签KDD Cup 99数据集上进行了实验，其中包括一些新的攻击，基于svm的IDS的总体精度为95.75%，假正率为0.7%。所有上述检测技术都是在KDD Cup 99数据集上进行评估的。
 
7] R. Chitrakar, C. Huang, Selection of candidate support vectors in incremental svm for network intrusion detection, Computers & Security 45 (2014) 231–241.  

参考点：

本文提出了基于候选支持向量的增量式SVM算法（简称CSV-ISVM）。该算法应用于网络入侵检测。他们在Kyoto 2006+ [11]数据集上评估了基于CSV-ISVM的IDS。实验结果表明，它们的IDS在检测率和误报率方面产生了令人满意的结果。
 
8] J. Song, H. Takakura, Y. Okabe, M. Eto, D. Inoue, K. Nakao, Statistical analysis of honeypot data and building of kyoto 2006+ dataset for nids evaluation, in: Proceedings of the First Workshop on Building Analysis Datasets and Gathering Experience Returns for Security, ACM, 2011, pp. 29–36.

参考点:

在[8]中提出的降维方法是找出建立一个朴素贝叶斯分类器进行入侵检测的最重要的特征。在NSL-KDD数据集上进行的实验产生了令人鼓舞的结果。

## 三、建议的系统/系统概述
 
图1描述了所提出的入侵检测系统的框架。检测框架包括四个主要阶段：（1）数据收集，其中收集网络分组的序列;（2）数据预处理，训练和测试数据预处理和重要功能是可以找出一个类与其它类的区别（3）分类器训练，其中训练分类模型;以及（4）攻击识别，其中训练的分类器用于检测测试数据上的入侵。
 
建议的系统算法：
 
1.	开始
2.	首先，我们从训练数据集中收集训练标记的数据。 
3.	其次，我们处理收集的数据，对特征提取进行预处理，采用灵活的基于信息的特征选择或基于柔性线性相关系数的特征选择算法。 
4.	特征选择后，我们对数据进行分类。 
5.	分类后使用攻击分类算法识别攻击。 
6.	最后的结果表明入侵检测与否。 
7.	停止

## 四、系统架构

![6-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/6-1.png)  
图1 建议的系统架构

## 五、结论
 
最近的研究表明，构建IDS需要两个主要组件，一种强大的分类方法和高效的特征选择算法。本文提出了一种基于监督滤波器的特征选择算法，即柔性互信息特征选择（FMIFS）。 FMIFS是对MIFS和MMIFS的改进。 FMIFS建议对Battiti算法进行修改以减少特征间的冗余。这在实践中是可取的，因为没有特定的程序或准则来选择该参数的最佳值。所提出的入侵检测已经使用两种已知的入侵检测数据集进行了评估：KDD Cup 99和NSL KDD。另外，当使用KDD Cup 99数据集的校正标签子数据集时，所提出的IDShas与其他现有技术方法的结果相当。此外，对于KDDTest的实验，相比于在同一数据集上测试的其他检测系统，IDS产生最佳分类准确度。最后，基于对所有数据集的实验结果，可以得出结论，所提出的检测系统在检测计算机网络上的入侵方面取得了很好的效果。总体而言，与其他先进的模型相比，IDS的表现最好。


## REFERENCES 
 
[1] F. Amiri, M. RezaeiYousefi, C. Lucas, A. Shakery, N. Yazdani, Mutual information-based feature selection for intrusion detection systems, Journal of Network and Computer Applications 34 (4) (2011) 1184–1199.<br> 
[2] R. Battiti, Using mutual information for selecting features in supervised neural net learning, IEEE Transactions on Neural Networks 5 (4) (1994) 537–550. <br> 
[3] S. Chebrolu, A. Abraham, J. P. Thomas, Feature deduction and ensemble design of intrusion detection systems, Computers & Security 24 (4) (2005) 295–307. <br> 
[4] A. Abraham, R. Jain, J. Thomas, S. Y. Han, D-scids: Distributed soft computing intrusion detection system, Journal of Network and Computer Applications 30 (1) (2007) 81–98. <br> 
[5] S. Mukkamala, A. H. Sung, Significant feature selection using computational intelligent techniques for intrusion detection, in: Advanced Methods for Knowledge Discovery from Complex Data, Springer, 2005, pp. 285–306. <br> 
[6] Y. Chen, A. Abraham, B. Yang, Feature selection and classification flexible neural tree, Neurocomputing 70 (1) (2006) 305–313 <br> 
[7] S.-J. Horng, M.-Y.Su, Y.-H.Chen, T.-W.Kao, R.-J.Chen, J.-L. Lai, C. D. Perkasa, A novel intrusion detection system based on hierarchical clustering and support vector machines, Expert systems with Applications 38 (1) (2011) 306–313. <br> 
[8] G. Kim, S. Lee, S. Kim, A novel hybrid intrusion detection method integrating anomaly detection with misuse detection, Expert Systems with Applications 41 (4) (2014) 1690–1700. <br> 
 

