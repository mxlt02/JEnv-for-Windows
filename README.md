# JEnv for Windows 版本 2 已经发布
汉化了一下， jdk8官网只有安装包 可以看这个弄绿色版https://www.jianshu.com/p/d64d961af945
### 完全重写 V.1 版本

## 用 3 个单词更改当前的 Java 版本

- JEnv 允许您更改当前的 JDK 版本。
- 这对于测试或需要不同版本 Java 的项目非常有用。
- 例如，您可以构建一个需要 Java8 的 Gradle 项目，而不必更改环境变量，然后切换回使用 Java15 进行工作。
- 它是用 cmd 和 powershell 编写的，因此可以更改环境变量并可在任何 Windows-10+ 上运行。

希望您喜欢它。如果您喜欢我的工作，请给我一个 star。谢谢！

# 视频演示:



![https://user-images.githubusercontent.com/55546882/162501231-b2e030bf-1194-4a1d-8565-ccd503b63402.svg](https://user-images.githubusercontent.com/55546882/162501231-b2e030bf-1194-4a1d-8565-ccd503b63402.svg)





## 安装

1. **克隆此存储库**
2. **将其添加到路径**
3. **运行 `jenv` 一次以便脚本可以完成其余部分**
4. **如果您使用 cmd，则需要调用批处理文件。如果您使用 PowerShell，则应调用 /src/jenv.ps1**
5. **一些人报告将 JEnv 放入其 C:/Programs 文件夹中时出现问题，因为需要管理员权限**
6. **希望我能帮到您。否则请打开一个 issue**

## 警告:

有时需要在指定本地 jenv 的新目录中调用 jenv。这将为当前 shell 设置您的 JAVA_HOME，并确保 Maven 等工具正常工作。

## 用法 (注意: local 会覆盖 change，使用前请覆盖 local)

1. **添加新的 Java 环境 (需要绝对路径)**
   *jenv add `<name> <path>`*
   例如: `jenv add jdk15 D:\Programme\Java\jdk-15.0.1`
2. **更改当前会话的 Java 版本**
   *jenv use `<name>`*
   例如: `jenv use jdk15`
   脚本环境变量:
   —PowerShell: `$ENV:JENVUSE="jdk17"`
   —CMD/BATCH: `set "JENVUSE=jdk17"`
3. **清除当前会话的 Java 版本**
   *jenv use remove*
   例如: `jenv use remove`
   脚本环境变量:
   —PowerShell: `$ENV:JENVUSE=$null`
   —CMD/BATCH: `set "JENVUSE="`
4. **全局更改 Java 版本**
   *jenv change `<name>`*
   例如: `jenv change jdk15`
5. **始终在此文件夹中使用此 Java 版本**
   *jenv local `<name>`*
   例如: `jenv local jdk15  `
6. **清除此文件夹的 Java 版本**
   *jenv local remove*
   例如: `jenv local remove`
7. **列出所有 Java 环境**
   *jenv list*
   例如: `jenv list`
8. **从 JEnv 列表中删除现有 JDK**
   *jenv remove `<name>`*
   例如: `jenv remove jdk15`
9. **启用 javac、javaw 或其他位于 java 目录中的可执行文件**
   *jenv link `<Executable name>`*
   例如: `jenv link javac`
10. **卸载jenv并自动恢复您选择的Java版本**
    *jenv uninstall `<名称>`*
    示例：`jenv uninstall jdk17`
11. **自动搜索要添加的Java版本**
    *jenv autoscan [–yes|-y] `?<路径>?`*
    示例：`jenv autoscan "C:\Program Files\Java"`
    示例：`jenv autoscan` // 将搜索整个系统 示例：`jenv autoscan -y "C:\Program Files\Java"` // 将接受默认值

## 这是如何工作的？

此脚本创建一个java.bat文件，该文件使用正确的版本调用java.exe 当ps脚本更改环境变量时，它们会被导出到tmp文件并由批处理文件应用 添加了PowerShell脚本的附加参数。"–output"别名为"-o"将为批处理创建tmp文件。请参见下面的图像

## 贡献

如果您想做出贡献，请随意这样做。对于初学者来说，这是一个很好的存储库，因为代码量不大，您可以很容易地理解它的工作原理。
要运行测试，建议您使用最新版本的powershell（pwsh.exe）：
https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.2
请注意，您必须将其作为pwsh而不是powershell运行
然后，您必须安装Pester。这仅用于测试：`Install-Module -Name Pester -Force -SkipPublisherCheck`
您也可以使用已安装的powershell。但是，它已经安装了一个旧的Pester模块，您无法使用它，我无法弄清楚如何更新它：https://github.com/pester/Pester/issues/1201
导航到测试文件夹并运行`test.ps1`文件。它将在测试时备份您的环境变量和jenv配置，并在以后自动恢复它们。但是，您应始终让测试完成，否则您的变量和配置将不会被恢复。
