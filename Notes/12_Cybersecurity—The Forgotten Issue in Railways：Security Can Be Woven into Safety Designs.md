# Cybersecurity—The Forgotten Issue in Railways：Security Can Be Woven into Safety Designs

## 作者：

1. Leonardo J. Valdivia 莱昂纳多J.瓦尔迪维亚
嵌入式系统和网络领域，Centro de Estudios e Investigaciones Tecnicas，San Sebastian，20018 Gipuzkoa，Spain  
Leonardo J. Valdivia（lvaldivia@up.edu.mx）2014年和2017年获得西班牙潘普洛纳纳瓦拉大学电信工程专业硕士学位和博士学位。在为汽车行业开发软件三年后，他于2013年加入西班牙Donostia-SanSebastián的Centro de Estudios eInvestigacionesTécnicas的嵌入式系统和网络领域。他的研究兴趣集中在安全和安全（safety and security）互动上。
2. Inigo Adin
Centro de Estudios e Investigaciones Tecnicas，San Sebastian，20018 Gipuzkoa，Spain  
IñigoAdin（iadin@ceit.es）2003年和2007年获得西班牙潘普洛纳纳瓦拉大学的硕士和博士学位。他自2003年以来一直担任西班牙Donostia-SanSebastián的Instit de Estudios eInvestigacionesTécnicas研究员，自2005年起担任纳瓦拉大学副教授。他的研究兴趣包括安全关键设计，特别关注电磁兼容性和传输互操作性。他是一项专利、两本技术书籍、一篇特邀章节，以及19篇期刊和国际会议文章的作者或合着者。
3. Saioa Arrizabalaga  
Saioa Arrizabalaga（sarrizabalaga@ceit.es）  
2003年获得西班牙毕尔巴鄂巴斯克大学工程学院电信工程硕士学位，并于2009年获得西班牙潘普洛纳纳瓦拉大学博士学位。她目前的研究兴趣包括通信协议，大数据平台和网络安全。她参与了14个项目，指导了6篇博士论文，出版了一本书，是国际期刊和会议上33篇科技论文的作者或合著者。
4. Javier Anorga
Centro de Estudios e Investigaciones Tecnicas，San Sebastian，20018 Gipuzkoa，Spain  
JavierAñorga（jabenito@ceit.es）2011年获得西班牙圣塞巴斯蒂安纳瓦拉大学工程学院电信工程硕士学位和于2015年加入纳瓦拉大学获得博士学位。他于2011年加入西班牙圣塞瓦斯蒂安市中心研究中心（CEIT）研究中心，并在CEIT-IK4数据分析和信息管理小组（TIC部门）工作 。他还是纳瓦拉大学工程学院的讲师。他的专业研究活动涉及通信协议，服务质量，体验质量，住宅网关，嵌入式系统，信息技术和网络安全。
5. Jaizki Mendizabal
Centro de Estudios e Investigaciones Tecnicas，San Sebastian，20018 Gipuzkoa，Spain  
Jaizki Mendizabal（jmendizabal@ceit.es）分别于2000年和2006年在西班牙圣塞瓦斯蒂安纳瓦拉大学工程学院获得电气工程硕士学位和博士学位。他目前是圣塞瓦斯蒂安市中心电子与通信部电子与通信部的讲师和研究员。他参与了8个研究项目，指导了两篇博士论文，是国家和国际期刊和会议上约21篇科技论文的作者或合着者，并且是由McGraw-Hill出版的GPS和Galileo双射频前端接收器设计、制作和测试的作者。

当今最关键的应用程序依赖于计算机，因此计算机故障可能导致财务灾难，严重伤害甚至死亡。在这种情况下，铁路被认为是一个关键应用，因此它们必须符合最高标准的可用性和安全性(safety)。可用性确保系统的连续运行，而安全系统必须在所有操作和环境条件下正常运行。  
但是，如果外部攻击会影响系统的可用性和/或安全性(safety)，会发生什么？在今天的铁路中，网络安全并不像安全那么重要 - 但网络安全威胁可能导致安全(safety)问题。此外，目前处理安全(security)模块开发的铁路标准只是一般性建议或仅是建议，不同于开发电子设备的铁路安全(safety)标准，这些标准既普遍又特别。本文介绍了影响铁路运输网络的当前网络威胁，提供了安全(security)标准与安全(safety)标准相比的一般分析，并介绍了一些改善网络安全的建议。

## 压倒性地关注安全
根据[1]中提供的定义，安全(safety)性被定义为“预防，检测和反应意外伤害的程度。”同一来源还将安全(security)定义为“防止，检测到恶意伤害的程度， “了解不同之处的一个有用的例子是公共办公大楼：烟雾探测器是防止意外伤害的安全(safety)装置，而旋转门和控制通道是防止恶意伤害的安全(security)装置。安全性(security)最受欢迎的组件之一是网络安全(cybersecurity)，其重点是保护网络，计算机和数据免受未经授权的访问。  
铁路和其他运输系统被认为是安全关键（safety-critical）应用，即系统，其失效可能导致这种或那种人类灾难。当应用程序或系统无法保证其所需功能时，会发生故障。虽然安全关键应用程序不一定受计算机控制，但随着应用程序复杂性的成熟，计算机在执行安全任务时变得比人类更可靠。因此，计算机越来越多地取代人类执行此类任务并不奇怪。因此，由于大多数运输系统都是基于计算机的，因此网络安全已变得至关重要。  

然而，正如其名称所暗示的那样，安全关键应用程序的重点是首先确保安全(safety)，而不是安全(security) - 这就是问题所在。是否有可能在没有安全(security)措施的情形下保证安全（safety）?安全(safety)与保障(security)能否共存？为了分析安全性和安全性(security as well as safety)的重要性，接下来的部分将描述每个主题及其当前的交互方式。
## 铁路行业的安全(safety)
在开发执行安全相关(safety-related)功能的系统时，必须遵守适用的标准。 此类标准定义了安全相关(safety-related)功能的安全完整性等级（SIL），具体取决于最大可容忍危险率。 表1显示了连续操作模式的SIL。 铁路控制系统依赖于SIL4设备，即每小时可能有10-9次故障，或者每109小时最多一次故障。
 
![12-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/12-1.png)

任何负责关键功能的系统都需要经过安全(safety)认证，如果它控制着重要的应用程序，则必须实施故障安全(fail-safe)行为。

要达到安全水平，必须遵循特定的标准。管理电子系统安全发展的标准是IEC 61508 [2]，在铁路中，它是EN 50129 [3]。这些规范规定了设计规则和测试程序，以达到特定的安全（safety）规范，这保证了系统在随机硬件故障的情况下继续满足其安全（safety）要求。 IEC 61508 [2]是实现电子和电气设备所需安全(safety)等级的通用标准。但是，EN 50129 [3]是确保应用于铁路的电子和软件设备安全的特定标准。

安全标准规定必须确定重要和非生命功能，因为必须将重要操作设计为故障安全(fail-safe)，即，如果发生故障，系统以不会造成伤害的方式作出响应。非生命职能涉及非安全行动。重要和非生命功能的一些例子如下：

■■非关键：平稳加速，实现运行速度和速度调节（通常由驾驶员控制的任务）  
■■重要：速度限制，制动系统激活（通常自动控制的任务）。  
因此，如果为铁路行业开发用于安全应用的电子设备，则必须按照标准EN 50129 [3]对其进行认证。因此，任何负责关键功能的系统都需要经过安全认证(safety certified,)，如果它控制着重要的应用程序，则必须实施故障保护行为。

## 铁路行业的安全（security）
在今天的安全标准中根本不考虑安全性(security); IEC 61508 [2]和EN 50129 [3]都没有涉及安全(security)问题。他们只提到必须考虑故意的，恶意的人类行为，并提出IEC标准62443 [4]来处理这个问题。 

IEC 62443 [4]提出了一套保护系统或组织的网络环境的技术。这些技术包括网络、软件、流程、服务和存储信息的安全性。该标准考虑了四级安全隐患，并将安全性分为四个级别（图1）。对于安全级别1（security level 1），几乎所有攻击都会对系统产生影响，但是对于安全级别4，预计只会发生灾难性攻击。
 
 ![12-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/12-2.png)
 
铁路基础设施主要基于通过有线或无线网络互连的计算机。这意味着铁路运输容易受到网络攻击。铁路基础设施分布广泛;因此，它很难保护，它是在必须处理敏感数据网络的威胁和风险之前设计的。另一个问题是每个国家都有自己的铁路基础设施。每个都有自己的规则来实现其网络，这同样适用于安全(security)策略，因此很难统一策略。为了更好地了解铁路系统目前的运作方式，我们将铁路基础设施分为五个部分。图2显示了这些部分及其相互作用，接下来我们将解释每个模块是如何开发的。
 
 ![12-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/12-3.png )
 
### 车载系统

在欧洲轨道交通管理系统（ERTMS）的情况下，车载单元控制列车的运行并通过全球移动通信系统（GSM-R）将信息发送到通信基础设施。车载系统通常实现IEEE 1473-2010 [5]中定义的配置之一。该标准定义了不同类型的网络协议：类型L（通用控制网络），类型T和类型E（因特网协议[IP]以太网网络），它被认为是最有前途的网络，因为它提供高带宽和能够将较低级别的控制网络与外部系统集成。然而，IEEE 1473-2010 [5]表示该标准“并非旨在确保安全性（safety and security）;该标准的实施者负责确定适当的安全性和安全性（safety and security）。“因此，应实施其他规范以确保两者兼顾。

### 车站系统

有管理站间运行的系统;这些任务包括控制站台门和向乘客提供信息。开发这些系统的一个标准是GB-50157-2003[6]。然而，该标准的目标是“保证地铁设计的安全性（safety）、可靠性、适应性、经济性和先进技术”;它不包括安全（security）问题。

### 轨旁的控制

轨旁控制系统与铁路车辆的车载系统相互作用以协调其运行，向操作控制中心(OCC)发送信息，并与来自其他区域(通常被划分为几个区域的运输网络)的轨旁系统相互作用。本模块使用的标准是IEC 62264[7]。此规范的目标是“定义企业活动和控制活动之间的接口”。这个标准提供了描述企业业务系统之间接口的标准模型和术语。“安全（security）问题不在本标准的范围之内。

### OCC

OCC是运营商管理其传输网络和许多操作任务合并在一起的地方。有许多OCC配置，每个都可以使用不同的标准。其中之一是美国公共交通协会- RT – OP - 005-03 [8] 标准，它只考虑物理安全（physical security）。目前还没有关于网络安全的指导方针，因此使用的是普通的保护工具，比如商业杀毒软件或防火墙。

### 业务支持系统

公共交通运营使用这些系统来支持业务。它们通常包括电信组件来执行面向客户的操作。与OCC一样，网络保护工具也是商业杀毒软件。

### 网络威胁

新的网络威胁在今天看来如此之大，以至于影响关键信息基础设施的事件被视为全球风险[9]。随着威胁的日益增多，很难建立一个可靠的分类。因此，本节显示了可能影响铁路系统[10]的已识别的威胁。

安全和保障(safety and security)虽然不同，但有一个共同的主要目标：减少并尽可能消除风险。

■■分布式拒绝服务：这是一种阻止访问某个网络或计算机的攻击。它可以通过信息端口的饱和来生成，导致目标过载并且无法继续提供服务，这就是攻击被称为拒绝的原因。

■■僵尸网络：在这里，攻击模式是通过自动运行的软件机器人组或网络。黑客可以远程控制所有受感染的计算机或服务器。  

■■恶意软件：这是一种渗透和损坏信息系统或计算机的软件。恶意软件这一术语在网络社区中被广泛用于表示各种侵入式软件，但它还包括病毒，蠕虫，特洛伊木马和任何其他恶意软件。

■■欺骗：在这里，攻击者通过伪造通信数据来模仿不同的实体来窃取信息。  

■■网络诈骗：在这种情况下，攻击者自动传统的盗窃形式;黑客可以从许多金融账户中窃取少量资金，并且不留任何痕迹。窃取机密信息并索要赎金也是可能的。

所有用作铁路基础设施设计参考的标准（IEEE 1473 [5]，IEC 62264 [7]等）都不考虑网络安全;他们只提到实施者应该设计一个与标准一起使用的网络安全机制。这有点令人惊讶，因为所有系统都容易受到各种攻击。图3显示了铁路网可能面临的威胁[10]。更令人担忧的是，铁路制造商不一定遵循IEC 62443 [4]（建议用于安全规范）来确保网络安全，因为铁路行业不需要达到特定的安全级别来实施系统。然而，关于安全性（safety），在铁路应用中使用系统需要SIL的认证。

目前的方法是从专用电路交换技术（如GSM-R）转向基于IP和共享媒体接入的先进移动技术。后一种情况会以指数方式增加安全(security)问题。因此，安全性的提高应该成为一个主要问题，因为私营公司警告铁路目前存在的安全性(security)较差以及可能产生的后果[11]。
 
## 安全关键(Safety-Critical)系统中包含安全(security)的挑战

安全和保障(safety and security)虽然不同，但有一个共同的主要目标：减少并尽可能消除风险。要达到一定的安全水平，必须遵循EN 50129 [3]。但是，该标准用作开发或设计运输基础设施的参考，并未考虑其范围内的安全性(security)。目前，通过追求以下选项之一来应用铁路系统的安全性：

 ![12-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/12-4.png )
 

■■一般规范用于开发系统，遵循通用标准。

■■遵循IEC标准62443 [4]（也称为ISA-99）。使用这些选项的主要问题是标准的设计并未考虑整个运输基础设施，因此它们经常相互矛盾或留下空白。另一个问题是具有通用标准的解决方案似乎不灵活，即，在不同模块中实现相同的解决方案非常困难。

除了与安全标准(security standards)相关的问题之外，还有另一个问题：在铁路环境中，安全(safety)始终优先于安全(security)。铁路被认为是一个安全(safety)关键系统，因此仅仅描述就已经强调了安全(safety)这一术语。但是，由于铁路行业的历史，只有缺乏安全性(safety)才会导致灾难性事故。由于网络安全是一个相对较新的术语，因此没有与这些类型的安全(security)问题相关的重大事故。

开发铁路安全(safety)模块的专业人员通常不了解安全(security)问题，因此如果实施任何安全(security)技术，很可能在系统或模块开发之后完成。反之亦然：即许多安全(security)专家不考虑安全(safety)问题。安全(safety)和安全(security)专业人员之间缺乏相互理解使安全(security)实施变得复杂。

此外，即使制造商决定在开发安全(safety)装置时考虑安全性(security)，也有难以解决的技术问题，例如：

■■执行关键功能的任何硬件或软件都需要经过安全(safety)认证，如果包含安全(security)模块，则很难获得认证，因为模块的设计不符合安全(safety)标准。

■■即使包含安全（security）实现的安全(safety) 系统是通过认证的，也存在另一个问题：每天都会出现新的网络威胁，因此需要更新安全模块以确保保护。但是，如果对安全认证系统(safety-certified)进行任何更改，则必须重新认证。因此，每次更新安全模块时都不可能对系统进行认证。

■■某些安全协议（如PROFIsafe）建议使用加密和身份验证解决方案，但这不是强制性的。因此，有多个设备使用未加密的协议。如果添加安全性，这些协议需要接受加密消息，这会增加可能显着影响实时任务的处理时间（加密和解密）[12]。

如上所述，安全(safety)是铁路行业比安全(security)更广泛和熟悉的话题，因此一些组织甚至整个政府都不了解安全(security)问题以及这一领域改进的重要性也就不足为奇了。最重要的是，为了降低在关键系统中广泛使用通信所固有的潜在风险，必须考虑安全性。

即使制造商决定在开发安全装置时考虑安全性，也存在难以解决的技术问题。

## 安全与安全并存(Coexistence of Safety and Security)

公司已经意识到忽视安全(security)的危险，这就是为什么私人和公共实体组成的许多欧洲研究项目已经分析并提出了铁路领域安全问题的解决方案。例如，在ERTMS中，一些通信已经被标准化，例如，车载关键计算机到无线闭塞中心（RBC）无线通信和RBC到RBC通信。标准化意味着设备之间的通信包含对称密钥，以改善针对入侵者的网络安全[13]。

然而，所实现的系统的问题在于火车或轨道中的密钥的安装或更新是手动完成的，即，需要操作员的人工干预。这有两个大问题需要解决：高维护成本和内部人员攻击的风险。其他铁路通信渠道的安全性尚未标准化，并根据具体情况进行管理[14]。接下来的部分提供了一些建议和建议，以改善安全和安全（safety and security）的共存。

### 标准

今天，安全和安全（security and safety）标准之间的相互作用存在很大问题，那就是没有互动。很明显，如果任何制造商想要开发安全（safety）装置，它必须遵循EN 50129标准[3]，这反过来建议遵循IEC 62443 [4]的安全性(security)。但IEC 62443 [4]并未应用于铁路，因此难以实施甚至理解。

然而，在美国，APTA在“确保轨道交通环境中的控制和通信系统安全(secutiry)”（第I-IIIb部分）[15]中创建了轨道交通安全的具体规范。但它们只是如何实现安全性(security)的建议。这是第一步，但还不够，因为每个制造商都可以选择遵循或忽略这些建议。

因此，政府和安全公司应共同努力，为铁路专门开发一个共同的网络安全框架。这需要更高水平的技术专业知识来解决每天发展的网络威胁。因此，第一步应该是优先考虑某些威胁并仅保护重要功能。必须强制遵守安全规定。
 
### 技术
安全和安全(safety and security)问题的理想解决方案是创建一个包含这两个区域的标准，并让所有制造商都遵循它。但是，就目前而言，这似乎非常困难。因此，有必要找到一个使用当前规范的短期解决方案，其中包括安全(safety)设备的安全性(security)。为了说明安全性和安全性(safety and security)如何协同工作，提出了将网络入侵检测系统（NIDS）集成到安全(safety)设备中的示例。

NIDS需要经常更新，因为它会根据网络模式检测入侵，并且可以随时添加新模式。因此，安全(security)模块需要避免安全(safety)认证。为此，NIDS安全模块在物理上与安全(safety)模块分离，即安全(security)功能与安全(safety)功能隔离。当然，设备不得执行任何安全(safety-critical)关键任务。

系统需要访问通信网络以检测入侵。为了在不影响安全(safety)认证的情况下执行此操作，使用黑色通道原理。该原则要求数据和连通元件具有内置机制来检测任何干扰[16]。 EN 50129 [3]指出，如果在通信协议中添加了具有内置安全(safety)机制的层，则安全认证(safety-certified)和未认证的设备可以共享同一网络。

 ![12-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/12-5.png )
 

图4显示了所提出的安全 - 安全(safety-security)集成的体系结构，其中NIDS安全(security)模块与安全(safety)模块物理分离。然后可以对安全(safety)模块进行认证，并且应用安全层，像NIDS这样的未认证设备可以访问网络并充当网络嗅探器来检测入侵者。由于安全(security)模块不需要经过安全(safety)认证，因此可以更新，同时系统的安全(safety)认证保持不变。

提出的解决方案和建议只是集成安全性和安全性(safety and security)的一小步。认证机构，政府和制造商必须进行更详尽的工作，以确保安全性(security)的重要性。例如，欧盟委员会已经开始意识到网络安全在铁路行业中的重要性，并且它希望改进它有两个原因：主要是为了避免攻击同时降低维护成本。目标是到2020年，所有安全（security）改进都准备好在欧洲列车上实施[17]，届时希望不会太晚。

## 结论

本文对铁路基础设施的网络安全进行了评价。网络威胁可以影响组成铁路基础设施的所有模块，攻击可以像更改车票信息一样简单，也可以像更改列车速度一样危险。因此，可以这样说，安全(security)可以影响安全(safety)功能，安全(security)应该被认为与安全(safety)一样重要。

有一般和具体的标准，以达到预期的安全(safety)水平的电子模块，被用于铁路。但在网络安全方面，只有建议遵守和一般规范，这意味着每个制造商都有自己的标准来遵守或不遵守这些标准。很难达到最佳的安全（security）级别，因为规范推荐了不同的东西，如果制造商在一个模块中达到了可接受的安全(security)级别，那么在其他模块中应用相同的解决方案就非常复杂。因此，这种解决方案不可能适用于整个铁路系统。

安全性和安全性(safety and security)如何共存的问题已经通过添加到安全(safety)模块中的NIDS示例来介绍，而不影响安全(safety)认证。然而，这个解决方案只提供入侵检测;应该实现其他安全机制，比如消息加密，但它们需要与安全(safety)要求兼容。然后，应该由政府、认证机构和铁路工业制造商等主要参与者开发一个包括安全(safety)关键系统安全(security)在内的通用框架。

## References
[1] D. G. Firesmith, “Common Concepts Underlying Safety, Security,
and Survivability Engineering,” Carnegie-Mellon Univ., Pittsburgh,
PA, Tech. Note CMU/SEI-2003-TN-033, 2003.

[2] Functional Safety of Electrical/Electronic/Programmable Electronic
Safety-Related Systems—Part 2: Requirements for Electrical/Electronic/
Programmable Electronic Safety-Related Systems, CENELEC EN
61508, 2011.

[3] Railway Applications. Communication, Signalling, and Processing
Systems. Safety-Related Electronic Systems for Signalling, CENELEC
EN 50129, 2005.

[4] Industrial Automation and Control Systems Security, International Society
for Automation, IEC 62443, 2013.

[5] Standard for Communications Protocol Aboard Passenger Trains, IEEE
Standard 1473-2010, 2011.

[6] Code for Design of Subway, Beijing Urban Engineering Design and
Research Institute, GB-50157-2003, 2003.

[7] Enterprise-Control System Integration, IEC 62264, 2013.

[8] Operations Control Centers, APTA-RT-OP-S-005-03, 2012.

[9] D. Tofan, T. Nikolakopoulos, E. Darra. (2016). The cost of incidents
affecting CIIs. European Union Agency for Network and Information
Security (ENISA), Heraklion, Greece. [Online]. Available: https://
www.enisa.europa.eu/publications/the-cost-of-incidents-affecting-ciis

[10] GSM-R Industry Group. (2016). Security aspects and transition management
when introducing IP in the railway domain. Presented at
the 12th Int. Union of Railways European Management Syst. World
Conf. [Online]. Available: http://www.ertms-conference2016.com/
IMG/pdf/1.3_selex_gsm-r_ig_p_di_labio_security_aspects_on_ip_
draft.pdf

[11] F. Pujol and J. S. Marcus, “Evolution of GSM-R,” IDATE Research,
Montpelier, France, ERA/2014/04/ERTMS/OP Final Report, 2015.

[12] K.Hansen, “Security attack analysis of safety systems,” in Proc. IEEE
Conf. Emerging Technologies and Factory Automation, 2009, pp. 1–4.

[13] “Offline key management FIS: SUBSET-038,” UNISIG, Brussels, Belgium,
2012.

[14] European Commission. (2015). Shift2Rail joint undertaking multiannual
action plan. European Commission, Brussels, Belgium.
[Online]. Available: http://www.shift2rail.org/wp-content/uploads/
2013/07/MAAP-final_final.pdf

[15] J. Thompson, T. Ellis, J. Moore, et al. (2010). Securing control and
communications systems in rail transit environments. American
Public Transportation Association, Washington, D.C. [Online].
Available: https://www.apta.com/resources/standards/Documents/
APTA%20SS-CCS-RP-004-16.pdf

[16] A. Elia, L. Ferrarini and C. Veber, “Analysis of Ethernet-based safe
automation networks according to IEC 61508,” in Proc. IEEE Conf.
Emerging Technologies and Factory Automation, 2006. doi: 10.1109/
ETFA.2006.355419.

[17] European Commission. (2015). HORIZON 2020: The EU framework programme
for research and innovation. [Online]. Available: https://
ec.europa.eu/programmes/horizon2020
