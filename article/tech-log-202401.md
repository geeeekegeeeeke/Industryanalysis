## techlog

![Alt text](image-36.png)

### atuin的使用方法，最好的使用就是代码本身，文件都是一种代码不合格的表现

atuin init bash
atuin register   login

atuin history list

```
 Possible values:
          - zsh:  Zsh setup
          - bash: Bash setup
          - fish: Fish setup
          - nu:   Nu setup

```
的区别？
这些值代表不同的命令行壳程序（shell）以及它们的设置方式。下面是它们之间的一些主要区别：

Zsh（Z Shell）：Zsh是一个功能强大的命令行壳，它提供了许多高级功能和配置选项。它具有自动补全、历史命令搜索、模糊匹配、主题和插件支持等特性。Zsh的配置文件是~/.zshrc。

Bash（Bourne Again Shell）：Bash是许多Linux和Unix系统默认使用的命令行壳。它是Zsh的前身，提供了基本的命令行功能，如命令历史记录、变量扩展、管道等。Bash的配置文件是~/.bashrc。

Fish（Friendly Interactive Shell）：Fish是一个用户友好的命令行壳，注重易用性和交互性。它提供了语法高亮、自动补全、智能提示、内置函数等功能。Fish的配置文件是~/.config/fish/config.fish。

Nu：Nu是一个现代化的命令行壳，旨在提供更简洁、可组合、易于使用的命令行体验。它采用了一种基于数据流的操作方式，支持结构化数据处理。Nu的配置文件是~/.nu/config.toml。



### binwalk
binwalk无法直接分解图片里面的图片文件
```apt install binwalk ```

[unblob](https://unblob.org/)


### foremost

[foremost](https://sourceforge.net/projects/foremost/)
分解图片
```
apt install foremost
```
解决binwalk无法直接分解图片里面的图片文件
picture下的file.jpg作为测试实验

### winhex

[winhex](https://en.softonic.com/download/winhex/windows/post-download?ex=CS-1689.4)


### osmedeus

[进攻性安全的工作流引擎](https://github.com/j3ssie/osmedeus)


前沿的动态的区块链安全切入角度

https://github.com/practical-tutorials/project-based-learning.git



[代码夹克和混淆工具](DRMsoft  EncryptEXE)
https://blog.51cto.com/senseshield/4314712



### EXECryptor
适用场景加壳运行的程序，反汇编而已。
有支持代码和资源的压缩


专业的程序加壳脱壳工具，可以有效地保护程序进行逆向工程分析、修改和破解，保护自己的版权。

VMProtect允许对可执行文件（EXE、SCR）、动态链接库（DLL，OCX，BPL）和驱动程序（SYS）进行保护



### awesome-malware-analysis

https://github.com/geeeekegeeeeke/awesome-malware-analysis

[匿名网络](http://anonymouse.org/cgi-bin/anon-www.cgi/http://www.google.com/webhp?hl=en)

基于网络的匿名器和Tor之间的一些区别：

架构和工作原理：基于网络的匿名器和Tor在架构和工作原理上有所不同。基于网络的匿名器通常是代理服务器，通过转发用户的网络请求来隐藏其真实IP地址和身份。基于网络的匿名器可以通过不同的协议（如HTTP、SOCKS等）提供代理服务。






### 什么是grapql，和普通的http的请求有什么不同？
代码层面展示

```
package main

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"

	"github.com/graphql-go/graphql"
)

type User struct {
	ID   string `json:"id"`
	Name string `json:"name"`
}

var data map[string]User

func init() {
	data = map[string]User{
		"1": User{
			ID:   "1",
			Name: "Alice",
		},
		"2": User{
			ID:   "2",
			Name: "Bob",
		},
	}
}

func main() {
	// 定义 GraphQL 对象类型
	userType := graphql.NewObject(graphql.ObjectConfig{
		Name: "User",
		Fields: graphql.Fields{
			"id": &graphql.Field{
				Type: graphql.String,
			},
			"name": &graphql.Field{
				Type: graphql.String,
			},
		},
	})

	// 定义 GraphQL 根查询类型
	rootQuery := graphql.NewObject(graphql.ObjectConfig{
		Name: "Query",
		Fields: graphql.Fields{
			"user": &graphql.Field{
				Type: userType,
				Args: graphql.FieldConfigArgument{
					"id": &graphql.ArgumentConfig{
						Type: graphql.String,
					},
				},
				Resolve: func(params graphql.ResolveParams) (interface{}, error) {
					id, _ := params.Args["id"].(string)
					return data[id], nil
				},
			},
		},
	})

	// 定义 GraphQL 模式
	schema, err := graphql.NewSchema(graphql.SchemaConfig{
		Query: rootQuery,
	})
	if err != nil {
		log.Fatalf("failed to create schema, error: %v", err)
	}

	// 定义 GraphQL 处理函数
	http.HandleFunc("/graphql", func(w http.ResponseWriter, r *http.Request) {
		result := graphql.Do(graphql.Params{
			Schema:        schema,
			RequestString: r.URL.Query().Get("query"),
		})
		json.NewEncoder(w).Encode(result)
	})

	// 启动 HTTP 服务器
	fmt.Println("Server started at http://localhost:8080/graphql")
	log.Fatal(http.ListenAndServe(":8080", nil))
}

```

``` http://localhost:8080/graphql?query={user(id:"1"){id,name}} ```

### 老老实实解决问题，产品化的需求，前后端分离注定是一种工作需求而不是能力需求！




https://github.com/99designs/gqlgen

https://github.com/vektah/gqlparser


支持查询语法的数据库

https://github.com/dgraph-io/dgraph 

github.com/graphql-go/graphql



https://github.com/TykTechnologies/tyk



https://github.com/TykTechnologies/tyk?tab=readme-ov-file


## 图数据库了解



## 构建信息秩序
## 选择信息源
## 消费信息

linux 执行文件的几种方式：

chmod +x 给文件可执行命令：

移动到 /usr/local/bin
或者 /usr/bin

命名规范是 snake case
struct camel case


## rust by example  
https://foresightnews.pro/article/detail/10089

https://rust-cli.github.io/book/tutorial/index.html

https://rustmagazine.org/

[包含了使用rust来写一个os的项目的博客](https://zh.practice.rs/elegant-code-base.html)

通过有挑战性的示例、练习题、实践项目来提升 Rust 水平，建立从入门学习到上手实战的直通桥梁
[Rust语言圣经github](https://github.com/sunface/rust-course)

# rust
 sudo code --no-sandbox --user-data-dir ~


 # truffle

 

# 一个严谨的devSecOps开发者的工具箱！
主要是通用工具在开发中的严谨的构造，从代码到发布产品的代码管理一整套工具。从代码编码检查，单元测试，静态动态分析，漏洞扫描和分析的一整套工具箱！







 sudo code --no-sandbox --user-data-dir ~




# 树莓派的体验和使用购买 


