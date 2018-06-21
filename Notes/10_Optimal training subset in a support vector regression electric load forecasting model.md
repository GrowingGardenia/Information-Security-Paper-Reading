# Optimal training subset in a support vector regression electric load forecasting model
# 支持向量回归电力负荷预测模型中的最优训练子集

JinXing Che a *，JianZhou Wang b，YuJuan Tang a
a南昌理工大学理学院，江西南昌330099
b兰州大学数学与统计学院，甘肃兰州730000

## 摘要：
本文提出了一种支持向量回归（SVR）的最优训练子集，该子集在解调功率下具有明显的优于基于全训练集SVR的优势，因为它解决了大样本内存复杂度O（N2）在不平衡数据回归中进行拟合。为了计算所提出的最优训练子集，通过将最优训练子集的大小的惩罚项与全训练集预测的平均绝对误差百分比（MAPE）相结合来构建近似凸性优化框架。此外，还介绍了寻找最优目标函数近似解的一种特殊方法，它使我们能够从完整训练集中提取最大信息，并提高整体预测精度。所提出的算法的适用性和优越性通过新南威尔士州三个不同样本大小的半小时电负载数据（每天48个数据点）实验来显示。尤其是，大型数据集开发方法的优势体现在CPU运行时间明显减少。
## 关键词：
支持向量回归、最佳训练子集、预测、电力负载、K最优训练子集方法

## 1.引言

负载预测在电力公司的日常运营中是无价的。它用于各种目的，如价格和收入弹性，能量转移调度，单位承诺和负载调度。随着负载管理策略的出现，负载预测在公用事业运营中发挥了更广泛的作用[1]。因此，精确，快速，简单和健壮的负载预测算法的发展对于电力公用事业及其客户来说非常重要。
随着统计学习理论的发展，支持向量回归（SVR）模型由于其对小样本，非线性和高维数据应用具有吸引力的特点和深刻的经验性能而变得非常有前途和流行[2-5]。 Quan等人[6]提出了非线性时间序列的加权最小二乘SVR局部区域算法。 Pai和Hong [7]提出了一种用遗传算法预测区域用电负荷的递归SVR模型。 Zhan和Cheng [8]采用稳健的SVR算法，报告了电力系统的谐波和谐波分析。文献[9-11]将两种不同的模型混合在一起，指出在竞争性市场中可以进一步提高绩效预测。
基于VC维理论和结构风险最小化原则，SVR解决方案的质量和复杂度不直接依赖于输入空间的维数。然后，解决方案通过解决线性和框约束的大规模二次规划问题进行优化。然而，这个问题的记忆复杂度是O（N2）（N是训练数据点的数量）。因此，一些中等或较大训练样本容量的应用模型很难加载到内存中，无法通过标准SVR来解决。在中等或大样本量情况下确定最优训练子集对于SVR预测的泛化性能，计算效率，高预测准确性和数据可解释性非常重要[12]。另一方面，冗余数据不仅对SVR预测毫无用处，而且可能导致计算效率低和准确度低。因此，在训练集中应忽略什么冗余信息一直是统计学、模式识别、机器学习和计算机视觉等领域的中心话题。最近，Moustakidis和Theocharis [13]提出了一种有效的滤波器特征选择方法，以实现分类精度和降维之间令人满意的折衷。杨等人利用改进的遗传算法 [14] ， Hamdani等人[15]提出了两种特征选择算法。杨[16]介绍了一种新颖的聚光树用于特征选择。廖[17]研究了使用膀胱癌数据集中最小的最佳特征子集进行分类的神经模型。过去的特征选择工作强调了特征提取和分类，然而，对训练数据集缩减和时间序列预测的关键问题的关注较少。只有靠近决策边界的训练数据点（即支持向量）对最终预测模型产生影响，受此启发，我们提出了一种用于SVR的训练数据集简化算法。由于这些原因，提出了代表完整训练集最大信息的最优训练子集，以提供SVR训练样本量相对较小的平衡数据。此外，本文提出了一种用于计算最优训练子集的近似凸性优化框架，并建立了该算法的停止准则。 K最优训练子集，初步提出了一种新算法，以获得自然稀疏最优训练子集。下一步的研究将对凸面进一步的研究进行总结。
为了显示所提出的算法的适用性和优越性，收集新南威尔士州的半小时电负荷数据（每天48个数据点）。在选择神经网络，统计方法和其他混合模型之前，应仔细考虑电力负荷数据的性质和预期用途。比较实验的结果证明，基于该算法的时间序列预测控制系统具有以下优点：（1）由于我们建立了一个计算最优训练子集的近似凸性优化框架，该子集可以提取满量程的最大信息以最小尺寸设置训练集。（2）大中型训练集响应速度快，精度高。（3）对参数变化稳健。
在本文的第二部分，我们提出了新的预测算法，并给出了该方法的主要步骤。然后，解释提出的技术的背景。在第3节中，我们介绍研究设计，数据描述和三种绩效评估。获得的数值结果和比较在第4节中给出和讨论。在第5节中，我们简要回顾本文并展示未来的研究。
## 2. 新算法的明确过程
### 2.1 非线性动力学和数据预处理

预测的目标是根据自己的发展规则推断物体的未来。本研究采用非线性预测算法来预测电力负荷动态。该算法将单变量时间序列转化为多维相空间，表示不同时刻的系统状态。根据Takens的嵌入定理[18]，一个标量时间序列（例如电负载序列）yt，其中t = 1,2，...。 。 T可以按如下方式重建

![10-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-1.png) 

其中j = 1，2，... T-（m-1）τ，m是嵌入维数，τ是时间延迟。基于维度m中的相空间重构，我们可以以反射的形式构造底层动力学F：Rm→Rm <br>
 ![10-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-2.png) 
 
其中Yj和Yj + 1分别是描述系统在时间j（当前状态）和j + 1（未来状态）的状态的维度为m的向量。然后预测反射F：Rm→Rm可以表示为： <br>
 ![10-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-3.png) 
 
这里，它是非线性的，需要找到一个特定的函数表达式，这可以通过利用ε-SVR模拟非线性反射的良好能力来获得。
在用训练数据训练ε-SVR之前，必须对数据进行归一化处理，以确定ε-SVR的参数值[19]。为此目的通常使用各种标准化方法。刘等人[20]比较了基于用于目标识别的RPROP算法的6种不同的归一化方法，他们得出结论：线性归一化方法和组分白化方法给出了几乎最好的结果，并且概念简单。为了简单起见，我们在本研究中将数据线性地映射到指定范围[ymin，ymax]。假设y’max和y’min是变换变量范围的最大值和最小值; ymax和ymin是训练数据的最大值和最小值。所以变量y的每个值都被转换如下： <br>
 ![10-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-4.png) 
 
由于（ymax，y'max）和（ymin，y'min）是上式的两点，所以我们可以得到常数A和B，如下所示： <br>
 ![10-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-5.png) 
 
在使用所提出的方法之后，数据可以通过以下公式恢复到未标准化的数据。 <br>
 ![10-6](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-6.png) 
 
### 2.2 支持向量回归
支持向量回归（SVR）[21]是一种利用核函数的回归技术，它是六十年代在俄罗斯开发的广义肖像算法的非线性扩展。 本小节简要介绍SVR，它执行时间序列预测的非线性映射; 并且我们会向读者介绍优秀的调查，以便对其进行更全面的报道[22-26]。
假设我们有训练数据（x1，y1），… ，（xn，yn）⊂W×R，其中W表示输入图形xi的空间（例如W = Rn），yi是xi的相关输出值。 在ε-SVR [27]中，我们的目标是产生一个函数F（x），对于所有训练数据，它的实际获得的目标yi最多有ε偏差，同时尽可能“平坦”。 也就是说，只要它们小于ε，我们就不会在意误差，但不会容忍比这更大的偏差。 因此，我们得到了ε-SVR中[27]中所述的公式。 <br>
 ![10-7](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-7.png) 
 
其中n表示样本的数量，常数C> 0决定了F（x）的平坦度与容许偏差大于ε的量之间的折衷，ξi表示训练误差的上限，而ξ*i是受到ε不敏感的较低训练误差| yi - （<ω，xi>+ b）| ≤ε。 这个ε不敏感损失函数|εε| 可以用下面的等式来描述。 <br>
 ![10-8](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-8.png) 
 
ε-SVR不是最小化观察到的训练误差，而是试图最小化泛化误差界限以实现广义性能，这使得ε-SVR对异常值非常健壮。换句话说，ε-SVR将F（x）拟合到数据上，使得：（i）通过使αi和αi最小化来使广义误差界最小化，（ii）（1/2）ωTω被最小化为促进F（x）的平坦性，或避免过于复杂的拟合函数。最后，通过引入拉格朗日乘子，核心技巧和采用最优性约束，我们得到以下显式形式 <br>
 ![10-9](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-9.png) 
 
#### 2.2.1 拉格朗日乘子
在等式（11）式中，αi和αi*是所谓的拉格朗日乘子，是通过最大化方程（2）的对偶函数得到的。关键思想是从目标函数Eq构造一个拉格朗日函数和相应的约束通过引入一组双变量。方程中的最大双重函数（8）具有以下形式： <br>
 ![10-10](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-10.png) 
 
根据解决二次规划问题的Karush-Kuhn-Tucker（KKT）条件，式（11）中的（αi-α* i） （11），其中只有一些将被视为非零值。这些关于非零系数的数据点，其近似误差将等于或大于ε，被称为支持向量。直观地说，当接受低于ε的误差时，位于所谓的“ε-管”内的训练数据点对问题解决方案没有影响（换句话说，轻微移动它们的位置不会扰乱解决方案）。从某种意义上说，问题的复杂性与输入空间W无关，而仅取决于支持向量的数量。通常，ε值决定了支持向量的数量，它代表了解决方案的稀疏级别。

#### 2.2.2 内核技巧
对偶公式也是将支持向量机扩展到非线性函数的关键，SVR的这个特点被称为“核心技巧”[28]。等式（12）中的点积{xi，xj}对于非线性情况成为核函数{ф（xi），ф（xj）}- K（xi，xj）。这是通过函数ф：W→F将输入模式映射到高维空间F。如果一个函数可以满足Mercer的条件，那么它可以用作核函数[21]。在这项研究中，我们讨论了使用径向基核 <br>
  ![10-11](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-11.png) 
  
一个无限维映射空间对应于它。
### 2.3  K最佳训练子集方法（K-OTS）
在本小节中，我们提出了一种新技术，以确保获得的训练子集从全套训练集中提取最大信息。它可以从整个训练对中选择一些训练对与最大差异，并将其应用于寻找最优训练子集（OTS）。由K表示训练子集的大小，一个常数待定，因此OTS具所有K个训练子集之间的有最大值信息。
我们的K-OTS方法是一种基于实例的算法，将最不常见的对象分配给子集。通常使用欧几里得距离作为距离度量，也可以使用另一个度量，例如重叠度量（或汉明距离）。所以更远的点比更近的点包含更多的信息。算法的训练阶段包括获得训练子集和训练SVR算法。在预测阶段，基于OTS的SVR预测测试点。为了获得表示训练集的最大信息的K个元素，称为K-OTS算法，实现了以下简单的伪代码。
输入：T=〖（x_i，y_i）〗_(i=1)^n   ,训练数据集; n，独立样本数量; K，训练子集的数量; X0，训练子集的初始元素。
输出：OTS，K-最佳训练子集。
终止条件：培训子集的数量达到K. <br>
 ![10-12](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-12.png) 
 
找到最合适的K值的关键问题将在以下小节中详细解决。

### 2.4 一种近似凸性优化框架的最佳训练子集
令T =（X1，y1），...，（Xn，yn）是完整的训练集。 Xis是输入值，而yis是系统的相应输出值。
最优训练子集尽可能少的点数，包含完整训练集的最大信息，可以概括为以下优化问题： <br>
 ![10-13](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-13.png)
 
其中m，n分别是最优训练子集和全训练集合T的大小，MAPE（m，T）是基于m的最优训练子集的SVR的平均绝对误差百分比（MAPE）；该λ是调整参数控制最优训练子集的大小和MAPE（m，T）之间的折衷（即预测准确性）。在等式（15）中，第一项表示OTS的浓度比，第二项表示基于OTS的拟议模型的预测精度。模型应该首先考虑模型的准确性，那么λ一般设置为相对较小的数字。大λ是，我们更关注OTS的规模。特别地，如果我们设置更适合小型OTS的λ = 0，那么所提出的模型将会得到最小误差而不考虑OTS的大小。在实践中，人们可以使用经验规则来粗略调整λ 的值。
寻找上述问题的确切解决方案在计算上很难。已经开发了基于K-OTS的近似方法和目标函数f（m）的性质。通常，有用信息随着值m的增加而增加，冗余信息也增加;有用信息一开始占主导地位，随后逆转。我们认为目标函数是变量m的连续函数。因此，以下属性直观地成立：  <br>
 ![10-14](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-14.png) 
 
在f(m)上使用上述属性，有 <br>
 ![10-15](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-15.png) 
 
作者还提供了一种通过最小化优化目标函数来找到最佳训练子集的经验方法。
利用这种凸性，从整个训练集中获得最小尺寸的最优子集变得更容易和更快。我们提出求解m的三个初始值的最优训练子集，从而通过训练SVR模型来计算相应的目标函数值。从实际的角度来看，我们提供了一个稳定的迭代方案和模型覆盖标准，并且调整m的更多初始值要容易得多。事实上，没有凸性，解决方案可能会达到局部最小值。用于计算最小最优训练子集的迭代算法，其缩写为OTS-SVR，可归纳如下：
输入：T=〖（x_i，y_i）〗_(i=1)^n，训练数据集; n，独立样本的数量; m1，m2，m3，最佳训练子集的三个初始尺寸值; X0，最佳训练子集的初始元素。
输出：m：最佳训练子集的收敛大小值。
终止条件：max（m1，m2，m3） - min（m1，m2，m3）= 0或迭代次数大于n / 2。 <br>
 ![10-16](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-16.png) 
 
Sayre和Poore [29]提出了多种停止统计测试的标准，并且我们根据m的三个值已经收敛到相同的值的程度来选择模型覆盖标准。以下实验研究中的收敛性进一步证明了优化框架的凸性。
电负载的行为不容易被捕获。它具有各种非线性特征。受SVR模型的启发，仅对小样本具有强大的非线性学习能力，因此，具有大样本和非线性建模能力的策略是预测电负载的好选择。首先，作者提出了K-OTS算法从2.3节讨论的训练集中提取具有最大信息特征的K个元素。然后，如上所述，让OTS-SVR算法获得预测过程的最小OTS。研究框架如下：
第1步：使用数据预处理公式（5）产生一个规范化系列，它将数据在指定的范围内线性地映射。 <br>
 ![10-17](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-17.png) 
 
步骤2：考虑步骤1中预处理数据的相空间构造。 <br>
![10-18](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-18.png) 

步骤3：将步骤2中的相位空间放入训练集作为OTS-SVR算法的输入，并获得OTS。
步骤4：在步骤3中用OTS训练SVR，并用这个训练好的SVR预测测试集。
第5步：使用数据处理公式（7）恢复到非标准化的数据。

#### 2.4.1  OTS-SVR的灵敏度分析
OTS-SVR模型受到一些参数的影响，涉及三个不同的领域。第一组包括参数m1，m2，m3和λ。 m1，m2，m3可以收敛到相同的最佳值，如下面的实验研究所示; λ一般设置为相对较小的数字。第二组与非线性动力学参数有关，即时间尺度τ和方程的维数m。（通常，时间刻度τ设置为1）。第三组，与SVR本身有关，公式（8）方程C的平滑因子，损失函数公式（9）和公式14中的内核函数的参数δ2。在下面通过OTSSVR模型进行的电力负荷预测中，我们简单地提供了在公式18范围中的SVR的粗略调整。其余参数可以由相应的理论给出[30]。
## 3 研究方法论
本研究的重点是在新南威尔士电力市场提出的OTS-SVR模型的适用性和优越性。如前所述，标准SVR和新SVR模型被用来预测三种不同样本大小下的电力负荷。更具体地说，解决了以下研究问题：（1）该模型在大样本量预测中的适用性如何？即OTS-SVR模型能够提取最小OTS并以高精度预测未来值吗？（2）OTS-SVR模型相对于现有SVR模型的预测精度是多少？

### 3.1 案例分析
新南威尔士州的电力负荷数据每半小时收集一次（每天48个数据点）（见图1）。为了公平比较，在实验中选择具有小，中和大样本量的数据集。在第一个实验中，2007年5月3日至2007年5月4日，分别使用标准SVR和新算法训练新南威尔士电力负荷，并使用2007年5月5日的电力负荷进行测试（小样本量： 144个数据点）。在第二个实验中，上述两个模型分别由2007年5月2日至2007年5月14日在新南威尔士州的电力负荷训练。然后，我们从2007年5月15日至2007年5月21日进行一周预测（中等样本量：960个数据点）。在第三个实验中，使用具有31天（1488个数据点）的数据集来评估所提出的模型在大样本量预测中的适用性，即故意不选择小样本大小的数据集。为了构建所考虑数据的预测模型，可用信息包括负载预测2天之前29天的半小时历史负载数据。非常大的训练集不应该与标准的SVR算法进行比较，因为它很费时并且可能在学习过程中过度训练。
前两个实验是证明我们的新算法与现有的SVR算法相比，在中小样本情况下的优越性和有效性，而最后一个实验是显示大样本量情况下的适用性和集中率。表1中显示了模型中使用的参数。 <br>
 ![10-19](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-19.png)
 
图1. 2007年5月1日至2007年6月1日新南威尔士州的半小时电力负荷。
### 3.2 模型评估方法
为了评估预测能力，我们采用三种不同的统计指标来检验预测精度：均方根误差（RMSE），平均绝对误差（MAE）和平均绝对误差百分比（MAPE）。他们可以表达如下： <br>
 ![10-20](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-20.png) 
Pi和Ai分别是第i个预测值和实际值，n是预测总数。
为了评估OTS的大小，浓缩比（CR）定义如下： <br>
 ![10-21](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-21.png)
 
其中m是OTS的大小，n是训练集的总大小。

## 4 实证结果与分析
我们详细描述了新SVR框架的思想，算法和过程的基础。通过构造逼近凸性优化目标函数来计算所提出的最优训练子集，可以建立中等或大样本尺寸的新SVR模型。现在，为了评估所提出的算法的性能，我们使用标准SVR模型和所提出的新的SVR模型对三个不同样本大小数据集上的预测电负载值进行比较，然后显示不同样本下的适用性和浓度比大小的情况。 <br>
  ![10-22](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-22.png) 
  ![10-23](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-23.png) 
  
图2. OTS-SVR模型的预测电力负荷，第一组训练集的标准SVR和原始数据以及相应的误差的比较。 （第一套培训是2007年5月3日至2007年5月4日在新南威尔士州的电力负荷数据。） <br>
  ![10-24](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-24.png) 
  
图3. OTS-SVR模型预测的电力负荷，第一套测试集的标准SVR和原始数据以及相应误差的比较。 （第一套测试集是2007年5月5日在新南威尔士州的电力负载数据。）
在第一个实验中，我们提出的SVR模型优于标准SVR模型。在附图中，在图2和图3中，分别显示了标准SVR模型和新SVR模型下的训练和预测结果。绝对误差也显示在相应的图中。在训练阶段，新SVR的训练误差稍好于SVR的训练误差，如图2所示。这是因为SVR的稍微过度拟合是由第一个数据集中的冗余训练样本造成的。预测结果见图3.我们可以看到，我们的新SVR算法提供了比标准SVR算法更准确的预测。尽管改进表明最优子集提取最小样本量训练集的最大信息并不具有统计意义，但我们的新算法确实在这种情况下取得了较好的结果。请注意，我们的OTS-SVR算法放弃了冗余信息，并导致更好的统计解释。
在第二个实验中，我们进行了中等样本量的比较实验。为了解决大尺寸复杂性的问题，我们设置了一个相对较大的值λ（λ= 0.37086）。本研究旨在展示中等样本量情况下的适用性和浓度比，因此更关注方程式的第一部分。4和5获得了类似的结果。 <br>
  ![10-25](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-25.png) 
  
图4. OTS-SVR模型的预测电力负荷，第二套训练集的标准SVR和原始数据以及相应误差的比较。 （第二套训练集是2007年5月2日至2007年5月14日在新南威尔士州的电力负载数据。） <br>
  ![10-26](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-26.png)
  
图5. OTS-SVR模型的预测电力负荷，第二套测试装置的标准SVR和原始数据以及相应的误差的比较。 （第二套测试套件是2007年5月15日至2007年5月21日在新南威尔士的电力负载数据。）
图5显示了一个星期的预测来看长期预测。所提出的新SVR模型的预测曲线比标准SVR模型更适合全时间序列，这表明了我们最优训练子集的价值。
如果训练集规模太大，调查标准SVR算法可能是不切实际的，因为它需要太多时间才能得到结果（在这种情况下，其运行时间大于100800s）。因此，第三个大样本量的实验仅由所提出的新的SVR模型来执行。第三个实验的主要目标是显示大样本量情况下的适用性和浓度比。
第三个实验显示这种情况提前2天预测。根据我们先前的论点，OTS-SVR模型可以获得用于SVR训练的OTS。这种OTS可以大幅度降低模型的复杂性并克服一些计算困难，而优化框架设计可以帮助我们找到OTS的最佳尺寸值。这个实验的详细预测结果如图6和7所示。
值得指出的是，λ可能会影响我们新的SVR算法的性能。对于不同的λ值，我们可以控制两个优化框架之间的权衡。λ越大，我们就越关注最优训练子集的大小。所以，如果我们设置λ = 0，所提出的SVR在不考虑最优训练子集的大小的情况下将得到最小训练误差，并且将更适合于回归。在实践中，可以根据他的经验规则大致调整价值。 <br>
  ![10-27](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-27.png) 
  
图6. OTS-SVR模型预测的电力负荷与第三套训练集的原始数据及相应误差的比较。 （第三套训练集是2007年5月1日至2007年5月29日在新南威尔士州的电力负载数据。） <br>
  ![10-28](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-28.png) 
  
图7. OTS-SVR模型预测的电力负荷与第三组测试的原始数据和相应的误差的比较。 （第三套测试是2007年5月30日至2007年5月31日在新南威尔士的电力负载数据。）
通过给出参数m生成8-10，不同的初始值从m = 1到m = N（N是完整训练集的数目）变化。 对于m的不同初始值，我们获得最优训练子集的最小数目。由于在我们的K-OTS方法中给出了相同的初始元素，相同尺寸的最优训练子集指示相同的最优训练子集。不同初始值的图似乎很快变平，这表明我们的方法随着迭代次数变大而收敛。
在表2中，应用了ANOVA的单向阻塞设计。 测试假设定义如下： <br>
  ![10-29](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-29.png) 
  
 图8.第一优化训练子集的最小尺寸图：[左] m1 = 6，m2 = 16，m3 = 47; [center] m1 = 8，m2 = 19，m3 = 47; [右] m1 = 18，m2 = 28，m3 = 41。如图所示，随着迭代次数的增加，收敛达到相当快。 <br>
 ![10-30](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-30.png) 
 
图9.第二优化训练子集的最小尺寸图：[左] m1 = 31，m2 = 52，m3 = 104; [center] m1 = 8，m2 = 21，m3 = 41; [右] m1 = 12，m2 = 21，m3 = 62。如图所示，随着迭代次数的增加，收敛速度相当快。 <br>
  ![10-31](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-31.png) 
  
图10.第三优化训练子集的最小尺寸图：[左] m1 = 18，m2 = 26，m3 = 53; [center] m1 = 56，m2 = 28，m3 = 14; [右] m1 = 76，m2 = 31，m3 = 9。如图所示，随着迭代次数增加，收敛达到相当快 <br>
  ![10-32](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/10-32.png) 
其中µ1,µ2和µ3是从实际数据，标准SVR和所提出的新SVR获得的平均值，其值在图3和5中示出。
从表2可以看出，最高达到α=0.05，F0.05,1.94 = 3.94，F0.05,1.334 = 3.84，在小样本情况下，F0 = 1.823,0.007 <3.94，这意味着µ1 = µ2，µ1 = µ3是真的。然而，在中等样本情况下，F0 = 4.291> 3.84，这意味着µ1！= µ2.该结果表明在中等样本情况下，原始数据与SVR模型之间存在显着差异。因此，在这种情况下，OTS-SVR模型显着优于标准SVR模型。
对于这三个数据集，利用三种性能指标来研究该模型的预测能力。以标准SVR为基线，报告浓度比和训练时间。
表3中，第一列表示模型，第二列表示训练评估方法，包括准确性，CPU训练时间和集中率，第三列表示测试精度评估方法。最优训练子集的大小为42，第一个数据集相应的集中率为43.75％，而第二个数据集的大小仅为48，相应的集中率为7.69％，大小为61和第三组数据的相应浓度比为4.38％。这个结果表明，这种情况下的冗余信息会随着整个训练集的规模变大而增加。 MAPEmax = 16.8344表明所有用于负荷预测的模型都是合理的。在第一次测试中，测试集的标准SVR的MAPE是16.8344，而OTS-SVR是12.0965。 MAEs和RMSEs的类似结果再次表明，所提出的预测模型在电力负荷预测中表现更好。可以看出，所提出的预测算法在第一种情况下给出了更准确的预测结果。对于第二和第三数据集，小浓度比表明该模型解决了SVR算法的大样本学习问题。此外，准确性和平均CPU训练时间是可以接受的，这表明了我们提出的算法的适用性。
从以上结果可以得出几点意见。首先，对于不同的训练样本大小，新SVR模型比标准SVR模型有更好的预测能力。其次，针对m的不同初始值，（OTS）在所提出的模型中是收敛性最优训练子集。第三，由OTS-SVR获得的OTS的大小明显小于全训练集的大小，并且基于全训练集的标准SVR在中等或大样本大小的情况下需要更多的时间来学习和收敛，基于OTS的新SVR。最后，为了提前2天进行大样本预测，我们简单地设定了一个相对较大的值λ，并选择与其他参数的先前实验相同的值。如表3所示，训练和测试集评估是可接受的，所以所提出的方法在对参数值进行粗略调整的情况下是稳健和有效的。该算法基于近似凸性优化框架，提出了一种新的最优训练子集选择技术。此外，该算法还包括一个由OTS和SVR预测引擎组成的新的最优预测机制。由于OTS-SVR方法可以通过计算OTS来降低学习复杂度，因此可以预期这些结果。总体而言，OTS-SVR方法为预测电力负载提供了一个非常强大的易于实施的工具。所有模型都使用MATLAB6.5软件[31]。所有的案例都在一台配备1 GB RAM和2.01 GHz处理器的个人电脑上运行。
## 5 结论

在SVR的学习过程中，所有训练对都被统一处理，然而，在许多现实世界的情况下，训练对的影响是不同的。特别地，过度拟合是由于训练系统中一类输入的压倒性冗余训练样本部分地消除了对不同类别的小训练样本的学习效应[32]。像软计算中的其他工具一样，丢弃冗余信息的失败会影响SVR的预测准确性，计算效率和学习收敛性。这种现象比较严重，因为训练集噪音很高。
基于上述原因，我们提出了一种新的计算最优训练子集的优化框架。该框架固有地具有能够解决SVR模型遭受的存储器复杂性问题O（N2）的集中。我们在本文中的贡献有两方面，一方面是OTS的近似凸性优化框架的规范，另一方面是构建求解OTS的收敛计算方案。尽管我们在本研究中没有提供完整性理论来证明我们的凸性优化框架，但我们已经建立了一个计算框架，为我们提出的解决方案的优点提供了一些经验证据。正如我们的图表所示，我们的初步结果指出了我们提出的算法的有效性。为了提取表示全训练集最大信息的最优训练子集，应用新的K-OTS方法和凸性迭代策略探索最优训练子集，并通过经验证明了凸性的性质。但是，可以说模型构建和参数设置还有很多工作要做。
## 致谢

我们感谢编辑和匿名审稿人提供有用的意见和建议。
## References
[1] J.T. Bernard, D. Bolduc, N.D. Yameogo, S. Rahman, A pseudo-panel data model of household electricity demand, Resource and Energy Economics 33 (2010) 315–325.<br>
[2] F.H. Tay, L.J. Cao, Application of support vector machines in financial time series forecasting, Omega 29 (4) (2001) 309–317.
[3] K.J. Kim, Financial time series forecasting using support vector machines, Neurocomputing 55 (1–2) (2003) 307–319. <br>
[4] M. Zhang, L. Fu, Unbiased least squares support vector machine with polynomial kernel, in: 8th IEEE International Conference on Signal Processing (ICSP-2006), vol. 3, Guilin, China, 2006, pp. 16–20. <br>
[5] S. Osowski, K. Garanty, Forecasting of the daily meteorological pollution using wavelets and support vector machine, Engineering Applications of Articial Intelligence 20 (6) (2007) 745–755. <br>
[6] T.W. Quan, X.M. Liu, Q. Liu, Weighted least squares support vector machine local region method for nonlinear time series prediction, Applied Soft Computing 10 (2) (2010) 562–566. <br>
[7] P.F. Pai, W.C. Hong, Forecasting regional electricity load based on recurrent support vector machines with genetic algorithms, Electric Power Systems Research 74 (3) (2005) 417–425. <br>
[8] Y. Zhan, H.Z. Cheng, A robust support vector algorithm for harmonic and interharmonic analysis of electric power system, Electric Power Systems Research 73 (3) (2005) 393–400. <br>
[9] A. Chaudhuri, K. De, Fuzzy support vector machine for bankruptcy prediction, Applied Soft Computing 11 (2) (2011) 2472–2486.  <br>
[10] H.T. Pao, Forecasting energy consumption in Taiwan using hybrid nonlinear models, Energy 34 (10) (2009) 1438–1446. <br>
[11] J.Z. Wang, W.J. Zhu, W.Y. Zhang, D.H. Sun, A trend fixed on firstly and seasonal adjustment model combined with the e-SVR for short-term forecasting of electricity demand, Energy Policy 37 (2009) 4901–4909. <br>
[12] L.Y. Chuang, C.H. Yang, J.C. Li, Chaotic maps based on binary particle swarm optimization for feature selection, Applied Soft Computing 11 (2009) 239–248. <br>
[13] S.P. Moustakidis, J.B. Theocharis, SVM-FuzCoC. A novel SVM-based feature selection method using a fuzzy complementary criterion, Pattern Recognition 43 (11) (2010) 3712–3729. <br>
[14] W.Z. Yang, D.L. Li, L. Zhu, An improved genetic algorithm for optimal feature subset selection from multi-character feature set, Expert Systems with Applications 38 (3) (2011) 2733–2740. <br>
[15] T.M. Hamdani, J.M. Won, A.M. Alimi, F. Karray, Hierarchical genetic algorithm with new evaluation function and bi-coded representation for the selection of features considering their confidence rate, Applied Soft Computing 11 (2) (2011) 2501–2509. <br>
[16] M. Yang, P. Yang, A novel approach to improving C-Tree for feature selection, Applied Soft Computing 11 (2) (2011) 1924–1931. <br>
[17] T. Warren Liao, Diagnosis of bladder cancers with small sample size via feature selection, Expert Systems with Applications 38 (4) (2011) 4649–4654. <br>
[18] F. Takens, Detecting strange attractors in turbulence, Dynamical Systems 11 (1981) 366–381. <br>
[19] L.B. Yann-Aël, S. Silvia, B. Gianluca, Adaptive model selection for time series prediction in wireless sensor networks, Signal Process 12 (87) (2007) 3010– 3020. <br>
[20] H.M. Liu, H.Q. Wang, X. Li, A study on data normalization for target recognition based on RPROP algorithm, Modern Radar 31 (5) (2009) 55–60. <br>
[21] B.E. Boser, I.M. Guyon, V.N. Vapnik, A training algorithm for optimal margin classifiers, in: ACMCOLT’92, Pittsburgh, PA, 1992, pp. 144–152. <br>
[22] A.J. Smola, B. Scholkopf, A tutorial on support vector regression Statistics and Computing, vol. 14, Kluwer Academic Pub., 2004, pp. 199–222. <br>
[23] C.J.C. Burges, A tutorial on support vector machines for pattern recognition, Journal of Database Management 2 (1998) 121–167. <br>
[24] D.N. Zheng, J.X. Wang, Y.N. Zhao, Non-flat function estimation with a multi-scale support vector regression, Neurocomputing 70 (1–3) (2006) 420–429. <br>
[25] N. Cristianini, J. Shawe-Taylor, An Introduction to Support Vector Machines and Other Kernel-based Learning Methods, Cambridge University Press, New York, NY, 1999. <br>
[26] Y.P. Zhao, J.G. Sun, Robust support vector regression in the primal, Neural Networks 21 (10) (2008) 1548–1555. <br>
[27] V. Vapnik, The Nature of Statistical Learning Theory, Springer, NY, 1995. <br>
[28] M. Aizerman, E. Braverman, L. Rozonoer, Theoretical foundations of the potential function method in pattern recognition learning, Automation and Remote Control 25 (1964) 821–837. <br>
[29] K. Sayre, J.H. Poore, Stopping criteria for statistical testing, Information and Software Technology 42 (12) (2000) 851–857. <br>
[30] J.W. Li, Z.H. Cai, A novel automatic parameters optimization approach based on differential evolution for support vector regression, Lecture Notes in Computer Science 5370 (2008) 510–519. <br>
[31] About MATLAB [Online]. Available from: http://www.mathworks.com/. <br>
[32] D.F. Li, W.C. Hu, W. Xiong, J.B. Yang, Fuzzy relevance vector machine for learning from unbalanced data and noise, Pattern Recognition Letters 29 (2008) 1175–1181. <br>





