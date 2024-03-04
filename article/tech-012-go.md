

### 现有使用的场景：

- 代码仓库：开发者和其他
 issue  pr  repo 分支模型  **组织权限控制不太符合**
 

- 代码hooks,钩子函数回调-devops回调，触发
code

- 版本发布：版本间代码差异提交入库，三方接口代码树结构查看，接口查询
tag

- 代码统计和简单分析 
code cloc
代码行数，文件数，注释数，空行数等等


- 代码库本身的权限管理，组织管理，代码分支管理！



### 常见的实现和约束：

.  先有个人，再有组织，企业，高校
. 个人空间不可以重复如:https://github.com/liuyuchao/demo.git 的空间是liuyuchao
. 空间名字英文
. 仓库http地址分三级（ip+user+repo）：https://github.com/liuyuchao/demo.git

现在不支持自定义个人命名空间git的地址，默认名字拼音作为空间组成 比如 https://github.com/docker/libcompose.git、git clone https://gitee.com/daka1004/godemo.git







### 问题：多租户备份、权限使用
 1. 不同部门相同的用户名会存在问题
 - 从onroad同步和登录的时候。
 - git push 等基本所有的操作的时候




2. 同步修改租户为onroad逻辑：二院，所，部门这种逻辑组织来使用数据库和代码文件保存会很复杂
 - 不是常规设计的使用方法包括git地址协议（不止三级），代码保存（/data/repo/{user,org}）
 - 代码仓库转让到其他的成员，成员之间的权限问题难以控制，
 - 代码按照组织层级保存在目录上或者存储应用上，比如 minio，导致备份复杂



3. 代码和数据库各组织部门备份
 - 数据库没有做到不同命名空间进行区分：如果要做没有java动态的数据源库，minio空间动态切换等
 - 代码存放./data/gitea-repo，类似文件分部门备份现有代码设计无法做到。
  (现在支持 /repo（ local  minio  lfs）所有代码备份，涉及到恢复问题（.git结构和实际代码不同）
 - ![minio storage](image-66.png)




4. 组织的使用需求场景还需要更清晰

 - 权限控制需求 
 - 数据备份 



共性问题：
-  备份指定用户或者组织的数据（数据库/代码），代码本质（hash object。同步用户用户名字维护如liuyuchao_1273

-  go实现的多数据源动态切换！如果是minio，bucket空间切换






### 改进方法

1. 使用 https://github/eryuan/706/sanbu/test.git代替https://github/liuyuchao/demo.git

 - 问题1：所有的代码逻辑接口都需要改变，.git的结构 git协议修改 如push pull的问题refs data

 - 问题2：所有用户数据都通过onroad接口调用，或者租户相关表导入同步过来

2. 和gitee,github类似只有企业和个人的解决方案,保存用户的所有信息，部门，身份证等，liuyuchao_1221（身份证后四位）当作git工作空间，（电话号）的登录名，进行区分，


  - 问题1：可能接受的企业单位粒度，以及粒度对应下的个人，就是gitee的企业组织的方法：706，还是三部这个粒度当作一个企业，或者一个团队为 git仓库
   （可能的方法，保存用户的所有信息，部门，身份证等，liuyuchao_1221（身份证后四位）的登录名，进行区分）
   （而且建立仓库的是否，是需要进入对应的组织再建立仓库，而且我可能是个人使用的场景，）


 - 问题2：
同步过来先有机构，再有个人--谁建立机构?root管理员的分配?部门的问题,
-- 后期没有登录，注册接口,同步数据如何保证第二个同名
--  同步数据如何保证第二个同名liuyuchao_7831类似数据 
-- 基础用户数据都是来自onroad,备份必要性
-- 代码仓库自身的数据库备份部分，没有不同命名空间的区分，有空间区分，使用逻辑很复杂，但是只有备份的时候才起作用
--用户进行操作需要反复访问onroad,确定租户，或者gitea数据库冗余很多没有用的数据，
-- 无法单独使用，无法独立使用
-- 不同步如何保证同onroad数据一致性



结论：
保证单主机多服务隔离使用空间部署-各部门独立使用代码库和空间
代码仓库权限外界访问隔离
支持minio使用
key管理模块，push代码权限验证支持
同步用户重名解决方法？？？涉及到onroad跳转，身份证验证问题


## go eth source code
https://github.com/agiletechvn/go-ethereum-code-analysis

https://github.com/Billy1900/Ethereum-tutorial

https://github.com/ZtesoftCS/go-ethereum-code-analysis/blob/master/go-ethereum%E6%BA%90%E7%A0%81%E9%98%85%E8%AF%BB%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA.md

https://github.com/ABCDELabs/Understanding-Ethereum-Go-version

https://learnblockchain.cn/article/3912

https://github.com/learnerLj/geth-analyze/blob/main/analyzeSourceCode/EVM%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%8E%9F%E7%90%86/%E5%88%9D%E6%AD%A5%E7%90%86%E8%A7%A3%E4%BB%A5%E5%A4%AA%E5%9D%8A%E8%99%9A%E6%8B%9F%E6%9C%BA.md


[手把手用智能合约开发去中心化交易所](https://www.zhihu.com/zvideo/1277985686630133760)


流动性：锁定在池子的相对于美元的价值数量

智能合约源码：
https://blog.csdn.net/llslinliansheng/article/details/129404672

https://learnblockchain.cn/article/4021
https://mirror.xyz/adshao.eth/VY6aLzdjwXGif9O1C7UMuYFmivC4q5jDQqQUho6tLWY

https://github.com/chennyouneng2020/Uniswap?tab=readme-ov-file



[EVM 设计原理](https://learnblockchain.cn/article/4952)


RLP(Recursive Length Prefix) 递归长度前缀编码是以太坊中最常使用的序列化格式方法。












### 如何衡量对一个系统的理解程度？
阅读源代码是一种漫长的修行。为了方便自检修行的结果，我们将对一个系统的理解程度划分为下面四个等级。

**Level 4: 掌握（Mastering）**
在完全理解的基础上，可以设计并编写一个全新的系统
根据实际需求，重写系统模块
可以使用另一种编程语言重新复现本系统
**Level 3: 完全理解（Complete Understanding）**
在理解的基础上，完全掌握系统各个模块实现的细节
能快速的从系统功能模块定位到其对应的代码库的位置
可以将系统定制化到不同的应用场景
能对系统中的各个模块做出优化
**Level 2: 理解（Understanding）**
熟练使用系统的常用 API
了解系统各个模块的调用关系
了解部分核心模块的设计细节
能对系统的部分模块进行简单修改/重构
**Level 1:了解（Brief understanding）**
了解系统设计的主要目标
了解系统的应用场景
了解系统的主要功能
可以使用系统的部分的 API
我们希望读者在阅读完本系列之后，对以太坊的理解能够达到 Level 2 - Level 3 的水平。



被应用在了多种私有/联盟/Layer-2的场景中(e.g., Quorum, Binance Smart Chain, Scroll, Arbitrum , Optimism)。

https://nishino.gitbook.io/wang-luo-guo-jia/kuai-su-kai-shi/1.1-xu-yan


Rollups 是强大的区块链扩展解决方案，在过去两年中变得非常流行。有两种类型的 rollups，ZK-rollups 和 Optimistic rollups，它们的目的相同但功能不同。


https://www.theblockbeats.info/news/34604

evm 

https://learnblockchain.cn/article/4952


这个是所谓的重商主义。这个商，其实不要觉得他是在鼓吹自由贸易，他其实鼓吹的就是国家的贸易顺差。国际贸易当中，你要有顺差，你要不断的出口。这种观点当然是非常片面的。

这三个方面有三个关键词，一个是自利之心，一个是市场均衡，第三个是演化秩序。

 
，他觉得英国的这个古典经济学家的古典精神非常好，因为既能够提炼出一个理论结构，而且看起来也相当有说服力的。他认为，人类社会不仅有经济规律可言，而且这个经济规律是可以研究的。




当我们在炫耀所谓的成就的时候，其实很少有你去看你是的经济，政治和科学技术，没有什么是我们做到的，这本身就是有很大问题的，一直追求所谓的一致性，结果就是一致性的愚蠢。

有货币，消费品也可以在其中决定出价格。问题在于，一旦你涉及到高级财货，这些高级财货是需要经过一系列生产的流程才能够变成最终产品，才能满足消费者的需求的，要决定这些高级财货的价格，就需要一个东西，叫做跨期的经济核算。比如说你在年头做的投资，增加的工厂

遗传，而不是择优录取本质上，是一种不知道什么玩意儿的梦想。

如说粮食。但是在计划经济体制之下，由于所有的计划都必须经过中央计划委员会的处理，因此就不可避免的会面临时滞问题，面临各种各样的调配的僵化问题，使得整个经济体越来越僵化，乃至于根本没有办法达到那种有效利用资源的状态。

就是 《奥地利学派经济学入门以及米塞斯思想精要》。这本书大家可以当把它当成是对米塞斯思想的一个简要的解读，也是米塞斯思想最重要的一部分。第二本书是米塞斯的 《人的行为》

为什么计划经济跟民主是不能兼容的。

现在的信息和思考，让人觉得，你可以没有电视，但是不能没有几个没有信息限制的电脑。

当和很普通人一样的思考逻辑，说明就是low,需要更换圈子子


因为所有的企业家都要依赖货币来进行经济核算，因此当货币本身的价值下降，使得所有的企业家的货币余额都出现了增长的情况之下，这些企业家就可能都以为自己赚到钱了，做了对的事情，而使得他们都去增加生产。就是我一核算，货币余额增加了，那我不是做了对的事情么，我应该增加生产才对啊。在这个过程当中，货币本身币值的变动构成了所有企业家犯错的一个根源。这就是商业周期的奥地利学派解释的核心。



