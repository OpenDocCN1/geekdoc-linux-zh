> > **重要提示**　使用会修改注册表的任何实用程序时，请确保在 64 位操作系统中运行的是实用程序的 64 位版本。32 位 x86 实用程序默认安装到 `C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools` 目录，64 位 x64 实用程序安装到 `C:\Program Files (x86)\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64` 目录。

结束程序集的开发和测试之后，要正式对其进行签名，以便打包和部署它。为了对程序集进行签名，要再次使用 SN.exe 实用程序，但这次换用 **-R** 开关，并指定包含了私钥的文件的名称。**-R** 开关指示 SN.exe 对文件内容进行哈希处理，用私钥对其进行签名，并将 RSA 数字签名嵌入文件中之前预留的空间。经过这一步之后，就可以部署完全签好的程序集。在开发和测试机器上，不要忘记使用 SN.exe 的 **-Vu** 或 **-Vx** 命令行开关来重新启用对这个程序集的验证。下面总结了使用延迟签名技术开发程序集的步骤。

+   1. 开发期间，获取只包含公司公钥的文件，使用 `/keyfile` 和 `/delaysign` 编译器开关编译程序集：
+   
+      ```text
+      csc /keyfile:MyCompany.PublicKey /delaysign MyAssembly.cs
+      ```

+   2. 生成程序集后执行以下命令，使 CLR 暂时信任程序集的内容，不对它进行哈希处理，也不对哈希值进行比较。该程序集能顺利安装到 GAC（如果有必要的话）。现在，可以生成引用了这个程序集的其他程序集，并可随意测试程序集。注意，在每台开发用的机器上，以下命令都只需执行一次，不必每次生成程序集都重复这一步：
+   
+      ```text
+      SN.exe -Vr MyAssembly.dll
+      ```

+   3. 准备好打包和部署程序集时，获取公司的私钥并执行以下命令。如果愿意，可以将这个新版本安装到 GAC 中。但只有先完成步骤 4，才能把它安装到 GAC 中。
+   
+      ```text
+      SN.exe -Ra MyAssembly.dll MyCompany.PrivateKey
+      ```

+   4. 为了在实际环境中测试，请执行以下命令，重新启用对这个程序集的验证：
+   
+      ```text
+      SN -Vu MyAssembly.dll
+      ```

本节开头就指出，大公司会将自己的密钥存储到硬件设备（比如智能卡）中。为了确保密钥的安全性，密钥值绝对不能固定存储在磁盘文件中。“加密服务提供程序”（Cryptographic Service Provider，CSP）提供了对这些密钥的位置进行抽象的容器。以 Microsoft 使用的 CSP 为例，一旦访问它提供的容器，就自动从一个硬件设备获取私钥。

如果公钥/私钥对在 CSP 容器中，必须为 CSC.exe、AL.exe 和 SN.exe 程序指定不同的开关。编译时（CSC.exe）指定 `/keycontainer` 开关而不是 `/keyfile` 开关；链接时（AL.exe）指定 `/keyname` 开关而不是 `/keyfile` 开关；使用强名称程序（SN.exe）对延迟签名的程序集进行重新签名时，指定 **-Rc** 开关而不是 **-R** 开关。SN.exe 提供了另外几个开关让开发人员与 CSP 互动。