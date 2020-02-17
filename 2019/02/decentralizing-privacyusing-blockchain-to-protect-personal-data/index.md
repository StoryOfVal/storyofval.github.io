# Decentralizing Privacy:Using Blockchain to Protect Personal Data


Zyskind G, Nathan O, Pentland A, et al. Decentralizing Privacy: Using Blockchain to Protect Personal Data[C]. ieee symposium on security and privacy, 2015: 180-184.

链接： https://ieeexplore.ieee.org/abstract/document/7163223 

## Abstract

最近揭露的监视和安全漏洞事件不断增加，这损害了用户的隐私，同时使得当前的模式受到质疑，其中第三方收集和控制了大量的个人数据。比特币已经证明了，通过一个公用的分类账，使用分布式的对等网络在金融领域进行可信的和可审计的计算是可行的。在本文中，我们描述了一个分布式的的个人数据管理系统，确保用户对他们数据的所有权和控制权。我们实现了一个协议，将区块链变成一个自动访问控制管理器，而不需要第三方信任。与比特币不同，我们系统中的交易不是严格的金融交易 - 它们被用于携带指令，例如存储，查询和共享数据的指令。最后，我们将讨论区块链未来可能的发展，这些发展可以使它们用于社会可信计算问题的全面解决。

<!--more-->

## I. Introduction

世界上的数据量正在迅速增加，我们世界的数据量正在迅速增加。根据最近的一份报告，过去几年世界上有20％的数据被收集。Facebook是最大的在线社交网络，自成立以来收集了300PB的个人数据  - 是国会图书馆200多年来收集的数百倍。在大数据时代，数据不断被收集和分析，从而带来创新和经济增长。公司和组织使用他们收集的数据来提供个性化服务，优化公司决策过程，预测未来趋势等。今天，数据是我们经济中的宝贵资产。

> 数据增长迅速及数据的重要地位

虽然我们都从数据驱动的社会中获益，但公众越来越关注用户隐私。中心化组织 - 包括公共和私人组织 - 收集大量个人和敏感信息。个人很少或根本无法控制存储的数据及其使用方式。近年来，公共媒体一再报道与隐私有关的争议事件。其中比较着名的例子是Facebook的大规模科学实验，它是在没有明确通知参与者的情况下进行的。

> 公众关注隐私但没有对自己隐私数据的控制权

### Related Work

已有各种尝试来解决这些隐私问题，包括从立法的角度和从技术的角度。Open-PDS是一个最近开发的框架，它提供了一个PDS自主部署模型，包括一个返回数据计算的机制，从而返回答案而不是原始数据本身。在整个行业中，领先的公司选择实施基于OAuth协议的专有认证软件，其中它们作为集中的可信管理机构。

> 采用Open-PDS的原因是，提供原始数据可能会被滥用，但提供计算后的结果没有这个问题

从安全角度来看，研究人员开发了各种针对个人数据的隐私问题的技术。**数据匿名化方法试图保护个人身份信息**。k-匿名（k-anonymity），匿名数据集的一个共同属性要求每个记录的敏感信息与至少k-1个其他记录可区分。k-匿名的相关扩展包括l-多样性（l-diversity），它确保敏感数据由足够多的可能值表示; t-closeness，它关注敏感数据的分布。最近的研究表明，即使是少量的数据点或高维数据，采用这些技术的匿名数据集如何进行去匿名化。其他隐私保护方法包括**差异隐私**（differential privacy），在共享数据之前扰乱数据或将噪声添加到计算过程的技术，以及允许在加密数据上运行计算和查询的加密方案。具体而言，**完全同态加密（FHE）**方案允许任何计算在加密数据上运行，但目前效率太低而无法在实践中广泛使用。

> 提供了保护数据隐私已有的三种方案，但不够完善，无法正式使用

区块链技术在近些年出现。第一个是比特币，它允许用户使用可公开验证的开放式分类账（或区块链）在没有集中式监管机构的情况下安全地转移货币（比特币）。从那时起，其他项目（统称为比特币2.0 ）展示了这些区块链如何服务于其他需要可信计算和可审计性的功能。

### Our Contribution

1. 我们将区块链和链下存储相结合，构建一个专注于隐私的个人数据管理平台。
2. 我们通过我们的平台和对未来技术改进的讨论来说明区块链如何成为可信计算的重要资源。

> 如题，这部分是该论文所做工作的核心

### Organzation

第二节讨论了我们在本文中解决的隐私问题;

第三节概述了平台;

第四节介绍了技术实施细节;

第五节讨论了区块链的未来发展;

第六节是结论。

<br>

## II. The Privacy Problem

在本文中，我们将解决用户在使用第三方服务时所面临的隐私问题。我们专注于移动平台，其中服务作为应用程序部署供用户安装。这些应用程序不断收集用户没有特定认识或控制能力的高度相关的个人数据。在我们的分析中，我们假设服务是诚实但好奇的（即，它们遵循协议）。值得注意的是，同一系统可用于其他数据隐私问题，例如患者共享其医疗数据用于科学研究，但同时意味着监控其使用方式和随时退出的能力。鉴于此，我们的系统可以应对以下常见隐私问题：

- **数据所有权**：我们的框架侧重于确保用户拥有和控制他们的个人数据。因此，系统将用户识别为数据所有者，服务则被授予权限作为宾客。
- **数据透明性和可审计性**：每个用户关于自己的数据以及如何访问这些数据都完全透明。
- **细粒度的访问控制**：移动应用程序的一个主要问题是用户在注册时需要授予一组权限。这些权限是无限期授予的，更改协议的唯一方法是选择退出。在我们的框架中，用户可以在任何给定时间更改权限集并撤消对先前收集的数据的访问权限。此机制的一个应用是改进移动应用程序中的现有权限对话框。虽然用户界面可能保持不变，但访问控制策略将安全地存储在区块链中，并只允许用户更改它们。

> 用户对其数据具有完全控制能力，服务提供商被授予权限，具体细节由“细粒度的访问控制”描述

<br>

## III. Proposed Solution

我们首先概述我们的系统。如图1所示，系统由三部分构成：智能手机用户，下载和使用应用程序；服务，这些应用程序的提供者，需要以用于操作和业务相关的原因（例如，有针对性的广告，个性化服务）来处理个人数据；节点，维护区块链和分布式私人键值对数据存储以换取奖励。请注意，虽然系统中的用户通常保持（伪）匿名，但我们可以在区块链上存储服务配置文件并验证其身份。

图1

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-fig-1-source-large.gif)

系统本身的设计如下。区块链接受两种新类型的交易：T<sub>access</sub>，用于访问控制管理；T<sub>data</sub>，用于数据存储和检索。这些网络操作可以轻松集成到一个移动软件开发工具包（SDK）中，其中的服务可以在开发过程中使用。

用一个例子来说明：用户安装一个应用程序，并使用我们的平台保护其隐私。当用户第一次注册时，生成新的共享（用户，服务）身份，并使用T<sub>access</sub>交易将其与相关联的权限一起发送到区块链。在手机上收集的数据（例如，传感器数据，位置）使用共享加密密钥加密，并使用T<sub>data</sub>交易发送到区块链，随后将其路由到链下键值存储，同时仅保留一个指向数据的指针存在区块链上（指针是数据的SHA-256哈希值）。

> 意即区块链上存访问权限和隐私数据哈希值
>
> 链下存隐私数据

现在，服务和用户都可以使用关联指针的T<sub>data</sub>交易查询数据。区块链会验证数字签名属于用户还是服务。对于服务，还会检查其访问数据的权限。最后，用户可以通过发布具有新权限的T<sub>access</sub>交易来随时更改授予服务的权限，包括撤销对先前存储的数据的访问权。正在开发基于Web的（或移动端）dashboard，允许对一个人的数据和权限更改作总览，类似于开发集中式钱包，比如比特币的Coinbase。

> T<sub>access</sub>交易用于权限，T<sub>data</sub>交易用于数据

链下的键值存储是分布式哈希表（或DHT）的一个实现，使用[LevelDB](http://leveldb.org/)和到区块链接口增加了持久性。DHT由节点网络（可能与区块链网络脱节）维护，其完成授权的读/写交易。数据在节点之间充分随机化并复制以确保高可用性。值得注意的是，可以考虑使用替代的链下存储方案。例如，可以使用集中式云来存储数据。虽然这需要对第三方的某种程度的信任，但它在可伸缩性和易部署方面具有一些优势。

> 链下存储用LevelDB，也可以用集中式存储

<br>

## IV. The Network Protocol

我们现在详细描述系统中使用的底层协议。在我们的平台中使用标准加密构建区块：由3元组（G<sub>enc</sub>，E<sub>enc</sub>，D<sub>enc</sub>）定义对称加密方案 - 分别是生成器，加密和解密算法；由3元组（G<sub>sig</sub>，S<sub>sig</sub>，V<sub>sig</sub>）描述数字签名方案（DSS） - 分别是生成器，签名和验证算法；加密散列函数H由SHA-256实现。

### A. Building Blocks

现在简要介绍本文提到的区块。假设熟悉比特币和区块链。

#### Identities

区块链使用伪身份机制。为了增加隐私，每个用户都可以根据自己的需要生成尽可能多的伪身份（实质是是一个公钥）。我们现在引入复合身份，这个模型的一个扩展用在我们的系统中。复合身份是一个两方或多方的共享身份，其中一些方（至少一方）拥有身份（所有者），其余方被限制访问（访客）。协议1说明了单个所有者（用户）和单个访客（服务）的实现。如协议所示，身份包括用于所有者和访客的签名密钥对，以及用于数据加密（和解密）的对称密钥，以便保护数据免受系统中的所有其他参与者的影响。形式上，复合身份在外部（如网络中）看来是一个二元组：
$$
\begin{equation*}Compound_{u, s}^{(public)}=(pk_{sig}^{u, s},pk_{sig}^{s, u})
\tag{1}
\end{equation*}
$$
相似的，整个身份（包括私钥）是如下五元组：
$$
\begin{equation*}Compound_{u, s}=(pk_{sig}^{u, s},sk_{sig}^{u, s}, pk_{sig}^{s, u},sk_{sig}^{s, u},sk_{enc}^{u, s})
\tag{2}
\end{equation*}
$$
协议1 Generating a compound identity

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-graphic-1-source-large.gif)

#### Blockchain Memory

我们让L代表区块链存储空间，表示为哈希表 L：{0,1} <sup>256</sup>→{0,1} <sup>N</sup>，其中N>>256并且可以存储足够大的文档。我们假设这个存储在比特币和其他区块链中使用的相同对抗模型下是防篡改的。为了直观地解释为什么这种可信数据存储可以在任何区块链（包括比特币）上实现，请考虑以下简化的，虽然效率低下的实现：区块链是一系列带时间戳的交易，其中每个交易包括可变数量的输出地址（每个地址是160位的值）。然后可以按如下方式实现L  - 交易中的前两个输出哈希为256位存储地址指针（其实就是哈希值），以及一些辅助元数据。其余的输出构成了序列化文档。查找L [k]时，仅返回最近的交易，除了插入之外，还允许更新和删除操作。

#### Policy

用户u授予服务s的一组权限，由**POLICY<sub>u，s</sub>**表示。例如，如果u安装了需要访问用户位置和联系人的移动应用程序，那么POLICY<sub>u，s</sub> = {location，contacts}。值得注意的是，假设服务不会破坏协议并错误地标记数据，任何类型的数据都可以通过这种方式安全存储。可以在移动SDK中引入部分防止这种情况的保护措施，但无论如何，用户可以轻松检测到作弊的服务，因为他可以看到所有更改。

#### Auxiliary Functions（辅助功能）

Parse（x）并行化发送到交易的消息，消息包含参数；协议2中说明的CheckPolicy（pk<sup>k</sup><sub>sig</sub>，x<sub>p</sub>）验证发起者是否具有适当的权限

协议2 Perissions check against the blockchain

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-graphic-2-source-large.gif)

### B. Blockchain Protocols

在这里，我们详细描述在区块链上执行的核心协议。当接收到T<sub>access</sub>交易时，协议3由网络中的节点执行，类似地，对T<sub>data</sub>交易执行协议4。

协议3 Access Control Protocol

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-graphic-3-source-large.gif)

协议4 Storing or Loading Data

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-graphic-4-source-large.gif)

如本文前面所述，T<sub>access</sub>交易允许用户通过发送POLICY<sub>u，s</sub>来更改授予服务的权限集。发送空集会撤消先前授予的所有访问权限。使用新的复合身份发送T<sub>access</sub>交易将被解释为用户首次注册服务。

类似地，T<sub>data</sub>交易控制读/写操作。在Check Policy的帮助下，只有用户（总是）或服务（如果允许）才能访问数据。请注意，在协议4的第9行和第16行中，我们使用简写符号来访问DHT，就像普通的哈希表一样。实际上，这些指令产生发送到DHT的链下的网络消息（读或写）。

### C. Privacy and Security Analysis

我们依赖于区块链是无篡改的，这种假设需要一个足够大的不受信任的对等网络。此外，我们假设用户以安全的方式管理她的密钥，例如使用安全的集中式钱包服务。我们现在展示我们的系统如何防止攻击者破坏系统中的节点。目前，我们不太关心改变协议或记录先前读取数据的恶意服务，因为它们很可能是有信誉的，但我们在第V-A节中提供了这种行为的可能解决方案。

> 足够大的对等网络是个问题，考虑小型网络是否可行

鉴于此模型，只有用户可以控制她的数据。区块链的分布式的特性与数字签名交易相结合，确保对手无法冒充用户或破坏网络，因为这意味着对手伪造了数字签名，或者控制了大部分网络资源。同样，攻击者无法从区块链中学到任何东西，因为只有哈希指针存在链里。

控制一个或多个DHT节点的对手无法得到有关原始数据的任何信息，因为它是使用没有任何节点拥有的密钥加密的。请注意，虽然每个节点都不能确保数据完整性，因为单个节点可以篡改其本地副本或以拜占庭方式操作，但我们仍然可以通过充分切分和复制数据来最小化风险。

> 这里带来的问题包括多个数据副本的存储开销，存储节点虽然无法获取数据，但篡改行为可能存在

最后，为每个用户 - 服务对生成新的复合身份可确保在攻击者获得签名和加密密钥的情况下，只有一小部分数据受到危害。如果攻击者只获得其中一个键值，那么数据仍然是安全的。请注意，在实践中，我们可以进一步分割身份，以限制单个复合身份的暴露。例如，我们可以为每100条记录存储生成新密钥。

<br>

## V. Discussion of Future Extensions

在本节中，我们稍微讨论一下区块链未来的发展。与当前最先进的系统相比，这些可以在塑造更成熟的分布式可信计算平台方面发挥重要作用。更具体地说，它们将大大增加先前提出的平台的实用性。

### A. From Storage to Processing

到目前为止，我们的分析侧重于存储指向加密数据的指针。虽然这种方法适用于存储和随机查询，但它对处理数据的效率不高。**更重要的是，一旦服务查询到一段原始数据，它就可以存储它以供将来分析**。

> 加粗的这句是重点，数据被获取到之后就不具有价值了

更好的方法可能是永远不要让服务获取原始数据，而是允许它直接在网络上运行计算并获得最终结果。如果我们split data into shares（例如，使用Shamir's Secret Sharing），而不是加密它们，我们就可以使用安全的多方计算（MPC）来安全地评估任何功能。

在图2中，我们说明了MPC如何与区块链结合使用，特别是在我们的框架中。考虑一个简单的例子，其中一个城市举行选举并希望允许在线秘密投票。它开发了一个投票的移动应用程序并使用了我们的系统，现在增加了MPC的功能。在线选举结束后，该市随后提交其后端数据以汇总结果。网络随机选择节点子集，解释器将数据转换为安全的MPC协议。最后，结果存储在区块链中，以防止篡改。结果，没有人知道个人投了什么票，但每个人都可以看到选举的结果。

> 解决办法是后台做计算，只存计算结果

图2 

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7160794/7163193/7163223/7163223-fig-2-source-large.gif)

### B. Trust and Decision-Making in Blockchains

比特币或一般的区块链假设所有节点都是同等不受信任的，并且它们在集体决策过程中的比例完全基于它们的计算资源（称为工作量证明算法）。换句话说 - 对于每个节点，资源（概率地）决定节点在投票中的权重。这会导致不利影响，最显著的是对sybil攻击的脆弱性，过度的能量消耗和高延迟。

直观上，工作量证明体系中将更多资源投入系统中的节点更不可能作弊。相似的，我们可以定义一种基于节点行为的新的信任的动态度量，比如遵循协议的行为会得到奖励。具体来说，我们可以将每个节点的信任度设置为其未来表现良好的预期值。同样，由于我们处理的是二进制随机变量，因此期望值只是概率p。逼近这种概率的一种简单方法是计算节点所采取的好的和坏的动作的数量，然后使用sigmoid函数将其压缩成概率。在实践中，每个块i我们都应该以公式(3)重新评估每个节点的信任分数 
$$
\begin{equation*}trust_{n}^{(i)}= \frac{1}{1+e^{-\alpha(\# good-\# bad)}},
\tag{3}
\end{equation*}
$$
其中α 只是步长

基于这种度量，网络可以为可信节点提供更多权重并更有效的计算区块，因为这些节点花费了时间在系统中获取信任。它应当能抵抗sybil攻击。这种机制可能会吸引其他类型的攻击，例如节点增加其信用只是为了以后恶意行为。这可以通过随机选择几个节点来缓解，这些节点按其信任加权，对每个块进行投票，然后进行同等加权的多数投票。这可以防止单个参与者受到太多影响，无论他们的信任级别如何。

> 有点类似于PoS和DPoS

<br>

## VI. Conclusion

个人数据和一般敏感数据的存储不应该信任第三方，因为第三方容易受到攻击和滥用数据。相反，用户应该拥有并控制他们的数据，而不影响安全性或限制公司和权威机构提供个性化服务的能力。我们的平台通过将区块链和链下存储解决方案相结合来实现这一目标。用户不需要信任任何第三方，并且始终知道正在收集的有关他们的数据及其使用方式。此外，区块链将用户识别为其个人数据的所有者。反过来，公司可以专注于利用数据而不过度担心正确保护和划分数据。

此外，通过分布式的平台，制定关于收集，存储和共享敏感数据的法律和监管决策应该更加简单。此外，法律法规可以编入区块链本身，以便自动执行。在其他情况下，分类帐可以作为访问（或存储）数据的合法证据，因为它是（计算上）防篡改的。

最后，我们讨论了区块链的几种可能的未来发展，这些发展可以利用它们为社会中可信计算问题提供全面的解决方案。
