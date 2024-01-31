
# wosame go principle

https://archive.org/details/github.com-0voice-Introduction-to-Golang_-_2021-08-18_08-08-36
[introduce to go](https://github.com/0voice/Introduction-to-Golang)
https://github.com/yongxinz/gopher
https://blog.csdn.net/github_36774378/article/details/124290796?spm=1001.2014.3001.5502


如果要继承一个接口，你只需要在结构体中实现该接口声明的所有方法。


```
// 定义 Animal 接口
interface Animal {
  Eat()  // 声明 Eat 方法
  Move()  // 声明 Move 方法
}

// ==== 定义 Dog Start ====
// 定义 Dog 类
type Dog struct {
}

// 实现 Eat 方法
func (d *Dog) Eat() {
  fmt.Printf("Eating bones")
}

// 实现 Move 方法
func (d *Dog) Move() {
  fmt.Printf("Moving with four legs")
}
// ==== 定义 Dog End ====

// ==== 定义 Human Start ====
// 定义 Human 类
type Human struct {
}

// 实现 Eat 方法
func (h *Human) Eat() {
  fmt.Printf("Eating rice")
}

// 实现 Move 方法
func (h *Human) Move() {
  fmt.Printf("Moving with two legs")
}
// ==== 定义 Human End ====
```

#### go语言编译比rust更快的原理是什么？


[如何编写一个全新的 Git 协议](https://linux.cn/article-6065-1.html)

 
 ```
 git remote add myremote go::http://example.com/repo
 git push myremote master

 ```
[Learn-Git-Guidebook-For-Developers-Chapter-2](https://initialcommit.com/blog/Learn-Git-Guidebook-For-Developers-Chapter-2)


https://learnblockchain-cn.translate.goog/article/4215?_x_tr_sl=zh-CN&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=sc



gitea organize 
最新版本的问题迭代


概念
Cobra 建立在命令、参数和标志这三个结构之上。要使用 Cobra 编写一个命令行程序，需要明确这三个概念。



命令（COMMAND）：命令表示要执行的操作。

参数（ARG）：是命令的参数，一般用来表示操作的对象。

标志（FLAG）：是命令的修饰，可以调整操作的行为。

```
要编写一个好的命令行程序，需要遵循的模式是 APPNAME VERB NOUN --ADJECTIVE 或 APPNAME COMMAND ARG --FLAG。

$ hugo server --port=1313

$ git clone URL --bare

```
在这种情况下，可以使用 git clone URL --bare 命令来克隆一个裸仓库。裸仓库是一个没有工作树的 Git 仓库副本，只包含版本控制的文件和元数据。它通常用于创建远程仓库或者作为共享仓库，供多个用户或团队使用。

我们可以使用 options.Output、options.Verbose 等字段访问各个标志的值，并根据需要执行相应的逻辑。




从零开始理清楚一个逻辑的耐心！和系统的轻视
大系统，小解读
多系统，大解读

[defi developer road map](https://github.com/OffcierCia/DeFi-Developer-Road-Map)







基本的git知识：
不可以汉语登录？
[Git-Guidebook-For-Developers-Chapter](https://initialcommit.com/blog/Learn-Git-Guidebook-For-Developers-Chapter-2)



gitea故事：saas








### 使用的场景：
repo

code

tag

code cloc





### 常见的实现和约束：

. 先有个人，再有组织，企业，高校
. 个人空间不可以重复，现在不支持自定义个人git的地址，默认名字拼音作为空间组成 比如 https://github/liuyuchao/demo.git、https://gitee/liuyuchao/demo.git

同一个用户：企业高校，旗舰只有一个











### 问题：
 1. 不同部门相同的用户名会存在问题
 - 登录和同步的时候。
 - git push 等基本所有的操作的时候

2. 组织的使用需求,场景无
 - 跳转问题
 - 权限控制需求  


3. 同步租户为：二院，所，部门这种逻辑组织来使用数据库会很复杂
 - 不符合常规设计的使用方法包括git协议，代码保存，机构直属等等
 -  代码仓库转让到其他的成员，成员之间的权限问题难以控制，
 - 代码按照组织层级保存再目录上或者存储应用上，比如 minio

4. 代码和数据库各组织部门备份
 - 数据库没有做到不同命名空间进行区分：如果要做没有java动态的数据源库
 - 代码存放再其他设备上，类似文件分部门备份
 - 支持 /repo（ local  minio  lfs）， 存储形式 /repo/{branch、 objects、tag等}
 - ![minio storage](image-66.png)



-- 备份指定用户或者组织的数据 数据库/代码hash object
-- go实现的多数据源动态切换！






### 改进方法

1. 使用 https://github/eryuan/706/sanbu/test.git代替https://github/liuyuchao/demo.git

问题1：所有的代码逻辑接口都需要改变，.git的结构 git协议修改 如push pull的问题
refs
data

2. 和gitee,github类似只有企业和个人的解决方案,保存用户的所有信息，部门，身份证等，liuyuchao_1221（身份证后四位），（电话号）的登录名，进行区分

问题2：可能接受的企业单位粒度，以及粒度对应下的个人，就是gitee的企业组织的方法：706，还是三部这个粒度当作一个企业，或者一个团队为 git仓库
   （可能的方法，保存用户的所有信息，部门，身份证等，liuyuchao_1221（身份证后四位）的登录名，进行区分）
   （而且建立仓库的是否，是需要进入对应的组织再建立仓库，而且我可能是个人使用的场景，）

问题3：
同步过来先有机构，再有个人--谁建立机构，root管理员的分配部门的问题,
- 后期没有登录，注册接口





