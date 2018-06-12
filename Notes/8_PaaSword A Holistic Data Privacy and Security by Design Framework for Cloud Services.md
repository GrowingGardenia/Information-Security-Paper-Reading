# PaaSword: A Holistic Data Privacy and Security by Design Framework for Cloud Services
# PasSword：云服务设计框架提供的整体数据隐私和安全性

Yiannis Verginadis1, Antonis Michalas2, Panagiotis Gouvas3, Gunther Schiefer4, Gerald H¨ubsch5,Iraklis Paraskakis6 <br>
1 Institute of Communications and Computer Systems, National Technical University of Athens, Athens, Greece <br>
2 Security Lab, Swedish Institute of Computer Science, Stockholm, Sweden <br>
3 Ubitech Ltd., Athens, Greece <br>
4 Karlsruhe Institute of Technology, Karlsruhe, Germany <br>
5 CAS Software AG, Karlsruhe, Germany <br>
6 South East European Research Centre, Thessaloniki, Greece <br>
jverg@mail.ntua.gr, antonis@sics.se, pgouvas@ubitech.eu, gunther.schiefer@kit.edu, gerald.huebsch@cas.de,iparaskakis@seerc.org <br>

## 关键词：
数据隐私，设计安全，情境感知安全，对称可搜索加密，云计算
## 摘要：
采用云计算的组织进行有价值的转型，无疑伴随着一系列需要考虑的安全威胁。在本文中，我们概述了迁移到云环境时出现的重大安全挑战，并提出PaaSword--一种新颖的整体数据隐私和安全性设计框架，旨在缓解这些挑战。 设想的框架旨在最大化和加强个人，专业和企业用户对云服务的信任。 具体而言，PaaSword涉及态势感知安全模型，必要的策略实施和治理机制以及物理分发，加密和查询中间件，旨在促进实施安全和透明的基于云的应用程序。

## 1 引言
   直到最近，大规模计算还是专门针对拥有丰富内部专业知识的大型组织。云计算已经改变了这一点，即任何拥有基本技术技能的用户都可以以低成本获得大量计算资源。在技术采用生命周期中，云计算现在已经逐渐成为大规模使用的早期阶段，我们通常会看到指数级的部署。在过去几年中，许多用户开始依赖云服务而没有意识到这一点。主要的网络邮件提供商利用云技术;平板电脑和智能手机通常会默认自动将用户照片上传到云存储和社交网络;最后，一些著名的CRM厂商使用云提供他们的服务。换句话说，云计算的采用已经从专注的兴趣转向广泛传播的大量实验，并且正在迅速普及近乎无处不在的应用前景。

   企业越来越认识到云计算的经济和操作效益。将IT资源虚拟化并集中到云中，可以使组织实现显著的成本节约，并加快新应用程序的部署，同时以前所未有的速度改变企业和政府。然而，如果不解决云计算带来的新的数据安全挑战，这些宝贵的业务优势就无法实现。
    
尽管云计算带来了好处，但出于安全考虑，许多公司仍保持谨慎。应用程序和存储卷通常位于潜在的恶意虚拟环境的旁边，使敏感信息面临被窃取、未经授权的暴露或恶意操纵的风险。政府对数据隐私和位置的监管带来了另一个重大的法律和财务后果，如果违反数据保密规定，或者云提供商将监管数据移到国境，则会引发额外的法律和财务后果。这份文件的贡献有两点。首先，我们给出了在迁移到云环境时必须考虑的核心安全需求和挑战列表。这些安全需求基于我们将现有应用程序迁移到私有基础设施即服务(IaaS)云(Michalas et al.， 2014)的经验。我们通过讨论云环境的重要攻击向量特征来扩展本指南，这将为构建云服务时提供更严格的安全性铺平道路。其次，为了应对关键的云安全挑战，我们提出了PaaSword，这是一个设想中的框架，将最大化并增强个人、专业和企业用户对云服务和应用程序的信任。PaaSword通过提供存储保护机制来实现这一点，该机制在不影响数据访问功能的同时，提高了用户数据在云中的保密性和完整性保护。

本文的其余部分组织如下。在第2部分中，我们进一步阐述了云服务和应用程序中的主要数据安全挑战。在第3部分中，我们通过设计引入了一个整体的、数据隐私和安全，通过复杂的上下文感知访问模型增强了框架，并引入了健壮的策略实施和治理机制，旨在促进安全透明的基于云的应用程序的实现。在第4节中，我们简要地讨论了相关工作，在第5节中，我们通过提出实施和评估框架建议的下一步步骤来结束本文。

## 2 云端数据安全挑战
根据云安全联盟（Alliance Security，2013），几种最高级别的安全威胁指的是信息泄露和否认，通过数据保护，隐私，保密性和完整性将数据安全性视为首要任务。更确切地说，确定的四大威胁包括：数据泄漏，数据丢失，帐户劫持和不安全的API。外包的外部化方面可能会使维护数据完整性和隐私性变得更加困难（IBM，2011），组织应该包括缓解虚拟化带来的安全风险的机制。尤其是当他们处理诸如健康记录等敏感数据时，保护存储信息成为首要任务。因此，数据安全可以被看作是向云体系结构的整个过渡应该基于的基础。为了确保组织的安全，必须解决用户记录的多重风险。最重要的方面之一是敏感信息的安全性。为此，部署必须确保所有敏感数据以加密形式存储。作为补充，正确的密钥管理必须确保加密密钥不会泄露给恶意用户。基于此，很明显现代云应用程序的最关键部分是数据持久层和数据库本身。由于所有敏感信息（包括用户凭证，信用卡信息，个人数据，公司数据等）均存储在这些架构部分中，因此数据库转移是每个对手的最终目标。Open Web Application Security Project基金会将数据库相关的攻击（SQL注入）归类为最关键的攻击。

各个事件报告也反映了这种攻击媒介的重要性。根据Web黑客事件数据库，SQL注入占所有安全漏洞的17％。从2005年到2011年，这些注入占窃取总记录数的83％，成功破解了与黑客相关的数据泄露事件。因此，持久层的关键是显而易见的。大多数在企业环境中配置的安全栅栏旨在强化所谓的网络边界（例如路由器，主机和虚拟机）。尽管现有的入侵检测系统（IDS）和入侵防御系统（IPS）试图应对数据库接管安全问题（如Snort），但一方面，自动化的开发工具（如SQLMap）已广泛普及，另一方面，IPS和IDS规避技术变得非常复杂，表明数据库的妥协风险比以往任何时候都要大。此外，通过使用依赖Web应用防火墙（WAF）的机制，组织可以防止各种类型的攻击，但它不足以防止今天复杂的SQL注入和DoS攻击。此外，内部对手在云供应商方面甚至是软件平台和安全组件的未知虚拟能力已经广泛应用于基于云的开发中，从而为敏感数据提供了敏感数据。最近的一个例子是Heartbleed flaw3，它在OpenSSL密码库中构成了严重的错误，两年以来一直未被注意到，并且影响了全球60％以上的Web服务器。此外，关于后期开发阶段，在采用对称加密算法来保护应用程序数据的情况下，情况更糟。利用GPU处理能力的已经可用的破解工具包（例如oclHashcat）能够使用强力技术破解密码，每秒的攻击速率为1620亿次。  

尽管大多数攻击媒介由于系统管理员的错误配置而暴露在任何“软件即服务”应用程序中，但数据库接管和所收集数据的后期利用完全由应用程序开发人员负责。应用程序开发人员是负责处理所有可用作存储向量的HTTP输入参数的负责人，并且确保在现有暴力破解和反向技术下，受损数据无效。尽管如此，即使应用程序开发人员遵循严格的指导原则，仅仅使用IaaS提供程序来托管虚拟机，或者为了开发云应用程序而使用平台即服务（PaaS）提供程序，也可以自行产生许多固有的漏洞。这些漏洞通常不能有效解决，因为它们通常超出了应用程序开发人员的责任。

## 3 可预见的框架

在本节中，我们将介绍PaaSword，这是一个允许云服务维护完全分布式和加密数据持久层的框架，以便在存在恶意对手时促进数据保护，完整性和保密性。为此，我们描述了一个可以作为细粒度访问控制方案基础的基于情境的安全模型，它允许每个用户管理访问权限。除此之外，我们还描述了物理分布，加密和查询中间件，它们都是基于可变数据加密（SE）方案，这将允许合法用户直接搜索加密数据，从而确保存储数据的保密性和完整性。

### 3.1上下文感知访问模型

 我们设想一个基于XACML的情景感知访问模型，开发人员需要它来注释他们应用程序的数据访问对象。这种情景模型应该概念化在选择数据访问策略期间必须考虑的方面。这些方面可能是机器可解析的任何类型的信息;说明他们可能包括用户的IP地址和位置，为了与应用程序交互以及在公司中的位置而使用的设备类型。这些方面可以在安全策略执行过程中以不同的方式进行解释。特别地，情境感知访问模型确定哪些数据在已经认证的用户的哪些情况下可以访问。访问控制模型负责决定是否对特定对象执行某种操作。对象可以是服务器，应用程序，整个数据库，甚至可以是表格行中的单个字段。用户被视为活动元素并被称为主题。权限将对象与操作（例如读取，写入）关联起来。访问控制模型提供了每个主题对特定对象的权限列表。常用的访问控制模型是强制访问控制（MAC），自主访问控制（DAC）和基于角色的访问控制（RBAC）（法拉利，2010）。在我们的方法中，授予/拒绝访问的过程将基于动态变化的参数，因此我们提出的模型依赖于具有组的DAC模型。上下文参数在单用户之前是独一无二的，在授予访问权限时，必须考虑与单个用户相关的所有信息。此外，RBAC模型是不适合的，因为每改变一次对象的参数对象，每个对象都必须改变。为了在静态访问控制模型中实现上下文参数的动态变化，我们将使用所谓的上下文切换。根据当前上下文，可以授予或拒绝（切换）权限。这可以随着上下文的每次改变而动态切换。上下文切换负责管理操作权限和对象权限。操作权限赋予主体执行特定操作的权利，而对象权限则赋予对特定对象执行操作的权利。
 
### 3.2策略访问和执行

我们提出的框架的另一个重要方面是中间件，它将封装维护访问策略模型，注释和管理数据访问对象注释，控制其有效性，将其动态解释为策略执行规则并执行它们的功能。这个设想的中间件将提供：
（a）透明密钥，用于身份验证目的，与验证传入访问请求的来源有关; 
（b）以工具形式的注释能力（也可以涉及IDE插件），以允许开发人员以声明方式创建安全执行所需的最小规则集; 
（c）将数据访问对象注释动态解释为策略执行规则; 
（d）注释的治理和质量控制及其各自的政策规则; 
（e）制定和实施总体政策执行业务逻辑。

就这个中间件而言，我们也考虑重用和适当扩展技术来发展合适的关键管理机制。这种机制对于涉及数据加密和解密的不同方面的认证是必要的。我们旨在构建对应用程序使用透明的密钥使用。这涉及到用户身份验证时的关键传播，直接涉及安全执行中间件。为了提高效率，我们将采用混合加密技术，以便利用两种不同的加密功能。内层将使用一个使用对称加密密钥K的算法进行加密，而外层将使用非对称加密来加密对称密钥K.对称加密允许更多的效率方案但隐私关注度被提高，因为参与方必须交换密钥键。但是，结合这两种技术有助于优化底层协议的效率，同时不牺牲安全性。为此，PaaSword将依靠对称和非对称加密，以便在合法用户之间安全地分发K.

此外，我们还将采用数据对象注释的治理和有效性控制的方法和机制。更具体地说，我们将着重于应用本体驱动的治理方法：
i）数据对象注释（即存储，检索，删除等）的基本管理，
ii）数据对象注释的有效性检查（例如拒绝开发人员做出的任何异议）; 
iii）数据对象注释之间的依赖关系跟踪。
该中间件的另一个关键方面是注释解释机制。这种机制将用于在应用程序运行时期间基于数据对象注释的解释动态生成访问控制策略。这种机制将实现访问决策与使用点（即XACML规范的策略执行点（PEP））之间的基本解耦。这个解释是基于一个符合XACML的上下文模型，它可以通过安全即服务层来增强任何PaaS提供商提供的功能。为此，我们将使用OASIS XACML，因为它支持并鼓励将访问决策与使用点分开。

![8-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/edit/master/picture/8_1.png)

图1：XACML组件的高级视图

### 3.3威胁模型，安全存储和查询中间件

在本小节中，我们提供了有关保护存储数据免受恶意对手攻击的协议的高级描述。为此，我们首先描述一个云应用将被视为安全的威胁模型。

#### 威胁模型：

与该地区现有的工作类似（Paladi等，2014; Santos等，2009），我们假设一个半诚实的云提供商。在最不诚实的敌对模式中，恶意云提供商正确地遵循协议规范。但是，她可以拦截所有消息，并可能尝试使用它们以获取本应保持私密的信息。半诚实的攻击者也被称为诚实但很好奇。此外，对于协议中的其他参与者，我们与基于Dolev-Yao对抗模型（Dolev和Yao，1983）的（Santos et al。，2009）共享威胁模型，并进一步假设特权访问权限可以被远程攻击者ADV用来泄漏保密信息。攻击者，例如一个损坏的系统管理员可以获得对提供商维护的任何主机的远程访问。但是，攻击者无法访问驻留在提供程序计算主机上的任何来宾虚拟机（VM）的易失性内存。如以下所述，此属性基于访客虚拟机的闭包执行环境Terra（Garfi nkel等人，2003）和（Zhang等人，2011）进一步发展。

#### 安全存储：

PaaSword的基本原则是存储在不受信任的服务器上的敏感数据必须始终加密。这有效地降低了隐私和安全风险，因为它依赖于底层密码系统的语义安全性，使系统相对免受内部和外部攻击。考虑到这一点，我们提出了一个基于类似于（Kamara and Lauter，2010）中提出的对称可搜索加密（SSE）方案的加密云存储的前瞻性设计。我们计划扩展先前的工作Cumulus4j（Huber等，2013）和MimoSecco（Gabel和Hüubsch，2014），其中提出了SSE方案，并基于INDICP安全性概念（Büoschet al，2014），它隐藏了不同数据的不同数据之间的关系，为安全的数据库外包创造了基础。 SSE方案允许用户搜索加密的数据，而无需了解有关明文数据的任何信息。假设DB = {m1，...，mn}是一组n个消息（w.l.o.g DB可以被认为是一个数据库）。对于每个mi∈DB，我们提取一组关键字，稍后可用于执行查询。这组关键字记为W = {w1，...，wn}。对于每个w∈W我们计算H（wi），其中H（·）是密钥K0下的密码安全散列函数。然后，我们用密钥K‘’ = K‘加密DB的元素。通过这样做，我们创建了一个可搜索的加密索引I，其中每个索引条目指向具有特定关键字的加密行列表。客户端可以使用陷门功能来搜索索引并确定索引中是否包含特定关键字。虽然上述计划在以前的工作中得到实施（Huber等，2013; Gabel和Hüubsch，2014），但我们倾向于在我们提出的框架中加以限制。更确切地说，目前的方案采用单一写/单读（S / S）架构，这对我们的云场景来说是不切实际的。为了克服这个限制，我们计划构建一个支持多写/多读（M / M）的SSE，这意味着一组基于访问权的用户将能够读写加密数据。为此，PaaSword将涉及采用分布式算法将灵活的S / S体系结构转换为M / M。此外，还将实施用户撤销功能，以排除恶意行为或不再具有访问权限的用户。如果我们认为许多现有的SSE计划（Büosch等，2014）不支持用户撤销并因此容易受到许多攻击，这是一个至关重要和具有挑战性的过程。

#### 查询中间件：

为了成功地支持上述SSE方案，我们的目标是开发一个称为虚拟数据库VB（图2）的持久层，它将成为在客户端数据上传到云之前保护客户端数据的中介。此外，此图层将负责处理用户查询。在我们的框架中，VB扮演着一个值得信赖的第三方的角色。例如，考虑用户想要在PaaSword安全数据库中搜索特定数据的情况。要做到这一点，她会生成一个查询（q），其中包含许多关键词，这些关键字对于VB来说很有兴趣并且很有必要。接收后，VB从q中提取关键字，计算它们的散列值并查询存储关键字wi的数据库。如果查询成功并且关键字存在于其中一个表中，则VB将从包含加密的原始数据的主表中删除它。接收后，VB将通过发送获取的数据来回复用户的请求。

### 3.4概念架构

将要开发的符合PaaSword的云应用程序将继承完全物理分布式和完全加密的数据持久层，该层将能够在临时基础上确定传入数据查询和处理请求是否应该被授权访问目标数据在应用程序运行时使用PaaSword框架的传统应用程序的转换过程以及转换后的应用程序安全并保护用户的敏感数据如图2所示，同时也揭示了框架的高层体系结构细节。在此框架中，我们考虑采用模型-视图-控制器（MVC）开发模式的应用程序（Krasner和Pope，1988）。如图2（步骤1）所示，应用程序开发人员在其最喜欢的集成开发环境（IDE）中导入现有的或创建一个新的基于MVC的应用程序，IDE将为其提供IDE专用插件。在此过程的第二步中，应用程序开发人员根据每个数据对象的物理分布，加密和访问权限方案，根据基于XACML的模式和访问权限方案，在控制器的DAO处创建注释，以引用应该受保护的敏感数据。在第三步中，DAO注释将被检查以确保其数据的安全性并与全部应用程序代码进行编译。这将允许使用基于XACML的DAO批注进行应用程序控制器的转换，从而实现PaaSword安全应用程序。在第四步中，应用程序的持久层将根据合并的DAO注释在模式和实例级别进行物理分布和加密，强加VB的模式和驱动查询处理能力，以增强实际数据持久层的应用。在应用程序运行时（步骤5），增强型控制器将最终用户的每个查询和处理请求转发到负责数据库代理查询合成和合成的查询处理机制。在步骤6中，在将增强查询提交给VB之前，查询处理机制咨询策略执行机制以确定是否应该允许传入请求。当按照强制和访问许可时，查询处理机制将增强查询提交（步骤7）到增强持久层（虚拟数据库）。知道实际应用数据库的物理分布方案的数据库代理实际上分布实际应用数据库的物理分布的加密部分（步骤8）。接下来，发生来自数据库的分布式部分的相应加密数据的联合（步骤9）。使用对应用程序透明的最终用户密钥的联合数据合成和特别解密传播到查询处理机制（步骤10）。最后，查询处理机制将解密的数据传递给应用程序控制器，应用程序控制器通过应用程序的“视图”组件将它们转发给最终用户。

根据概念图（图2），每个最终用户都配备了一个硬件安全模块，例如USB棒或带有数字权限管理模块的智能手机，其中包含数字证书（例如X.509）。部分认证包括可由PaaS / IaaS提供商出口的密钥。这些端口和端口将被转交给查询中间件，后者将负责与VB进行交互，对目标数据进行加密和解密。

## 4 相关工作

为了加强远程服务访问的安全性，研究人员引入了位置感知访问控制（LAAC）的概念，该系统允许系统根据用户的物理位置授予或拒绝访问用户。 LAAC模型通常扩展了三个基本访问控制模型DAC，MAC和RBAC（Decker，2011）。尽管LAAC协议已被广泛研究（Cleeff et al。，2010），但明显缺乏确定用户访问权限的方案，这些方案不仅基于用户的物理位置和凭证，而且还包含最新的相关上下文信息。该报告是第一个引入情境感知访问控制（CAAC）的概念，由智能家庭的应用程序驱动。更确切地说，作者介绍了一组基于对象或主题位置的服务。所提出的模型的主要缺点是它不支持动态生成的上下文，而它却失败了，以至于无法支持多位置的多重性要求。其他现有的CAAC模型主要基于RBAC（Kayes et al。，2013），并且通常针对特定领域（Costabello等，2012）。然而，这些模型并没有被设计为提供细粒度的数据访问控制，例如通过提供为数据库的不同行指定不同访问规则的能力。关于政策管理，最近对当代开放源码注册管理机构和知识库系统方法的调查显示（Kourtesis和Paraskakis，2012），主要缺点是缺乏恰当的问题分离。政策定义和政策执行纠缠在一个单一软件组件 - 策略检查器的实施中。最后的行为准则通常以一种命令式的方式进行编码，这种方式是检查潜在的政策违规行为的代码。这有一些负面影响，其中包括可携带性和政策关系缺乏明确表示。

数据分发和加密算法也是可信云服务和应用的重要方面。在（Gentry，2009）中，C.Gentry提出了第一个完全同态加密方案，它使语义上安全扩展到云中。云提供商盲目运行加密数据并产生正确的加密结果。尽管如此，它的实用性仍然存在问题，因为最新的实现比下载所有加密数据的速度还要慢，在本地解密，处理和加密，最后再次上传。在另一个有趣的方法（Popa et al。，2011）中，使用了洋葱的概念。洋葱由单一的过氧化物质处理，充当用户和存储后端之间的适配器。关系表中的每个属性都是不对称加密的。如果发出某属性的某种查询，则将洋葱层剥离，导致另一种不太安全的洋葱。 CryptDB使用一种新颖的保留加密顺序的方案，除了顺序之外不泄漏任何有关数据的信息，因此可以安全地对加密数据进行排序。 CryptDB的主要缺点是缺乏客户端的安全保证。更确切地说，唯一的保证是不可信的服务器只会学习那些必要的信息。在最坏的情况下，这可能会导致每个属性都被简化为纯文本。此外，剥离层不能颠倒，因此单个查询足以永久降低安全性。

![8-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/edit/master/picture/8_2.png)

图2：PaaSword框架概念架构

## 5 结论
在这篇文章中，我们提出了PaaSword框架，它可以作为PaaS级别的服务公开。该框架可以解决已识别的云安全需求和挑战，以便在存在恶意对手时增强数据保护，完整性和保密性。设想的PaaSword超越了最先进的技术，并允许云服务可维护地分配对数据持久层进行加密。我们的框架包含一个contextaware安全模型，必要的策略实施机制以及物理分布，加密和查询中间件。未来的工作涉及设计和实施建议的框架，以确保功能完善的解决方案，这将通过以下五位飞行员在各种工业环境中验证：i）加密持久性作为PaaS供应商的服务，ii）政府间安全文档和个人数据交换，iii）安全传感器数据融合和分析，iv）保护多租户CRM中的个人数据，v）保护多租户ERP中的不可见企业信息。这些案例将允许我们测试PaaSword并验证其在各种异构情况下的附加价值。最后，从PaaSword框架中受益的一个领域就是所谓的参与式传感。这一领域的进展是由于将传感器引入移动设备。这些系统的开放性和用户数据的丰富性对其存储和处理提出了重要的关注。通过拥有PaaSword框架的协议设计人员将能够整合安全的云计算技术，以便于存储和处理大量收集的数据。

## 致谢
导致这些结果的研究得到了欧盟地平线2020研究和创新计划的资助，该计划根据ICT计划ICT07-2014：高级云基础设施和服务中的PaaSword项目（www.paasword.eu）的拨款协议No 644814提供。

## REFERENCES
[1]	Alliance, C. S. (2013). The notorious nine – cloud computingtop threats in 2013.<br>
[2]	B¨osch, C., Hartel, P., Jonker, W., and Peter, A. (2014).A survey of provably secure searchable encryption.ACM Comput. Surv., 47(2):18:1–18:51.<br>
[3]	Cleeff, A. v., Pieters, W., and Wieringa, R. (2010). Benefits of location-based access control: A literature study. In Proceedings of the 2010 IEEE/ACM Int’L Conference on Green Computing and Communications & Int’L Conference on Cyber, Physical and Social Computing, GREENCOM-CPSCOM ’10, pages 739–746, Washington, DC, USA. IEEE Computer Society.<br>
[4]	Costabello, L., Villata, S., and Gandon, F. (2012). Contextaware access control for rdf graph stores. In Raedt, L. D., Bessire, C., Dubois, D., Doherty, P., Frasconi, P., Heintz, F., and Lucas, P. J. F., editors, ECAI, volume 242 of Frontiers in Artificial Intelligence and Applications, pages 282–287. IOS Press.<br>
[5]	Covington, M. J., Long, W., Srinivasan, S., Dev, A. K., Ahamad, M., and Abowd, G. D. (2001). Securing context-aware applications using environment roles. In Proceedings of the Sixth ACM Symposium on Access Control Models and Technologies, SACMAT ’01, pages 10–20, New York, NY, USA. ACM. <br>
[6]	Decker, M. (2011). Modelling of location-aware access control rules. In Handbook of Research on Mobility and Computing: Evolving Technologies and Ubiquitous Impacts, pages 912–929. IGI Global.<br>
[7]	Dey, A. K. (2001). Understanding and using context. Personal Ubiquitous Comput., 5(1):4–7.<br>
[8]	Dolev, D. and Yao, A. C. (1983). On the security of public key protocols. Information Theory, IEEE Transactions,29(2):198–208.
[9]	Ferrari, E. (2010). Access Control in Data ManagementmSystems. Morgan and Claypool Publishers.<br>
[10]	Gabel, M. and H¨ubsch, G. (2014). Secure database outsourcing to the cloud using the mimosecco middleware. In Krcmar, H., Reussner, R., and Rumpe, B., editors, Trusted Cloud Computing, pages 187–202. Springer International Publishing.<br>
[11]	Garfinkel, T., Pfaff, B., Chow, J., Rosenblum, M., and Boneh, D. (2003). Terra: A virtual machine-based platform for trusted computing. In ACM SIGOPS Operating Systems Review, volume 37, pages 193–206.<br>
[12]	Gentry, C. (2009). A Fully Homomorphic Encryption Scheme. PhD thesis, Stanford, CA, USA. AAI3382729.<br>
[13]	Huber, M., Gabel, M., Schulze, M., and Bieber, A. (2013). Cumulus4j: A provably secure database abstraction layer. In Cuzzocrea, A., Kittl, C., Simos, D. E., Weippl, E., Xu, L., Cuzzocrea, A., Kittl, C., Simos, D. E., Weippl, E., and Xu, L., editors, CD-ARES Workshops, volume 8128 of Lecture Notes in Computer Science, pages 180–193. Springer. <br>
[14]	IBM (2011). Security and high availability in cloud computing environments. Technical report, IBM SmartCloud Enterprise, East Lansing, Michigan. <br>
[15]	Kamara, S. and Lauter, K. (2010). Cryptographic cloud storage. In Sion, R., Curtmola, R., Dietrich, S., Kiayias, A., Miret, J., Sako, K., and Seb, F., editors, Financial Cryptography and Data Security, volume 6054 of Lecture Notes in Computer Science, pages 136–149. Springer Berlin Heidelberg.<br>
[16]	Kayes, A. S. M., Han, J., and Colman, A. (2013). An ontology-based approach to context-aware access control for software services. In Lin, X., Manolopoulos, Y., Srivastava, D., and Huang, G., editors, WISE (1), volume 8180 of Lecture Notes in Computer Science, pages 410–420. Springer.<br>
[17]	Kourtesis, D. and Paraskakis, I. (2012). A registry and repository system supporting cloud application platform governance. In Proceedings of the 2011 International Conference on Service-Oriented Computing, ICSOC’11, pages 255–256, Berlin, Heidelberg. Springer-Verlag.<br>
[18]	Krasner, G. E. and Pope, S. T. (1988). A cookbook for using the model-view controller user interface paradigm in smalltalk-80. J. Object Oriented Program., 1(3):26– 49.<br>
[19]	Michalas, A. and Komninos, N. (2014). The lord of the sense: A privacy preserving reputation system for participatory sensing applications. In Computers and Communication (ISCC), 2014 IEEE Symposium, pages 1–6. IEEE.<br>
[20]	Michalas, A., Komninos, N., Prasad, N. R., and Oleshchuk, V. A. (2010). New client puzzle approach for dos resistance in ad hoc networks. In Information Theory and Information Security (ICITIS), 2010 IEEE International Conference, pages 568–573. IEEE.<br>
[21]	Michalas, A., Paladi, N., and Gehrmann, C. (2014). Security aspects of e-health systems migration to the cloud. In e-Health Networking, Applications and Services (Healthcom), 2014 IEEE 16th International Conference on, pages 212–218. IEEE.<br>
[22]	Micro, T. (2010). The need for cloud computing security. In A Trend Micro White Paper. <br>
[23]	Paladi, N. and Michalas, A. (2014). “One of our hosts in another country”: Challenges of data geolocation in cloud storage. InWireless Communications, Vehicular Technology, Information Theory and Aerospace Electronic Systems (VITAE), 2014 4th International Conference on, pages 1–6.<br>
[24]	Paladi, N., Michalas, A., and Gehrmann, C. (2014). Domain based storage protection with secure access control for the cloud. In Proceedings of the 2014 International Workshop on Security in Cloud Computing, ASIACCS ’14, New York, NY, USA. ACM.<br>
[25]	Popa, R. A., Redfield, C. M. S., Zeldovich, N., and Balakrishnan, H. (2011). Cryptdb: Protecting confidentiality with encrypted query processing. In Proceedings of the Twenty-Third ACM Symposium on Operating Systems Principles, SOSP ’11, pages 85–100, New York, NY, USA. ACM.<br>
[26]	Santos, N., Gummadi, K. P., and Rodrigues, R. (2009). Towards trusted cloud computing. In Proceedings of the 2009 Conference on Hot Topics in Cloud Computing, HotCloud’09, Berkeley, CA, USA. USENIX.<br>
[27]	Zhang, F., Chen, J., Chen, H., and Zang, B. (2011). Cloudvisor: retrofitting protection of virtual machines in multi-tenant cloud with nested virtualization. In Proceedings of the Twenty-Third ACM Symposium on Operating Systems Principles, pages 203–216. ACM.<br>
