# rust

## 第一章


## 简介

### 为什么要用rust

* 可以用来替换c/c++，rust和它们具有同样得性能，但是很多常见得bug在编译时就可以被消灭
* rust善于一下场景
  * 需要运行时得速度
  * 需要内存安全
  * 更好得利用多处理器



### 与其他语言比较

* c/c++性能非常好，但是类型系统和内存都不安全
* java/c#，拥有GC，能保证内存安全，也有很多优秀特性，但是性能不行。
* Rust:
  * 安全
  * 无需GC
  * 易于维护、调试，代码安全高效




### Rust特别擅长的领域

* 高性能Web Service
* WebAssembly
* 命令行工具
* 网络编程
* 嵌入式设备
* 系统编程

### Rust的优点

* 性能
* 安全性
* 无所畏惧的并发

### Rust的缺点

* “难学”

### 注意

* Rust有很多独有的概念，它们和现在大多主流语言都不同。
  * 所以学习Rust必须从基础概念一步一步学，否则会懵。



## 安装Rust

### 安装rust

* 官网：[http://www.rust-lang.org]()
* linux or mac：
  * curl https://sh.rustup.rs -sSf | sh
* windows：按官网指示操作
* windows Subsystem for linux：
  * curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

### 更新与卸载rust

* 更新rust
  * rustup update
* 卸载rust
  * rustup self uninstall

### 安装验证

* rustc --version
  - 结果格式： rust x.y.z（abcabcabc yyyy-mm-dd）
  - 会显示最新稳定版得：版本号、commit hash、commit 日期
  
  ![1726976526926](.\rust\1726976526926.jpg)

### 本地文档

* 安装rust得时候，还会在本地安装文档，可离线浏览
* 运行rustup doc 可在浏览器打开本地文档

### 开发文档

* Visual Studio Code
  * rust插件
* Clion（Intellij Idea系列）
  * rust插件

 

## Hello World

### 编写Rust程序

* 程序文件后缀名：rs
* 文件命名规范：hello_world.rs

![1727054754124](.\rust\1727054754124.jpg)

### 编译与运行Rust程序

* 编译：rustc main.rs
* 运行： 
  * Windows： .\main.exe
  * Linux/mac： ./main
  

### Rust程序解剖

* 定义函数：fn main() {}
  * 没有参数，没有返回
* main函数很特别：它是每个Rust可执行程序最先运行得代码
* 打印文本： println!("Hello, world!");
  * Rust得缩进是4个空格而不是tab
  * println!是一个Rust macro（宏）
    * 如果是函数得话，就没有！
  * "Hello World"是字符串，它是println!得参数
  * 这行代码是；结尾

### 编译和运行是单独得两步

* 运行Rust程序之前必须先编译，命令为：rustc 源文件名
  * rustc main.rs
* 编译成功后，会生成一个二进制文件
  * 在Windows上还会生成一个.pdb文件，里面包含调试信息
  
  ![1727054869108](.\rust\1727054869108.jpg)
* Rust是ahead-of-time编译得语言（预先编译语言）
  * 可以先编译程序，然后把可执行文件交给别人运行（无需安装rust）
* rustc只适合简单得rust程序



## Hello Cargo

### Cargo

* cargo 是Rust的构建系统和包管理工具
  * 构建代码、下载依赖的库、构建这些库……
* 安装Rust的时候会安装Cargo
  * cargo --version（查看版本）

### 使用Cargo创建项目

* 创建项目：cargo new hello_cargo

  * 项目名称也是hello_cargo

  * 会创建一个新的目录hello_cargo

    * cargo.toml

    * src目录

      * main.js

    * 初始化了一个新的Git仓库，.gitignore

      * 可以使用其他的VCS或不使用VCS：cargo new 的时候使用 --vcs 这个flag

      ![1727093529749](.\rust\1727093529749.jpg)

### Cargo.toml

![1727093857977](.\rust\1727093857977.jpg)

* toml（Tom's Obvious, Minimal Language)格式，是Cargo的配置格式

* [package]，是一个区域标题，表示下方内容是用来配置包（package）的
  * name，项目名
  * version，项目版本
  * authors，项目作者
  * edition，使用的Rust版本
* [dependencies]，另一个区域的开始，它会列出项目的依赖项。
* 在Rust里面，代码的包称作Crate。



### src / main.rs

* cargo生成的main.rs在src目录下
* 而Cargo.toml在项目顶层下
* 源代码都应该在src目录下
* 顶层目录可以放置：README、许可信息、配置文件和其他与程序源代码无关的文件
* 如果创建项目时没有使用cargo，也可以把项目转化为使用cargo：
  * 把源代码文件移动到src下
  * 创建Cargo.toml并填写相应的配置



### 构建Cargo项目 --- cargo build

* cargo build
  * 创建可执行文件：target / debug / hello_cargo 或 target \ debug \ hello_cargo.exe（Windows）
  * 运行可执行文件：./target/debug/hello_cargo 或 .\target\debug\hello_cargo.exe（Windows）
* 第一次运行cargo build会在顶层目录生成cargo.lock文件
  * 该文件负责追踪项目依赖的精确版本
  * 不需要手动修改该文件



### 构建和运行cargo项目 --- cargo run

![1727094736994](.\rust\1727094736994.jpg)

* cargo run，编译代码 + 执行结果
  * 如果之前编译成功过，并且源代码没有改变，那么就会直接运行二进制文件



### cargo check

* cargo check，检查代码，确保能通过编译，但是不产生任何可执行文件
* cargo check要比cargo build快的多
  * 编写代码的时候可以连续反复的使用cargo check检查代码，提高效率



### 为发布构建

* cargo build --release
  * 编译时会进行优化
    * 代码会运行的更快，但是编译时间更长
  * 会在 `target/release`而不是`target/debug`生成可执行文件
* 两种配置：
  * 一个开发
  * 一个正式发布

## 第二章



### 猜数游戏：一次猜测

* 学会什么：
  * let、match等方法
  * 相关的函数
  * 外部的crate
  * ……

#### 目标

* 生成一个1到100间的随机数
* 提示玩家输入一个猜测
* 猜完之后，程序会提示猜测是太小了还是太大了
* 如果猜测正确，那么打印出一个庆祝信息，程序退出

````rust
use std::io;
// std 标准库

fn main() {
    println!("猜数！");

    println!("猜测一个数：");

    // let mut foo = 1;
    // let bar = foo; //默认是不可变的 immutable
    // foo = 2;

    // 使用utf-8编码，可以按自己的需求扩展自己的大小
    // ：new是string类型的关联函数，针对类型本身来实现的，相当于c#,java的静态方法，new在rust里面创建类型实列的惯用名称
    let mut guess = String::new();  

    // read_line ： rust标准库里面有好多Result类型，Result枚举类型
    io::stdin().read_line(&mut guess).expect("无法读取行");
    // io::Result Ok, Err

    println!("你猜测的数是：{}", guess);
}

````



### 2.2 猜数游戏 - 生成神秘数字

[下载库的地址](https://crates.io/)

![1727098581228](.\rust\1727098581228.jpg)

* 根据`cargo.toml`生成更新后的`cargo.lock`文件 `cargo update`

````rust
use rand::Rng;
use std::io;

fn main() {
    println!("猜数！");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("神秘数字是：{}", secret_number);

    println!("猜测一个数：");

    // let mut foo = 1;
    // let bar = foo; //默认是不可变的 immutable
    // foo = 2;

    // 使用utf-8编码，可以按自己的需求扩展自己的大小
    // ：new是string类型的关联函数，针对类型本身来实现的，相当于c#,java的静态方法，new在rust里面创建类型实列的惯用名称
    let mut guess = String::new();

    // read_line ： rust标准库里面有好多Result类型，Result枚举类型
    io::stdin().read_line(&mut guess).expect("无法读取行");
    // io::Result Ok, Err

    println!("你猜测的数是：{}", guess);
}

````

### 2.3 猜数游戏 - 比较猜测数字与神秘数字

````rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("猜数！");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("神秘数字是：{}", secret_number);

    println!("猜测一个数：");

    // let mut foo = 1;
    // let bar = foo; //默认是不可变的 immutable
    // foo = 2;

    // 使用utf-8编码，可以按自己的需求扩展自己的大小
    // ：new是string类型的关联函数，针对类型本身来实现的，相当于c#,java的静态方法，new在rust里面创建类型实列的惯用名称
    let mut guess = String::new();

    // read_line ： rust标准库里面有好多Result类型，Result枚举类型
    io::stdin().read_line(&mut guess).expect("无法读取行");
    // io::Result Ok, Err

    // shadow（隐藏特性），rust里面的shadow特性，可以隐藏变量，变量名可以重复，一般用在类型转换的时候
    let guess: u32 = guess.trim().parse().expect("解析失败！");

    println!("你猜测的数是：{}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("小了"), // arm match手臂，他会从上到下以此匹配
        Ordering::Greater => println!("大啦"),
        Ordering::Equal => println!("猜对了"),
    }
}

````

 ### 2.4 猜数游戏 - 允许多次猜测

````rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("猜数！");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    loop {
        println!("猜测一个数：");

        let mut guess = String::new();
        // read_line ： rust标准库里面有好多Result类型，Result枚举类型
        io::stdin().read_line(&mut guess).expect("无法读取行");
        // io::Result Ok, Err

        // shadow（隐藏特性），rust里面的shadow特性，可以隐藏变量，变量名可以重复，一般用在类型转换的时候
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("你猜测的数是：{}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("小了"), // arm match手臂，他会从上到下以此匹配
            Ordering::Greater => println!("大啦"),
            Ordering::Equal => {
                println!("猜对了");
                break;
            }
        }
    }
}

````

## 第3章 通用的编程概念

* 变量与可变性
* 数据类型
  * 标量类型
  * 复合类型
* 函数
* 注释
* 控制流

### 3.1 变量与可变性

* 声明变量使用`let`关键词

* 默认情况下，变量是不可变的（immutable）

  ````rust
  fn main() {
      println!("Hello, world!");
  
      let mut x = 5;
      println!("The value of x is {}", x);
  
      x = 6;
      println!("The value of x is {}", x);
  }
  ````

* 声明变量时，在变量前面加上`mut`，就可以使变量可变。

#### 变量与常量

* 常量（constant），常量在绑定值以后也是不可变的，但是它与不可变的变量有很多区别：
  * 不可以使用`mut`，常量永远都是不可变的
  * 声明常量使用`const`关键词，它的类型必须被标注
  * 常量可以在任何作用域内进行声明，包括全局作用域
  * 常量只可以绑定到常量表达式，无法绑定到函数的调用结果或只能在运行时才能计算出的值
* 在程序运行期间，常量在其声明的作用域内一直有效
* 命名规范：Rust里常量使用全大写字母，每个单词之间用下划线分开，例如：
  * MAX_POINTS
* 例子：`const MAX_POINTS: u32 = 100_000`

#### Shadowing（隐藏）

* 可以使用相同的名称声明新的变量，新的变量就会shadow（隐藏）之前声明的同名变量
  * 在后续的代码中这个变量名代表的就是新的变量
* shadow和把变量标记为mut是不一样的：
  * 如果不使用let关键字，那么重新给非mut的变量赋值会导致编译时错误
  * 而使用let声明的同名新变量，也是不可变的
  * 使用let声明的同名新变量，它的类型可以与之前不同

````rust
fn main() {
    let x = 1;
    let x = x + 1;
    let x = x * 2;

    println!("The value of x is: {}", x);

    let spaces = "    ";
    let spaces = spaces.len();

    println!("{}", spaces);
}

````



### 3.2数据类型

* 标量和复合类型

* Rust是静态编译语言，在编译时必须知道所有变量的类型

  * 基于使用的值，编译器通常能够推断出它的具体类型

  * 但是如果可能的类型比较多（例如把String转为整数的parse方法），就必须添加类型的标注，否则编译会报错

    ````rust
    fn main() {
        // let guess = "42".parse().expect("Not a number!");
        let guess: u32 = "42".parse().expect("Not a number!");
    
        println!("{}", guess)
    }
    
    ````

    

#### 标量类型

* 一个标量类型代表一个单个的值
* Rust有四个主要的标量类型：
  * 整数类型
  * 浮点类型
  * 布尔类型
  * 字符类型

#### 整数类型

* 证书类型没有小数部分

* 例如`u32`就是一个无符号的整数类型，占据32位的空间

* 无符号整数类型以 U 开头

* 有符号整数类型以 i 开头

* Rust的整数类型列表如图：

  * 每种都分 i 和 u， 以及固定的位数
  * 有符号范围：

  $$
  -(2^n - 1) 到 2^{n-1} - 1
  $$

  * 无符号范围：

  $$
  0 到 2^n - 1
  $$



![1727183160244](.\rust\1727183160244.jpg)

#### isize 和 usize类型

* isize 和 usize 类型的位数由程序运行的计算机的架构所决定：
  * 如果是64位计算机，那就是64位的
  * ……
* 使用 isize 或 usize 的主要场景是对某种集合进行索引操作。

#### 整数字面值

* 除了byte类型外，所有的数值字面值都允许使用类型后缀。
  * 例如 `57u8`
* 如果你不太清楚应该使用那种类型，可以使用Rust相应的默认类型：
* 整数的默认类型就是`i32`：
  * 总体上来说速度很快，即使在64位系统中

![1727183877312](.\rust\1727183877312.jpg)

#### 整数溢出

* 例如：u8的范围是 0 - 255，如果你把一个 u8 变量的值设为 256，那么：
  * 调式模式下编译：Rust会检查整数溢出，如果发生溢出，程序在运行时就会panic
  * 发布模式下（--release）编译：Rust不会检查可能导致panic的整数溢出
    * 如果溢出发生：Rust会执行“环绕”操作：
      * 256 变成 0， 257 变成 1 ……
    * 但程序不会panic

#### 浮点类型

* rust有两种基础的浮点类型，也就是含有小数部分的类型

  * `f32`，32位，单精度
  * `f64`，64位，双精度

* rust的浮点类型使用了 `IEEE-754`标准来表述

* `f64`的默认类型，因为在现代CPU上`f64`和`f32`的速度差不多，而且精度更高

  ````rust
  fn main() {
      let x = 4.0;    // f64
  
      let y: f32 = 5.0;       // f32
  }
  ````

  

#### 数值操作

* 加减乘除余等

````rust
fn main() {
    let sum = 5 + 10;

    let difference = 95.5 - 4.3;

    let product = 4 * 30;

    let quotient = 56.7 / 32.2;

    let reminder = 54 % 5;
}
````

#### 布尔类型

* rust的布尔类型也有两个值： `ture`和`false`

* 一个字节大小

* 符号是`bool`

  ````rust
  fn main() {
      let t = true;
      let f: bool = false;
  }
  ````

#### 字符类型

* rust语言中char类型被用来描述语言中最基础的单个字符
* 字符类型的字面值使用单引号
* 占用4字节大小
* 是`Unicode`标量值，可以表示比`ASCII`多得多的字符内容：拼音、中日韩、零长度空白字符、emoji表情等。
  * U+0000 到 U+D7FF
  * U+E000 到 U+10FFFF
* 但是`Unicode `中并没有“字符”的概念，所以直觉上认为的字符也许与Rust中的概念并不相符

```` rust
fn main() {
    let x = 'z';
    let z = '😀';
}
````



### 3.3 复合类型

* 复合类型可以将多个值放在一个类型里。
* Rust提供了两种基础的复合类型：元组（Tuple）、数组

#### Tuple

* Tuple可以将多个类型的多个值放在一个类型里
* Tuple的长度是固定的：一旦声明就无法改变

##### 创建Tuple

* 在小括号里，将值用逗号分开
* Tuple中的每个位置都对应一个类型，Tuple中各元素的类型不必相同

```` rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
    println!("{}, {}, {},", tup.0, tup.1, tup.2);
}
````

##### 获取tuple的元素值

* 可以使用模式匹配来解构（destructure）一个Tuple来获取元素的值

  ````rust
  fn main() {
      let tup: (i32, f64, u8) = (500, 6.4, 1);
      
      let (x, y, z) = tup
      println!("{}, {}, {},", x, y, z);
  }
  ````

##### 访问Tuple的元素

* 在tuple变量使用点标记法，后接元素的索引号

#### 数组

* 数组也可以将多个值放在一个类型里
* 数组中每个元素的类型必须相同
* 数组的长度也是固定的

##### 声明一个数组

* 在中括号里，各值用逗号分开

````rust
fn main() {
    let arr = [1, 2, 3, 4, 5];
}
````

##### 数组的用处

* 如果想让你的数组存放在`stack`（栈）上而不是`heap`（堆）上，或者想保证有固定数量的元素，这时使用数组更有好处
* 数组没有`Vector`灵活
  * `Vector`和数组类似，它由标准库提供
  * `Vector`的长度可以改变
  * 如果你不确定应该用数组还是`Vector`，那么估计你应该用`Vector`。

##### 数组的类型

* 数组的类型以这种形式表示：[类型; 长度]
  * 例如： `let a: [i32; 5] = [1,2,3,4,5];`

##### 另一种声明数组的方法

* 如果数组的每个元素值都相同，那么可以在：
  * 在中括号里指定初始值
  * 然后是一个“；”
  * 最后是数组的长度
* 例如：`let a = [3; 5];`它就相当于：`let a = [3,3,3,3,3];`

##### 访问数组的元素

* 数组是`Stack`上分配的单个块的内存

* 可以使用索引来访问数组的元素

  * `a[0]`

* 如果访问的索引超出了数组的范围，那么：

  * 编译会通过

  * 运行会报错（runtime时会panic）

    * Rust不会允许其继续访问相应地址的内存

    ![1727185908048](.\rust\1727185908048.jpg)

### 3.4 函数

* 声明函数使用`fn`关键字
* 依照惯例，针对函数和变量名，Rust使用`snake case`命名规范：
  * 所有的字母都是小写的，单词之间使用下划线分开

````rust
fn main() {
    println!("hello world");
    another_function();
}

fn another_function() {
    println!("Another function");
}
````

##### 函数的参数

* parameters（定义时的参数）,argument（调用时的参数）
* 在函数签名里，必须声明每个参数的类型

````rust
fn main() {
    println!("hello world");
    another_function(5);	// argument
}

fn another_function(x: i32) {	// parameter
    println!("Another function");
}
````

##### 函数体中的语句与表达式

* 函数体由一系列语句组成，可选的由一个表达式结束
* Rust是一个基于表达式的语言
* 语句是执行一些动作的指令
* 表达式会计算产出一个值
* 函数的定义也是语句
* 语句不返回值，所以不可以使用let将一个语句赋给一个变量

```` rust
fn main() {
    //let x = (let y = 6); // panic
    
    let x = 5;
    let y = {
        let x = 1;
        x + 3
        //x + 3; //返回空元组()
    };
    
    println!("The value of y is: {}", y);
}
````

##### 函数的返回值

* 在 `->` 符号后边声明函数返回值的类型，但是不可以为返回值命名
* 在Rust里面，返回值就是函数体里面最后一个表达式
* 若想提前返回，需使用`return`关键字，并指定一个值
  * 大多数函数都是默认使用最后一个表达式最为返回值

````rust
fn five(x: i32) -> i32 {
    x + 5 
}
fn main() {
    let x = five(6); // 5 + 6
    
    println!("The value of x is {}", x);
}
````

##### 注释

* `//` 和 `/* */`
* Rust还有一种“文档注释”