# cmake project learn

## 1. what

```
什么是 CMake

CMake是一个跨平台的安装（编译）工具，可以用简单的语句来描述所有平台的安装(编译过程)。
他能够输出各种各样的makefile或者project文件，能测试编译器所支持的C++特性,类似UNIX下的automake。
只是 CMake 的组态档取名为 CMakeLists.txt。
Cmake 并不直接建构出最终的软件，而是产生标准的建构档（如 Unix 的 Makefile 或 Windows Visual C++ 的 projects/workspaces），然后再依一般的建构方式使用。
这使得熟悉某个集成开发环境（IDE）的开发者可以用标准的方式建构他的软件，
这种可以使用各平台的原生建构系统的能力是 CMake 和 SCons 等其他类似系统的区别之处。


All problems in computer science can be solved by another level of indirection.
David Wheeler
你或许听过好几种 Make 工具，
例如 GNU Make ，
QT 的 qmake ，
微软的 MS nmake，
BSD Make（pmake），
Makepp，等等。

这些 Make 工具遵循着不同的规范和标准，所执行的 Makefile 格式也千差万别。
这样就带来了一个严峻的问题：如果软件想跨平台，必须要保证能够在不同平台编译。
而如果使用上面的 Make 工具，就得为每一种标准写一次 Makefile ，这将是一件让人抓狂的工作。

CMake 就是针对上面问题所设计的工具：它首先允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。从而做到“Write once, run everywhere”。显然，CMake 是一个比上述几种 make 更高级的编译配置工具。一些使用 CMake 作为项目架构系统的知名开源项目有 VTK、ITK、KDE、OpenCV、OSG 等 [1]。

在 linux 平台下使用 CMake 生成 Makefile 并编译的流程如下：

编写 CMake 配置文件 CMakeLists.txt 。
执行命令 cmake PATH 或者 ccmake PATH 生成 Makefile 1 
1ccmake 和 cmake 的区别在于前者提供了一个交互式的界面。
。其中， PATH 是 CMakeLists.txt 所在的目录。
使用 make 命令进行编译。
本文将从实例入手，一步步讲解 CMake 的常见用法，文中所有的实例代码可以在这里找到。如果你读完仍觉得意犹未尽，可以继续学习我在文章末尾提供的其他资源。

```

## 2. how

```
入门案例：单个源文件

```

## 3. why

```

```

## refer

    https://www.hahack.com/codes/cmake/

    https://baike.baidu.com/item/cmake
