# 2023-3-23 Thu
### 安装环境
可不安装有[在线环境](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

本人采用ubuntu20.4+vmware+vscode的安装方式

1. 在ubuntu和vmware的官网下载镜像和虚拟机软件并进行安装
2. 在rust官网直接下载deb包并在Ubuntu中进行安装，例：sudo dpkg -i   XXX.deb
3. 进一步在Ubuntu中安装网络工具和ssh。
    > apt install net-tool
    > 
    > apt install ssh
    > 
    > service ssh restart
    >
    > service sshd start
    >
    >vim /etc/ssh/sshd_config
    >
    >>#将修改里面的内容
    >>
    >> LoginGraceTime 2m
    >>
    >>PermitRootLogin yes
    >>
    >>StrictModes yes
    >
    >#检查ip信息 
    >
    > ifconfig

    > #然后再window上用cmd或者xshell登录
    >
    > ssh username@ip

4. vscode远程登录
在vscode中安装Remote-SSH插件，填写hostname(你的ip)和username

### Rustup & Cargo
**rustup** 是 Rust 的安装程序，也是它的版本管理程序。

与其它语言相比，Rust 的更新迭代较为频繁

* 每 6 周发布一个迭代版本

* 2-3 年发布一个新的大版本，例如 Rust 2018 edition，Rust 2021 edition

**rustc** 是rust的编译器，单个可执行文件编译直接
```
rustc xxx.rs
./xxx
```

**cargo** 是 Rust 的构建系统和包管理器，用来管理 Rust 工程和获取工程所依赖的库。cargo 提供了一系列的工具，从项目的建立、构建到测试、运行直至部署，为 Rust 项目的管理提供尽可能完整的手段。

```
//编译+运行
cargo run 
//编译
cargo build
./XXX
```
Cargo.toml 是项目数据描述文件。它存储了项目的所有元配置信息，定义了项目按照怎样的方式进行构建、测试和运行

Cargo.lock 文件是 cargo 工具根据同一项目的 toml 文件生成的项目依赖详细清单，一般不作修改

# 2023-03-29 Wed
### 语法规则

#### 变量与常量
常量使用 const 关键字而不是 let 关键字来声明，并且值的类型必须标注（Rust 常量的命名约定是全部字母都使用大写，并使用下划线分隔单词）

变量分可变变量和不可变变量

可变变量指变量的内容可以改变，不需要重新分配内存，直接修改内存中的内容，用**mut**修饰
```
let mut a = 1;
a += 2;
```
不可变变量表示变量的内容不可变，变量名与内存绑定，变量名拥有当前内存所有权。相同变量名可以重新绑定，此时会重新分配内存
```
let a = 2;
a = 3;  //error, a 不可变

let a = 3;  //重新指代，之前的a被遮蔽不可用
let a = "123";  //重新指代，并且数据类型发生变化
```

#### 数据类型
数值类型: 有符号整数 (i8, i16, i32, i64, isize)、 无符号整数 (u8, u16, u32, u64, usize) 、

浮点数 (f32, f64)、以及有理数、复数

字符串：字符串字面量和字符串切片 &str

布尔类型： true和false

字符类型: 表示单个 Unicode 字符，存储为 4 个字节

单元类型: 即 () ，其唯一的值也是 ()
