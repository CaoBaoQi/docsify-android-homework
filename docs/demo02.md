# 🌈目标

- [x] 掌握 Java 环境的安装和配置
- [x] 掌握 Android Studio 的安装和配置
- [x] 了解基本项目结构
- [x] 在 Android Studio 创建虚拟机
- [x] 使用 Android Studio 构建 HelloAndroid 项目

## 1.1 开发环境配置

Android 应用开发是基于 Java 语言开发的，所以在进行 Android 开发前我们需要下载 JDK 并将其配置到环境变量中。

### 1.1.1 Java 语言

### 发展历程

[Java](https://www.oracle.com/cn/java/technologies/downloads/#java17) 最初由 James Gosling 等人在 Sun Microsystems 公司开发，于1995年发布第一个版本。自那时以来，Java 一直在不断发展和改进，下面是 Java 发展历程的简要概述：

1. 1995年：发布第一个版本 Java ，用于编写安全可靠的客户端和服务器应用程序。
2. 1997年：发布 Java  2 Enterprise Edition（J2EE），引入了一系列企业级特性，如 JCA（Java Connection API）和 JDBC（Java Database Connectivity），使 Java 更适合用于大型企业级应用程序。
3. 1998年：Java 引入了网络编程特性，如 RMI（Remote Method Invocation）和 JNDI（Java Naming and Directory Interface），使 Java 可以用于网络应用程序。
4. 2001年：Java 发布了新版本 Java SE 6，其中包括新的语言特性，如 Lambda 表达式和接口支持，以及改进的多线程和集合框架。
5. 2006年：Java 发布了新版本 Java SE 7，其中包括更快的垃圾回收和更高效的网络编程支持，以及新的 JavaFX 框架，用于创建交互式图形用户界面。
6. 2010年：Java 发布了新版本 Java SE 8，其中包括新的语言特性，如 Optional 类型和增强的方法重载和抽象方法支持。

### 组成

JDK（Java Development Kit）和JRE（Java Runtime Environment）是 Java 开发和运行的两个关键组件。

JRE 是 Java 运行时环境，它是 Java 应用程序所需的一组软件库和 JVM 的实例。JRE 提供了 Java 语言的基本运行环境，包括 JVM、Java 字节码解释器、垃圾回收器、日志记录器等。JRE 的作用是在运行 Java 应用程序时，为 Java 程序提供必要的运行环境和资源。

JDK 是 Java 开发工具包，它包含了许多开发 Java 应用程序所需的工具和软件库。JDK 包括了编译器、工具、API 等组件，开发者可以使用 JDK 来开发和测试 Java 应用程序。JDK 的作用是为 Java 应用程序的开发和调试提供必要的工具和支持。

总的来说，JRE 和 JDK 都是 Java 开发和运行的重要组件。JRE 提供了 Java 应用程序所需的运行环境和资源，而 JDK 提供了开发者所需的工具和支持，用于开发和调试 Java 应用程序。

### 1.1.2 Java 环境配置

通过上面的讲述我们了解了 Java 的发展历程和组成，其中：

- JDK 不仅包括 JRE 还带有相关的工具包
- JRE 为 Java 运行环境

即有了 JRE 只能保证我们可以运行 Java 程序，所以作为开发人员我们直接下载 JDK 即可 ~

### JDK 的下载

我们可以通过 [Java 官网](https://www.oracle.com/cn/java/technologies/downloads/#java17) 来下载 JDK （此处选用的是 JDK 17）

Oracle 为我们提供了多种安装方式

- x64 Compressed Archive 压缩包方式需要手动配置环境信息
- msi 安装包方式无需手动配置环境信息

#### MSI 方式



![image-20231017175850942](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175850942.png)



如果你是使用的 MSI 方式安装的 JDK 在安装完成后其实已经可以使用了



![image-20231017175903020](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175903020.png)



#### 压缩包方式

压缩包方式需要我们手动为 JDK 配置相关的环境变量



![image-20231017175912334](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175912334.png)



### 配置环境变量

环境变量是操作系统中的一种设置，用于存储系统中需要访问的文件和配置信息。在 Windows 中，可以使用环境变量来存储 Java JDK 所需的库文件、系统设置和工具，以便程序可以在运行时访问这些资源。

在 Windows 中设置环境变量可以通过以下步骤完成：

1. 打开“控制面板”，然后选择“系统和安全”。
2. 选择“系统”，然后选择“高级系统设置”。
3. 在“高级”选项卡中，单击“环境变量”按钮。



![image-20231017175924117](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175924117.png)



#### JAVA_HOME

我们先新建一个名为 `Java_HOME` 的变量（用于引入到 path 中作为替换）



![image-20231017175937563](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175937563.png)



这样做的好处是当我们需要修改 JDK 版本时只需要修改 `JAVA_HOME` 指定的路径即可而不需要改动 Path 中的参数



![image-20231017175951380](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017175951380.png)

添加 `%JAVA_HOME%\bin` 至环境变量 Path 中



#### CLASSPATH

CLASSPATH环境变量，是当我们在开发Java程序时需要引用别人写好的类时，要让 Java解释器知道到哪里去找这个类。

Emmmm 网上资料说 Java17 是不需要配置 CLASSPATH 的但 (我好像遇到过相关类找不到的问题) 此处给出配置方式吧



![image-20231017180001702](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180001702.png)



- `CLASSPATH`
- `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar`



注意变量值中 `.` 的作用表示当前目录下因此要注意不能缺少

### 验证

在 cmd 中输入 `java -version`



![image-20231017180010435](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180010435.png)

## 1.2 Android Studio 安装和配置

### 1.2.1 下载安装 Android Studio

我们可以前往 [Android Studio 官网](https://developer.android.google.cn/studio?hl=zh-cn) 进行安装包的下载



![image-20231017180024346](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180024346.png)



#### SDK 下载

在 settings → Languages & Frameworks → Android SDK 选取即可

此处只是以 Android 13.0 作为示范 （起初已经安装了 Android 11.0）我使用的是 Android 11.0



![image-20231017180039008](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180039008.png)



![image-20231017180050165](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180050165.png)



#### 配置虚拟机

我们可以使用 ：

- Android Studio提供的Virtual Device （我使用的 ）
- Genymotion （EX:X.1 使用 Genymotion 创建虚拟机）

来创建虚拟机

我使用的是 Android Studio提供的Virtual Device

在 Device Manager 中根据提示创建相应系统 API 级别的虚拟机即可



![image-20231017180101411](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180101411.png)



### 1.2.2 创建第一个项目 HelloAndroid

#### 创建项目



![image-20231017180119664](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180119664.png)



![image-20231017180134900](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180134900.png)



#### Hello Android

修改  app → main → res → layout  中的 activity_main.xml



![image-20231017180148069](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180148069.png)



#### 启动



![image-20231017180205497](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180205497.png)

## 1.3. Android Studio 的基本使用

上面我们已经成功构建了 HelloAndroid 项目，但只是照猫画虎般的模仿，对具体的一些细节还是不熟悉，接下面我们将介绍Android Studio 的基本使用。

### 项目目录说明



Android Studio 有多种任务视图，不同视图文件上没有差异只是专注不用的场景，粗略的说每个视图类似于 Filter 过滤器可以让我们专注不同情景的开发情况，下面将对常用的 项目视图 和 Android 视图进行介绍。



![image-20231017180231463](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180231463.png)



#### 项目视图



![image-20231017180249318](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180249318.png)



1. 橙色显示的文件夹为 Gradle 构建之后生成的文件
2. 蓝色部分表示的为 源代码目录
3. 绿色部分为模块目录



我们着重对 app 模块下的各个文件夹以及文件进行讲解：



```text
├─androidTest
│  └─java
│      └─jz
│          └─init
│              └─runoob_study
├─main （用于存放源代码目录以及 classpath: 资源文件目录）
│  ├─java
│  │  └─jz
│  │      └─init
│  │          └─runoob_study
│  │              ├─activity
│  │              └─service
│  └─res
│      ├─drawable （存放图片等资源）
│      ├─layout （存放布局文件）
│      ├─mipmap-anydpi
│      ├─mipmap-hdpi
│      ├─mipmap-mdpi   (xxx.mdpi 为显示适配文件)
│      ├─mipmap-xhdpi
│      ├─mipmap-xxhdpi
│      ├─mipmap-xxxhdpi
│      ├─values (常量)
│      ├─values-night
│      └─xml
└─test
    └─java
        └─jz
            └─init
                └─runoob_study

```



#### Android 视图



![image-20231017180302117](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180302117.png)





## X.1 使用 Genymotion 创建虚拟机

1. 官网下载 [Android Emulator on the Cloud and cross-platform - Genymotion](https://www.genymotion.com/)



![image-20231017180313196](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180313196.png)



![image-20231017180326524](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180326524.png)



Genmotion 需要 VirtulBox 为其提供虚拟环境如果我们没有安装 VirtualBox 可以选择第二个带有 VirtualBox 选项的安装器进行安装，反之~



1. 创建账户 （选择个人）



![image-20231017180337759](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180337759.png)



1. 创建虚拟机



![image-20231017180347220](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180347220.png)



1. 启动



![image-20231017180400061](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180400061.png)



## X.2 前后端分离开发模式

在 Android 中我们主要采用前后端分离开发模式。



![image-20231017180410858](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180410858.png)



---

前后端分离开发模式是指将网站或应用程序的前端和后端分别由不同的开发团队独立完成的开发模式。前端开发团队负责开发网站或应用程序的用户界面、交互和前端逻辑等，后端开发团队负责开发网站或应用程序的业务逻辑、数据存储和数据交互等。

前后端分离开发模式的优点包括：

1. 提高开发效率：前后端分离开发可以分别专注于不同的任务，提高开发效率。
2. 降低维护成本：前后端分离开发可以使得前后端代码更加独立和清晰，降低后期维护的成本。
3. 支持团队协作：前后端分离开发可以使得不同的开发团队独立完成自己的任务，便于团队之间的协作和沟通。

但是前后端分离开发也存在一些缺点，例如：

1. 技术难度较高：前后端分离开发需要不同的开发团队掌握不同的技术，技术难度较高。
2. 前后端协作难度较大：前后端分离开发需要不同的开发团队进行协作，协作难度较大。
3. 可维护性降低：前后端分离开发需要进行多次修改和升级，可维护性降低。

在前后端分离开发模式，数据的传输是一个非常重要的环节，通常会使用 JSON 格式来传输数据。以下是围绕数据传输从服务端和客服端两方面说明 Android 项目开发流程的步骤：

1. 数据的存储

在 Android 项目开发中，通常会使用 SharedPreferences 或 SQLite 数据库来存储数据。对于本地数据，我们可以直接从 SharedPreferences 中读取数据，对于需要持久化的数据，则需要使用 SQLite 数据库来进行存储。

1. 数据的解析

当我们从服务端获取数据时，通常会使用 JSON 格式进行传输。为了在 Android 项目中解析 JSON 数据，我们可以使用第三方库，例如 Gson 或 Jackson。这些库可以帮助我们将 JSON 数据解析成 Java 对象，方便我们进行数据处理和展示。

1. 数据的传输

在 Android 项目开发中，通常会使用 HTTP 协议来进行数据传输。对于服务端和客服端之间的数据传输，我们需要编写相应的 HTTP 客户端和服务端代码。服务端通常会使用 RESTful API 或者 websocket 协议来进行数据传输。在客服端，我们需要编写相应的 HTTP 客户端代码，来向服务端发送请求并获取响应数据。

1. 数据的展示

在 Android 项目开发中，数据的展示是非常重要的一环。通常会使用 UI 框架，例如 Activity、Fragment、ViewPager 等来进行数据的展示。对于数据的展示，我们可以使用数据绑定、ListView、RecyclerView 等方式来实现。

综上所述，Android 项目开发中围绕数据的传输（JSON）从服务端和客服端两方面，主要包括数据的存储、解析、传输和展示四个步骤。



## X.3 遇到的问题

### 默认项目中 Language 选项中没有 Java 选项

Android Studio 2023.x  创建项目过程中部分模板的 Language没有 Java 选项 （默认为 Kotlin ）

解决：

- 创建 No Activity项目
- 或者 🥹
- 创建 Empty Views Activity 项目



![image-20231017180423200](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180423200.png)

![image-20231017180432956](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180432956.png)



### Genymotion 安装过程中需要 C++ 2019 环境

[Latest supported Visual C++ Redistributable downloads | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)



![image-20231017180444044](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180444044.png)



### Genymotion 下载镜像过程中提示网络相关错误

科学上网，启动！



### VirtualBox 提示虚拟机启动失败 （NetWork Error）

> 修改网络模式为桥接 NAT



![image-20231017180454788](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180454788.png)

