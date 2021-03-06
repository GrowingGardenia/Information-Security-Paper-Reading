# Developing Cyber Security Asset Management Framework for UK Rail
# 发展英国轨道交通的网络信息安全资产管理框架

Shruti Kohli BCRRE, University of Birmingham Birmingham, Great Britain s.kohli@bham.ac.uk

## 摘要：
在部分技术进步、有组织的犯罪中有利可图的应用以及政府支持的创新的驱动下，网络攻击的复杂性和普遍性正在不断上升。现代化的铁路控制系统导致了对数字技术持续增长的依赖和潜在的信息安全违反和攻击。这篇文章展示了发展加强轨道资产的网络安全可重复使用的可扩展的的框架的重要性。一个网络安全框架被认为是应该发展对铁路信号的网络攻击而不是工业资产的检测。这个架构将基于铁路资产情景的保护概念的发展，例如点式设备和为保证挑选过的铁路资产满足安全和信息安全特性的评估确认水平。为保证铁路资产不受网络攻击而努力。

## 关键词：铁路资产，网络安全，网络本体，防护简介，英国轨道交通，轨道交通信息安全

## 1、	介绍
轨道传输在国际、城际、和城内连接中扮演着重要的角色，需要与其他交通模式以及终端用户有着广泛而高效的信息交换。轨道交通系统的开放性以及相互联系的增长，对高效的网络安全带来了更高的要求，预防可以让安全和操作性能均下降的恶意攻击。过去，有很多在信息物理系统的的网络安全攻击事件。据报道，一个网络攻击在九月打断了以色列的网络。一个特洛伊木马程序渗透进了Carmel Tunnels高速公路的视频监控系统，导致了当天20分钟的道路关闭，以及第二天八个小时的关闭，造成了大范围的拥堵。由于对基于网页式的信息安全系统的增长，附加的威胁可能更多的依赖于Dos攻击的形式。最近有在控制系统的勒索的攻击证据。尽管这样，没有具体的证据可以表明恐怖分子、激进分子、以及有组织的犯罪者总是会成为控制系统潜在的威胁。英国铁路系统基础设施操作轨道交通网络是计划用一种数字的更高效且很快成为国际规范的ERTMS系统替代旧的、模拟的轨道信号，然而，这种转变吸引了很多关注。此举将使列车容易受到安全漏洞和网络的攻击，造成潜在的致命后果。ERTMS系统连续不断地进行连接的安全审计，定义了潜在的脆弱性候和缓解建议 [ 16 ]。下面的表[ 1 ]突出了一些过去发生的包含轨道交通攻击的网络攻击的实例【19】，
![2-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/2-1.png)
 
铁路作为一项国家关键基础设施，在面对业余攻击者、有组织犯罪、工业间谍或者不满意的雇员的攻击时是脆弱的。这些中的一个或多个都有动机持续增长的技术能力来攻击脆弱的系统，英国的铁路领导者纽约铁路认识到网络攻击造成的风险。图1展示了铁路基础设施可能遭受到网络安全威胁的多个来源。
![2-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/2-2.png)
图1 铁路资产多个来源的网络安全威胁

## 2、网络安全资产管理的发展

### 工具（CAMT）框架

国家标准技术研究所（NIST）安全框架[ 12 ]是一种工业系统确保关键的基础设施的一种流行的框架。该框架的目的是“帮助关键基础设施的所有者和使用者来定义、评估和管理网咯风险。由一个核心、一个概要文件和信息层组成。核心包含标准和很多部门和行业的最佳实践。 与工业和其他国际信息安全标准例如ISO 27001一样，这些标准被划分为分为五个功能：识别、保护、检测、响应和对抗网络物理系统的网络攻击。证明虽然它并不愚蠢，但它提供了以确保工业资产的安全的起点。
在这项研究工作中，正在探索创建网络安全资产管理框架的可能性。 目标是将网络安全标准从语法表达演变为更多语义表示。 正在开发一个网络资产管理框架，包括以下功能：
1.	进行威胁分析，以确定铁路资产易受网络攻击的脆弱点。
2.	开发可以利用运输安全领域现有工作的方法，鼓励重复使用模型并最大限度地提高工作效益。
3.	该方法具有可扩展性，可与其他领域正在开发的其他许多网络安全本体集成以应对网络物理系统上的网络攻击。 伯明翰大学BCRRE团队与西门子铁路自动化公司联合开发的现有本体工作为轨道领域提供了候选核心本体[13] [14]。 铁路核心本体的范围是基于提出的实施领域，认知交叉应用的有用性和隐含的领域知识来确定的。 图[2]代表了可以使用本体建模的铁路基础设施实例。 提议的框架包括抽象级别来封装不同的资产交互，并因此提供保护每条铁路资产的指导原则。
![2-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/2-3.png)
图2.铁路机车车辆资产的表示
CAMT的关键目标可以描述如下：
1.创建网络铁路资产的钻石模型来衡量其网络攻击的脆弱性。该模型需要创建网络态势感知以保护敏感数据，监控基本操作并保护铁路资产。
2.确定并记录定义可及性的网络安全标准，并将不同铁路利益相关者群体对铁路资产可及性的程度进行分类。这相当于创建受保护的配置文件，可以提供远程监控网络资产的特权访问权限;
3.创建可扩展和可扩展的数据量和多样性的模块化系统架构。使用RDF三重存储和OWL推理，实例数据和领域知识透明地传递到应用程序，从而保护现有应用程序免受后端数据实现的更改影响，并简化访问数据资源的新软件的开发。正在为各种铁路设备和相应的数据集开发本体。通过loT收集的传感器数据可以通过内存数据库（如REDIS）缓存高吞吐量数据并防止在本体实例上过度触发推理，从而与三重存储中的资产实例相关联[20]。
4.通过包含网络故障的失败模式类型来改进网络资产的FMEA（失效模式影响分析），以捕捉网络威胁的概念。
本文表示正在进行的研究。其中一些功能已在下面的小节中进行了描述：
### A 创建网络轨道资产的钻石模型
正在建立钻石铁路资产模型来衡量其网络攻击的脆弱性。 针对Rail Signaling，Point Machines和Railway Track等铁路资产进行漏洞分析。 由MITER研究人员开发的钻石模型[21]已经过修改，以进行网络安全的可行性研究。 图[3]代表铁路资产的钻石模型。 该模型最简单的形式描述了敌人在某些基础设施上部署对抗受害者的能力。 例如。 黑客行为主义者操纵传感器数据来扰乱影响乘客的列车服务。 正如基于钻石模型在分析之前的研究或机器可以在事件被发现和检测时填充模型顶点那样[21]。
![2-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/2-4.png)
图3.铁路资产的钻石模型
顶点= {对手，基础设施，能力，受害者}，
边= {{对手，能力}，{对手，基础设施}，{基础设施，能力}，{基础设施，受害者}，{能力，受害者}}
事件={（对手，对手可信度），（基础设施，基础设施可信度），（能力，能力可信度），（受害者，受害者可信度），（时间戳初始值，可信度初始值，（时间戳，可信度最终值），其他元功能...）
事件可以被形式化地定义为n元组，其中元组的每个元素是由独立置信度值组合的特征的知识。需要通过监测导致事件发生的条件来定量或定性计算此值。边定义了各个顶点之间存在的关系，对于识别涉及网络攻击的事件很重要。
假设主要利益相关者是铁路本身，入侵者可能是任何有意图的人。
#### 确定的任务是：
1.识别受害者资产（目标）：受害者资产是攻击面，由攻击者引导其能力的一组网络，系统，组件，子组件等组成。受害者资产通常存在于角色的内部和外部控制和可见性范围内，但仍可供敌人作为目标。
2.识别对手：一组对手可能是内部人员，外部人员，个人，团体和组织，这些人试图破坏运行控制系统。铁路工作人员中的各种人员可以有限/无限制地使用铁路资产。
3.收集元信息：在将网络攻击识别为事件时，收集时间戳，阶段，结果，方向，方法论资源等元功能以描述发生网络攻击事件很重要。
一些重要的元功能可以包含在以下类中：
a 含义：描述执行攻击的各种方法和由子类，如缓冲区溢出，握手溢出，逻辑漏洞利用，Tcp端口扫描等。它包括观察到的或潜在的攻击者战术，技术和程序的细节。
b后果：用于列出可能的攻击结果。对于可能的网络攻击，它可能会采用诸如DenialOfService，PrivilegeEscalation等值。 
c 攻击：这个类代表网络威胁攻击。
d 攻击者：这个类表示可能的未经授权访问资源的入侵者。
e 攻击模式：攻击模式是指攻击者可以使用的常用方法的描述，这可以为缓解其影响的方法提供指导。 
f 漏洞利用：这个类描述了单个漏洞的描述。 
g 攻击目标：攻击目标是针对攻击目标的系统中的漏洞。
h 时间戳：事件开始和结束时的时间戳。
#### 预期输出
•识别特定铁路资产（包括物理和网络资产）的网络威胁。
•针对不同类别的铁路资产 - 产出开发标准威胁评估流程/概况：威胁评估技术库适用于不同的铁路资产概况。
•确定一系列候选领域的最佳做法对网络威胁的反应 - 输出：收集针对确定的网络威胁的最佳实践案例研究
### B 文件安全标准
需要制定网络安全标准，以确定铁路资产对不同铁路利益相关者群体的可及性。这相当于创建受保护的配置文件，该配置文件可以提供远程监控网络资产的特权访问权限。保护配置文件可以在通用标准中定义，以表征组成通用系统框架的元素/子系统的安全性和安全性。对网络攻击的抵御能力需要对基础架构，体系结构和企业运营进行技术，程序和策略方面的改变。对于任何系统，威胁分析都始于识别主要威胁（任何可能直接导致损失的事件）;传感器不必要的触发并不是主要威胁，然而“由于某些传感器的不良作用导致培训延迟”是一个主要威胁，因为它会导致延误，财务损失和行业声誉受损。根据Buldas的说法，如果每个主要威胁不太可能发生，即对攻击者无利可图，那么系统就被理性地认为对于攻击“实际上是安全的”。网络铁路资产标准的主要内容已在下表中确定和总结。作为EPSRC资助的SKEPTICS项目[22]的一部分，该中心正在开展这一领域的流程开发工作。为简单起见，文件的细节已被省略。
![2-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/2-5.png)
Cherdantseva [9]调查并制定了信息系统各个组成部分需要遵循的安全目标指导原则。 表II和表III表示安全特征和关键实体，围绕这些实体需要开发铁路应用的保护配置文件[9]。 正在为不同资产创建网络安全文件，重点是Point机器和铁路轨道信号系统。
表III 网络标准文件的主要元素
 
### C.铁路资产的网络本体论
针对该框架提出了包含域级，设备级和安全级模型的三级铁路资产本体。为各种铁路设备和相应的数据集开发了本体[13]。通过loT收集的传感器数据可以通过内存数据库（例如REDIS [17]）与三重存储中的资产实例相关联，缓冲高吞吐量数据并防止在本体实例上引发过多的推理。这里的想法是重用现有的本体并使它们可扩展以包含网络本体层[10]。本研究论文中略去了相同的细节。
### D.改进的FMEA（失效模式影响分析）
使用FMEA技术分析失败的最常见原因以及故障趋势和相关性。据观察，FMEA和其他相关技术不包括故意失败的检查[10]。已经针对网络资产提出了改进的FMEA，其中包含一种用于捕获网络威胁概念的“网络故障”故障模式类型。安全级别本体数据可用于衡量信任因子，可能与此领域的其他现有模型结合使用。欧洲资助项目PCIPP正在进行FMEA分析[11]。这个想法是为了改进FMEA来整合由网络攻击产生的故障。本文中FMEA的细节已被省略，并将很快发布。
## 3、结论
在这项研究工作中，已经提出了一个铁路资产管理框架，强调铁路资产的保护特性生成，并展示使用本体来检测对工业资产的网络攻击的迹象。关于未来的工作，我们设想开发具有隐含安全知识的基于标准的最佳实践数据库，以确保易受攻击的铁路资产的安全。
## 致谢
大学致力于开发网络安全框架的工作正在进行中，该框架可以展示为大学管理网络安全欧洲资助项目的能力。
## 参考文献
[I] C. Pu,"A world of opportunities: CPS, lOT, and beyond", In Proceedings of the 5th ACM international conference on Distributed event-based system, 2011, July, pp. 229-230.<br>
[2] A. Cardenas, S. Amin, S. Sastry, "Research Challenges for the Security of Control Systems", In HotSec, 2008, July.<br>
[3] A. Cardenas, S. Amin, B. Sinopoli, A. Giani, A. Perrig, S.Sastry,"Challenges for securing cyber physical systems",In Workshop on future directions in cyber-physical systems security, 2009, July, p. 5.<br>
[4] Combs, M. Marcia,"lmpact of the Stuxnet Virus on Industrial Control Systems", XIII International Forummodern Information Society Formation Problems, Perspectives, Innovation Approaches,2011 ,5-1 O.<br>
[5] US Rail Attack, http://www.nextgov.com/cybersecurity/20 12/0 I/hackers-manipulatedrailway-computers-tsa-memo-says/504981<br>
[6] A. Effendi, R. Davis,"ICS and IT: Managing Cyber Security Across the Enterprise", In SPE Middle East Intelligent Oil and Gas Conference and Exhibition. Society of Petroleum Engineers,20 15 <br>
[7] Lee, Robert M., Michael J. Assante, and Tim Conway. "German Steel Mill Cyber Attack." Industrial Control Systems 30 (2014).<br>
[8] Network Rail. "Cyber Security Strategy September 2013".2013. https:l/www.networkrail.co.uklWorkArealDownloadAsseLaspx?id=3 0064788605<br>
[9] Y. Cherdantseva, J. Hilton,"A reference model of information assurance & security", In Availability, reliability and security (ares), 2013 eighth international conference on, pp. 546-555. IEEE, 2013.<br>
[10] R. Lewis, F. Fuchs, M. Pirker, C. Roberts, G. Langer,"Using ontology to integrate railway condition monitoring data", In Railway Condition Monitoring, 2006. The Institution of Engineering and Technology International Conference on (pp. 149-155). IET.<br>
[II] S. Kohli , J.M. Easton,"PCIPP: An Approach for Predictive Maintenance of Railway Assets", International<br>
[12]NlST,http://www.nist.gov/cyberframework/<br>
[13]Tutcher, J., 2014, October. Ontology-driven data integration for railway asset monitoring applications. In Big Data (Big Data), 2014
IEEE International Conference on (pp. 85-95). IEEE.<br>
[14] M. C. Morris, J. M. Easton, C. Roberts,"Ontology Domain", 7th International Joint Conference on Discovery, Knowledge Engineering, and Management,20 15 in the Rail Knowledge Knowledge<br>
[15] A. Buldas, P. Laud, 1. Priisalu, M. Saarepera,1. Willemson," Rational choice of security measures via multi-parameter attack
Trees",ln Critical Information Infrastructures Security,2006, pp. 235- 248, Springer Berlin Heidelberg<br>
[16] R. Bloomfield, I. Gashi,R. Stroud,"How secure is ERTMS?", In Computer Safety, Reliability, and security , 2008, pp. 247-258, Springer Berlin Heidelberg.<br>
[17] REDTS,https:l Iredislabs.coml<br>
[18] M. Abrams, J. Weiss,"Malicious control system cyber- security attack case study-Maroochy Water Services", Australia. McLean, VA: The MITRE Corporation,2008.<br>
[19] A. Cardenas, A. Saurabh, S. Sastry, "Secure control: Towards survivable cyber-physical systems.", In The 28th International Conference on Distributed Computing Systems Workshops, pp. 495- 500. IEEE, 2008.<br>
[20] L. Obrst,P. Chase, R. Markeloff," Developing an Ontology of the Cyber Security Domain", In STIDS, 2012, October,pp. 49-56.<br>
[21] S. Caltagirone, A. Pendergast, C. Betz,"The diamond model of intrusion analysis",Center for cyber intelligence analysis and threat research hanover md, 2013.<br>
[22] R. Evans, 1. Easton, and C. Roberts, "SCEPTICS: A Systematic Evaluation Process for Threats to Industrial Control Systems", in Press, World Congress on Railway Research, 29th May - 2nd June 2016, Milan, Italy.<br>
