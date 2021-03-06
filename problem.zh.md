
# {{Paj.Toe}}

## 问题: 建立一个网络

> 我必须创造一个系统,或者被另一个人奴役,没有原因与比较心理,只因为: 我主旨是创造. *—William Blake*

假设您希望构建计算机网络,而该网络具有增长到全球范围的潜力,并且支持各种应用程序,如电话会议, 视频点播, 电子商务, 分布式计算和数字图书馆. 哪些可用技术将作为基础构建块,以及您将设计什么样的软件体系结构来将这些构建块集成到有效的通信服务中? 回答这个问题是本书的首要目标 - 描述可用的建筑材料,然后展示如何从地基开始构建网络. 

在我们了解如何设计计算机网络之前,我们应该首先就计算机网络是什么达成一致. *网络*一词的术语, 一度解释为用来连接哑终端到大型计算机的串行线路集合. 其他重要的网络,包括语音电话网络和用于传播视频信号的有线电视网络. 这些网络的主要共同点在于它们专门处理一种特定类型的数据 (按键, 语音或视频) ,并且它们通常连接到专用设备 (终端, 手持接收器和电视机) . 

计算机网络与其他类型的网络有什么区别?计算机网络最重要的特征可能是它的通用性. 计算机网络主要是由通用可编程硬件构建的,并且它们没有针对特定的应用进行优化,例如打电话或传送电视信号. 相反,它们能够承载许多不同类型的数据,并且它们支持广泛且不断增长的应用范围. 今天的计算机网络正在逐步接管以前的网络执行的单调用途功能. 本章着眼于计算机网络的一些典型应用,并探讨一下,哪些希望支持此类应用的网络设计人员必须了解的要求. 

一旦我们了解了需求,我们该如何着手? 幸运的是,我们不会建立第一个网络. 其他人,尤其是负责互联网的研究者们,已经在我们面前种树了. 我们将利用互联网产生的丰富经验来指导我们的设计. 这些经验体现在*网络架构*中,*该架构*定义了可用的硬件和软件组件,并展示如何安排它们以形成完整的网络系统. 

除了理解如何构建网络之外,理解如何操作和管理网络以及如何开发网络应用程序也变得越来越重要. 我们中的大多数人现在在家里, 办公室里和一些汽车里都有计算机网络,所以操作网络不再只是少数专家的事情. 而且,随着可编程, 网络+设备 (如智能手机) 的扩散,这代人将比过去开发更多的网络应用. 因此,我们需要从多个角度考虑网络: 构建器, 运营商, 应用程序开发人员. 

为了让我们开始了解如何构建, 操作和编程一个网络,本章做了四件事. 首先,探讨了不同应用和不同社区的人对网络的需求. 其次,介绍了网络架构的思维,为本书的其余部分奠定了基础. 第三,介绍了实现计算机网络的一些关键要素. 最后,确定了用于评估计算机网络性能的关键指标. 
