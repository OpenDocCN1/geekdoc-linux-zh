
        ```
        
        ## 匿名...
        ...
        ```
        
        ls -d /var/ftp
        
        ```
        
        这看起来像是原文中已经把代码块写成了 ``` 单独一行。我需要确保最终输出是标准的 Markdown 代码块。
        
    *   特别注意：原文中有些代码块被拆分了，例如：
        ```
        [ftp]
        ```
        ```
        path = ...
        ```
        这需要合并为一个代码块或者确保语法正确。`[ftp]` 是配置文件的 section，`path = ...` 是内容。通常应该放在同一个代码块里，或者作为文本描述。根据上下文，“这里显示了一个用于匿名访问的 FTP 模块示例：”，后面跟着 `[ftp]` 和 `path...`。最好合并为一个代码块。

3.  **去除星号/斜体**：
    *   检查是否有 `**` 或 `*` 包围变量，如果有，去掉星号加反引号。
    *   原文中 `--progress` 前面没有星号，但描述中说 “--progress` 选项”，看起来原文可能丢失了开头的反引号或者格式错误。需修正为 `` `--progress` ``。

4.  **详细处理步骤**：

    *   **Part 1: 匿名 FTP 目录**
        *   标题：`## 匿名 FTP 服务器目录` (保留层级，或者提升为 `###` 如果上面有 `#`。鉴于下面有 `# 第 22 章`，我将暂时保留原文层级，稍后统一调整。实际上，原文第一个标题是 `##`，后面出现 `#`。这意味着文档结构可能是：章节 (`#`) -> 节 (`##`)。
        *   文本处理：
            *   `/var` -> `/var`
            *   `ftp` -> `ftp`
            *   `ls` -> `ls`
            *   `/bin` -> `/bin`
            *   `vsftpd`, `ProFTPD` -> `vsftpd`, `ProFTPD`
            *   `root`, `ftp` -> `root`, `ftp`
            *   `ls -d` -> `ls -d`
            *   代码块 `ls -d /var/ftp` 规范化。
            *   `chown` -> `chown`
            *   代码块 `chown root:root /var/ftp` 规范化。
            *   `bin`, `ftp` -> `bin`, `ftp`
            *   `/bin` -> `/bin`
            *   `ls` -> `ls`
            *   `chmod` -> `chmod`

    *   **Part 2: 章节标题修正**
        *   原文：`# 第 22 章：FTP 服务器 427`
        *   处理：去除 `427`。保留 `# 第 22 章：FTP 服务器`。
        *   原文：`## 匿名 FTP 文件` -> 保留 `##`。
        *   内容：`pub`, `README`, `INDEX`, `/var/ftp`, `pub` -> 加反引号。

    *   **Part 3: rsync 使用**
        *   `## 使用 rsync 使用 FTP` (标题有点怪，原文如此，保留)。
        *   `rsync` -> `rsync`。
        *   `## 使用 rsync 访问 FTP 站点`
        *   `mytrek.com`, `myproject` -> `mytrek.com`, `myproject`。
        *   代码块 `rsync mytrek.com::/var/ftp/pub/myproject /home/myproject`。
        *   `/etc/rsync.conf` -> `/etc/rsync.conf`。
        *   代码块 `rsync mytrek.com::`。
        *   `ftp` -> `ftp`。
        *   `-r` -> `-r`。
        *   代码块 `rsync -r mytrek.com::ftp`。

    *   **Part 4: 第六部分**
        *   `# 第六部分：互联网与网络服务`。
        *   内容：`rsync`, `ibiblio`, `fedora-linux-core`, `Fedora` -> 加反引号。
        *   URL/命令 `rsync://distro.ibiblio.org/fedora-linux-core/` -> 加反引号。
        *   描述：“--progress` 选项...” -> 修正为 “`--progress` 选项...”。
        *   代码块 `rsync -a --progress rsync://...`。

    *   **Part 5: 配置 rsync**
        *   `# 配置 rsync 服务器` (原文是 `#`，保持)。
        *   `chkconfig`, `sys-rc-conf`, `rsync`, `xinetd`, `/etc/xinetd.d`, `rsync` -> 加反引号。
        *   代码块 `chkconfig rsync on`。
        *   `/etc/rsyncd.conf` -> `/etc/rsyncd.conf`。
        *   `[ftp]`, `path`, `uid`, `gid`, `nobody` -> 加反引号。
        *   代码块合并：
            ```
            [ftp]
            path = /var/ftp/pub
            comment = ftp site
            ```
        *   `auth`, `rsync`, `/etc/rsyncd.secrets` -> 加反引号。
        *   代码块（秘密文件内容）：
            ```
            aleina:mypass3
            larisa:your5
            ```
        *   代码块（模块示例）：
            ```
            [specialftp]
            path = /var/projects/special
            command = restricted access
            auth users = aleina,larisa
            secrets file = /etc/rsyncd.secrets
            ```
            *注意：原文中 `command` 在 rsync.conf 中不是标准字段，通常是 `max connections` 等，但作为文档工程师，我不修改语义，只排版。原文写的是 `command = restricted access`，照录。*

    *   **Part 6: 第 22 章 (重复?) 与 查看模块**
        *   `# 第 22 章：FTP 服务器` (再次出现)。这可能是一个新的部分，或者原文结构混乱。鉴于前面已经有一个 `# 第 22 章`，这里可能是 PDF 提取错误，将章节标题在页面顶部重复了。但在 Markdown 排版中，如果中间穿插了内容，我们通常保留，或者如果它是纯噪声则删除。看内容：“如果你位于一个 FTP 服务器上并想查看哪些模块可用...”。这部分内容其实属于 rsync 的使用。
        *   为了逻辑清晰，我将把这部分归并入之前的 `# 配置 rsync 服务器` 或 `# 第六部分` 下，或者保留 `## 查看可用模块` 这样的小节标题，去掉重复的章节大标题 `# 第 22 章：FTP 服务器`，因为它显然是页眉残留。
        *   *修正策略*：原文中 `# 第 22 章：FTP 服务器` 出现在 `rsync 镜像` 之前。而前面已经出现过一次。考虑到 `# 第六部分` 也在中间，这很可能是一本 PDF 书的线性提取。
        *   为了“重新划分标题层级”并“保留核心内容”，我会：
            *   保留第一个 `# 第 22 章：FTP 服务器` (去噪 427)。
            *   后续的 `# 第 22 章：FTP 服务器` (在 rsync 镜像前) 很可能是页眉。如果我删除它，逻辑更通顺。但规则说“保留正文核心内容”。标题算核心吗？通常页眉不算正文。但如果是章节开始，算。
            *   观察上下文：`rsync 镜像` 是 `#` 级别。它前面是 `# 第 22 章...`。
            *   我将假设文档结构是：
                *   `# 第六部分...`
                *   `## 使用 rsync...`
                *   `## 配置 rsync...`
                *   `## rsync 镜像` (原 `#` 降级或保持？原文是 `#`。在 `# 第六部分` 下，应该是 `##`。但如果 `# 第六部分` 是书的大结构，而 `# 第 22 章` 是章，那 `rsync 镜像` 应该是章内的节，即 `##`。)
            *   让我们简化：将主要技术节设为 `##`，大结构设为 `#`。
            *   删除明显的页眉残留 `# 第 22 章：FTP 服务器` (出现在 rsync 镜像前那个)，因为它紧跟在一大段配置文本后，且没有新的章节迹象，更像是页眉。
            *   将 `# rsync 镜像` 调整为 `## rsync 镜像`，使其隶属于之前的章节或作为独立节。考虑到它前面有 `# 第六部分`，`rsync 镜像` 作为 `##` 是合适的。

    *   **Part 7: rsync 镜像**
        *   内容：`mytrek`, `ftp`, `/var/ftp/mirror/mytrek` -> 加反引号。
        *   代码块：`rsync -a --delete ftp.mytrek.com:ftp /var/ftp/mirror/mytrek`。

5.  **最终检查**：
    *   变量/命令/路径/文件名均已加反引号。
    *   代码块已规范。
    *   标题层级合理。
    *   无多余空行。

**具体实施细节**：

*   **标题层级调整**：
    *   `# 第六部分：互联网与网络服务` -> `#`
    *   `## 匿名 FTP 服务器目录` -> `##`
    *   `## 匿名 FTP 文件` -> `##`
    *   `## 使用 rsync 使用 FTP` -> `##`
    *   `## 使用 rsync 访问 FTP 站点` -> `##`
    *   `# 配置 rsync 服务器` -> `##` (因为它在 `# 第六部分` 下)
    *   `# 第 22 章：FTP 服务器` (第一次出现，带 427) -> 这是章节标题，设为 `#`。但它在 `## 匿名...` 之后？这顺序不对。
    *   让我们看原文顺序：
        1. `## 匿名 FTP 服务器目录` ... 内容 ...
        2. `# 第 22 章：FTP 服务器 427` (页眉噪声 + 章节标题)
        3. `## 匿名 FTP 文件`
        4. `## 使用 rsync 使用 FTP`
        5. `## 使用 rsync 访问 FTP 站点`
        6. `# 第六部分：互联网与网络服务` (大标题)
        7. 内容...
        8. `# 配置 rsync 服务器`
        9. 内容...
        10. `# 第 22 章：FTP 服务器` (页眉噪声)
        11. `# rsync 镜像`

    *   **重构逻辑**：
        原文本似乎是两本书或两个大章节的混合，或者 PDF 提取乱了。
        “第 22 章：FTP 服务器” 和 “第六部分：互联网与网络服务” 可能是同一本书的不同层级。
        通常 “第六部分” > “第 22 章”。
        但原文中 `## 匿名...` 在 `# 第 22 章` 之前出现。
        
        最安全的做法：尊重原文的顺序，但规范化标题层级。
        1. 将 `# 第 22 章：FTP 服务器` (带 427) 视为章节开始。前面的 `## 匿名 FTP 服务器目录` 可能是上一章的结尾或本章的开篇但标题写错了。
        2. 鉴于用户要求“重新划分标题层级”，我有权调整。
        3. 我决定：
            *   `#` 用于主要章节（第22章、第六部分）。
            *   `##` 用于小节（匿名目录、rsync使用、配置、镜像）。
            *   删除“427”和重复的页眉“# 第 22 章...”。
            *   将 `# 配置 rsync 服务器` 降为 `##`。
            *   将 `# rsync 镜像` 降为 `##`。
            *   开头的 `## 匿名 FTP 服务器目录` 保持不变 `##`，因为它在 `# 第 22 章` 出现之前？不，原文中 `# 第 22 章...` 在 `## 匿名 FTP 文件` 之前。
            *   等等，原文第一段是 `## 匿名 FTP 服务器目录`。然后是 `# 第 22 章...`。然后是 `## 匿名 FTP 文件`。
            *   这表明 `## 匿名 FTP 服务器目录` 可能属于前一章，或者排版错位。
            *   为了清晰，我将 `# 第 22 章：FTP 服务器` 作为本章起点。如果 `## 匿名 FTP 服务器目录` 在其后，则它是本章第一节。如果在先前，它可能是前一章的剩余。
            *   看内容：“如前所述，FTP 主目录命名为 `ftp`...”。这像是在承接上文。
            *   我将保留原文顺序，但将 `# 第 22 章：FTP 服务器` 放在它出现的位置，设为 `#`。后面的 `##` 设为 `##`。
            *   `# 第六部分` 设为 `#`。
            *   `# 配置 rsync 服务器` 设为 `##` (在第六部分下)。
            *   `# rsync 镜像` 设为 `##`。
            *   中间重复的 `# 第 22 章：FTP 服务器` (无页码) 视为噪声删除。

    *   **代码块合并**：
        *   原文中配置文件的代码块被拆分：
            ```
            [ftp]
            ```
            ```
            path = /var/ftp/pub
            ...
            ```
            我会合并为一个代码块。

    *   **变量加反引号细节**：
        *   `ls` -> `ls`
        *   `/bin` -> `/bin`
        *   `vsftpd` -> `vsftpd`
        *   `ProFTPD` -> `ProFTPD`
        *   `root` -> `root`
        *   `ftp` -> `ftp`
        *   `ls -d` -> `ls -d`
        *   `chown` -> `chown`
        *   `pub` -> `pub`
        *   `README` -> `README`
        *   `INDEX` -> `INDEX`
        *   `rsync` -> `rsync`
        *   `mytrek.com` -> `mytrek.com`
        *   `myproject` -> `myproject`
        *   `/etc/rsync.conf` -> `/etc/rsync.conf`
        *   `-r` -> `-r`
        *   `ibiblio` -> `ibiblio`
        *   `fedora-linux-core` -> `fedora-linux-core`
        *   `Fedora` -> `Fedora` (作为发行版名，通常斜体或粗体，但规则说变量名加反引号，Fedora 是专有名词，不是变量。但规则说“所有单独出现的变量名...”。Fedora 不是变量。但 `fc7-i386-discl.iso` 是文件名。`rsync://...` 是 URL/命令。)
        *   规则：“所有单独出现的变量名...路径名...命令名...”。
        *   `Fedora` 是系统名，不加反引号？通常文档中系统名不加反引号，或者加粗。规则没提系统名。但 `ISO 镜像` 是普通词。
        *   `--progress` -> `--progress` (选项名，属于命令参数，视作命令的一部分或独立参数，加反引号)。
        *   `chkconfig` -> `chkconfig`
        *   `sys-rc-conf` -> `sys-rc-conf`
        *   `xinetd` -> `xinetd`
        *   `/etc/xinetd.d` -> `/etc/xinetd.d`
        *   `/etc/rsyncd.conf` -> `/etc/rsyncd.conf`
        *   `[ftp]` -> `[ftp]` (配置项，加反引号)
        *   `path` -> `path`
        *   `uid` -> `uid`
        *   `gid` -> `gid`
        *   `nobody` -> `nobody`
        *   `auth` -> `auth`
        *   `/etc/rsyncd.secrets` -> `/etc/rsyncd.secrets`
        *   `aleina` -> `aleina` (用户名，视作变量/标识符？通常用户名在代码块里才重要。正文中提到的用户名 `aleina`，加反引号更清晰。)
        *   `localhost` -> `localhost`
        *   `mytrek` -> `mytrek`
        *   `/var/ftp/mirror/mytrek` -> `/var/ftp/mirror/mytrek`
        *   `ftp.mytrek.com` -> `ftp.mytrek.com`

    *   **关于“去掉星号再加反引号”**：
        *   原文中 `--progress` 之前没有星号。
        *   检查是否有 `**` 或 `*`。原文似乎没有。

    *   **关于代码块**：
        *   原文中代码块是 ` ``` ` 单独成行。
        *   我需要把它们变成标准的：
            ```
            code
            ```

    *   **标题“第 22 章：FTP 服务器 427”**：
        *   改为 `# 第 22 章：FTP 服务器`。

    *   **标题“第六部分：互联网与网络服务”**：
        *   改为 `# 第六部分：互联网与网络服务`。

    *   **标题“配置 rsync 服务器”**：
        *   原文是 `#`。在 `# 第六部分` 下，应为 `##`。

    *   **标题“rsync 镜像”**：
        *   原文是 `#`。在 `# 第六部分` 下，应为 `##`。

    *   **标题“第 22 章：FTP 服务器” (第二次出现)**：
        *   位于 `rsync 镜像` 标题前。显然是页眉。删除。

    *   **标题“匿名 FTP 服务器目录”**：
        *   原文 `##`。保留。

    *   **标题“匿名 FTP 文件”**：
        *   原文 `##`。保留。

    *   **标题“使用 rsync 使用 FTP”**：
        *   原文 `##`。保留。

    *   **标题“使用 rsync 访问 FTP 站点”**：
        *   原文 `##`。保留。

    *   **整合**：

    ```markdown
    # 第 22 章：FTP 服务器
    
    ## 匿名 FTP 服务器目录
    
    如前所述，FTP 主目录命名为 `ftp` 并放置在 `/var` 目录下。当用户匿名登录时，保护系统的一个重要部分是防止远程用户使用限制目录之外的任何命令或程序。例如，你不会让用户使用 `ls` 命令列出文件名，因为 `ls` 位于你的 `/bin` 目录中。同时，你希望让 FTP 用户能够使用 `ls` 命令列出文件名。新的 FTP 守护进程（如 `vsftpd` 和 `ProFTPD`）通过创建对系统命令和文件的访问，同时将远程用户限制在 FTP 站点的目录内来解决这个问题。此外，确保 FTP 主目录属于 `root` 用户，而不是 `ftp` 用户。使用 `ls -d` 命令检查 FTP 目录的所有权。

    ```bash
    ls -d /var/ftp
    ```
    
    要更改目录的所有权，你使用 `chown` 命令，如示例所示：

    ```bash
    chown root:root /var/ftp
    ```
    
    另一种传统做法是创建远程用户所需的常用系统目录和文件的副本，并将它们放置在用户可以访问的 `ftp` 目录中。一个 `bin` 目录被放置在 `ftp` 目录中并将远程用户限制其中，而不是系统的 `bin` 目录。每当他们使用 `ls` 命令时，远程用户使用的都是你放在 `/bin` 中的那一个。例如，如果你自己设置匿名 FTP 目录，你必须使用 `chmod` 命令更改远程用户无法访问的目录访问权限。

    ## 匿名 FTP 文件
    
    位于 FTP 主目录的名为 `pub` 的目录通常存放你供远程用户下载的文件。当 FTP 用户登录时，他们被放置在 FTP 主目录（`/var/ftp`），然后他们可以访问 `pub` 目录。在 `pub` 目录下的每个存放 FTP 文件的子目录中，你应该创建一个 `README` 文件和一个 `INDEX` 文件，以方便 FTP 用户。`README` 文件包含该目录下文件的简要描述。`INDEX` 文件包含文件列表以及每个文件的功能描述。

    ## 使用 rsync 使用 FTP
    
    许多 FTP 服务器支持使用 `rsync` 进程进行 `rsync` 操作。这允许从 FTP 服务器进行智能增量更新。你可以更新目录或单个文件（例如大型 ISO 镜像）。

    ## 使用 rsync 访问 FTP 站点
    
    要访问运行 `rsync` 的 FTP 服务器，输入 `rsync` 命令，主机名后输入双冒号，然后输入你想访问的目录路径或 FTP 服务器的模块之一。在以下示例中，用户从 `mytrek.com` FTP 站点更新本地的 `myproject` 目录：

    ```bash
    rsync mytrek.com::/var/ftp/pub/myproject /home/myproject
    ```
    
    要确定哪些目录支持 `rsync`，请检查该站点上的 `rsync` 模块。这些由站点的 `/etc/rsync.conf` 配置文件定义。一个模块只是包含其所有子目录的目录。要查找可用的模块，你输入 FTP 站点加双冒号。

    ```bash
    rsync mytrek.com::
    ```
    
    这会告诉你 `mytrek.com` 站点有一个 `ftp` 模块。要列出模块中的文件和目录，你可以使用 `rsync` 命令配合 `-r` 选项。

    ```bash
    rsync -r mytrek.com::ftp
    ```

    # 第六部分：互联网与网络服务
    
    许多运行 `rsync` 服务器的站点，其 `rsync` 协议可能已设置为访问可用的 `rsync` 模块（目录）。例如，可以使用以下 URL 配合 `rsync` 访问你所在 Linux 发行版的 `ibiblio` 位置。对于 `Fedora`，该模块命名为 `fedora-linux-core`，紧跟在主机名之后。

    ```bash
    rsync://distro.ibiblio.org/fedora-linux-core/
    ```
    
    你可以使用 `rsync` 更新单个文件，例如可能已经更改的 ISO 镜像。以下示例更新了 `Fedora` 7 ISO 磁盘。`--progress` 选项将显示下载进度。

    ```bash
    rsync -a --progress rsync://distro.ibiblio.org/fedora-linux-core/7/i386/iso/fc7-i386-discl.iso
    ```

    ## 配置 rsync 服务器
    
    为了配置你的 FTP 服务器以允许客户端在你的站点上运行 `rsync`，你首先需要以服务器模式运行 `rsync`。使用 `chkconfig` 或 `sys-rc-conf` 开启 `rsync` 守护进程（通常称为 `rsync`）。你通过 `xinetd` 运行 `rsync` 守护进程，使用 `/etc/xinetd.d` 中的 `rsync` 脚本来启动它并设置参数。

    ```bash
    chkconfig rsync on
    ```
    
    当作为守护进程运行时，`rsync` 会读取 `/etc/rsyncd.conf` 文件来获取配置选项。你可以指定 FTP 选项，例如 FTP 站点文件的位置。配置文件被划分为多个模块，每个模块都有自己的选项。模块是条目（目录及其子目录）的符号表示。模块名包含在括号中，例如用于 FTP 模块的 `[ftp]`。然后你可以为模块输入选项，比如通过使用 `path` 选项指定你 FTP 站点目录和文件的位置。用户 ID 和组 ID 可以通过 `uid` 和 `gid` 选项指定。默认值是 `nobody`。这里显示了一个用于匿名访问的 FTP 模块示例：

    ```bash
    [ftp]
    path = /var/ftp/pub
    comment = ftp site
    ```
    
    对于更严格的访问，你可以添加 `auth` 选项来指定授权用户；`rsync` 默认允许所有用户匿名访问。使用 `rsync` 访问 FTP 站点上的区域可以通过密码文件（如 `/etc/rsyncd.secrets`）进行进一步控制。这是一个冒号分隔的用户名和密码列表。

    ```bash
    aleina:mypass3
    larisa:your5
    ```
    
    与受控区域对应的模块看起来如下：

    ```bash
    [specialftp]
    path = /var/projects/special
    command = restricted access
    auth users = aleina,larisa
    secrets file = /etc/rsyncd.secrets
    ```

    ## rsync 镜像
    
    如果你位于一个 FTP 服务器上并想查看哪些模块可用，可以运行带有 `localhost` 选项的 `rsync`，且双冒号后不跟跟任何内容。

    ```bash
    $ rsync localhost::
    ftp
    specialftp
    ```
    
    远程用户只需通过输入你的主机名和双冒号即可知道你拥有哪些模块。

    ```bash
    rsync mytrek.com::
    ```
    
    某些站点允许你使用 `rsync` 执行镜像操作。通过 `rsync`，你不需要复制整个站点，只需复制那些更改的文件。以下示例将 `mytrek` FTP 站点镜像到本地站点的 `/var/ftp/mirror/mytrek` 目录。

    ```bash
    rsync -a --delete ftp.mytrek.com:ftp /var/ftp/mirror/mytrek
    ```
    ```

    *Self-Correction on Title Hierarchy*:
    The original text had `# 第 22 章...` *after* `## 匿名 FTP 服务器目录`. This suggests the first part belongs to the same chapter. I will place `# 第 22 章：FTP 服务器` at the very top, encompassing the first sections.
    Then `# 第六部分...` starts a new major section.
    Then `## 配置 rsync 服务器` and `## rsync 镜像` are subsections of Part 6? Or are they still Part of Chapter 22?
    Usually, "Part" contains "Chapters". "Chapter" contains "Sections".
    If the document is a chapter within a part, the structure might be:
    # Part 6
    ## Chapter 22
    ### Section 1
    ### Section 2
    
    However, the input text mixes them.
    `## 匿名...` -> `# 第 22 章` -> `## 匿名...` -> `# 第六部分`.
    This is confusing.
    Let's look at the flow.
    1. Anonymous FTP stuff.
    2. Chapter 22 header appears.
    3. Anonymous FTP Files.
    4. Rsync usage.
    5. Part 6 header appears.
    6. More Rsync usage (URLs).
    7. Rsync Config.
    8. Rsync Mirror.
    
    It is highly likely that "Chapter 22" is the context for the first half, and "Part 6" is the context for the second half (or the whole thing is from a book where Part 6 contains Chapter 22, but the headers are scattered).
    
    Given the instruction "Re-divide title levels", I will create a logical hierarchy:
    If "Part 6" is the highest level present, I'll use `#` for it.
    If "Chapter 22" is inside Part 6, it should be `##`.
    But the text flows linearly.
    
    Alternative interpretation: The text provided is a raw dump.
    I will use:
    `#` for major divisions (Chapter 22, Part 6).
    `##` for sections (Anonymous FTP, Rsync Usage, Config, Mirror).
    
    I will place `# 第 22 章：FTP 服务器` at the start (removing 427).
    I will place `# 第六部分：互联网与网络服务` where it appears.
    I will make `## 匿名...`, `## 使用...`, `## 配置...`, `## 镜像` be `##` level.
    
    Wait, if `# 第六部分` appears in the middle, it implies a structural break.
    
    Let's stick to the visible structure but clean it up:
    1. `# 第 22 章：FTP 服务器` (Top level)
    2. `## 匿名 FTP 服务器目录`
    3. `## 匿名 FTP 文件`
    4. `## 使用 rsync 使用 FTP`
    5. `## 使用 rsync 访问 FTP 站点`
    6. `# 第六部分：互联网与网络服务` (Top level, indicating a new major section in the source book)
    7. (Text about rsync URLs) -> No header? It falls under Part 6. Maybe I should infer a header or just keep it as text. The original text has no header for the "ibiblio" section, it just follows Part 6 header.
    8. `## 配置 rsync 服务器` (Subsection of Part 6? Or Chapter 22? It's under Part 6 in the flow).
    9. `## rsync 镜像`
    
    This seems the most faithful representation of the provided text flow, just correcting the levels to be consistent (Chapters/Parts are `#`, Sections are `##`).

    One detail: The text "如果你位于一个 FTP 服务器上并想查看哪些模块可用..." in the original text was under a repeated `# 第 22 章` header. I will remove that repeated header and fold that content into the flow. It looks like general rsync usage info. It fits well before or within the "Rsync Mirror" or "Config" section. In the original, it was between Config and Mirror. I will keep it there but without the junk header. Actually, looking closely, that block "如果你位于... $ rsync localhost::" is about *checking* modules. It's a specific example. I will put it in a small section or just leave it as text under the relevant `##` header. The original had `# 第 22 章` then `# rsync 镜像`. I will make `## 查看可用模块`? No, I shouldn't invent headers unless necessary. I will keep the text flowing under `## 配置 rsync 服务器` or create a `## 查看可用模块` if it seems distinct.
    Original structure:
    - Config
    - [Junk Header]
    - Text: Check modules locally (`$ rsync localhost::`)
    - Text: Remote users check modules (`rsync mytrek.com::`)
    - Header: `# rsync 镜像`
    
    I will keep the text as is, perhaps under `## 配置 rsync 服务器` or a new `## 查看可用模块`?
    To be safe and not add semantic headers not in the main structure, I will just let the text flow.
    Actually, `# rsync 镜像` is clearly a new section.
    The text before it "Check modules" is a procedure.
    I will stick to the main headers provided in the input (`##` or `#`), cleaning up the obvious page headers.

    Final check on code blocks:
    - `chkconfig rsync on`
    - Config files `[ftp] ...`
    - Secrets file
    - `[specialftp] ...`
    - `$ rsync localhost:: ...`
    - `rsync mytrek.com::`
    - `rsync -a --delete ...`

    All good.

[content]
# 第 22 章：FTP 服务器

## 匿名 FTP 服务器目录

如前所述，FTP 主目录命名为 `ftp` 并放置在 `/var` 目录下。当用户匿名登录时，保护系统的一个重要部分是防止远程用户使用限制目录之外的任何命令或程序。例如，你不会让用户使用 `ls` 命令列出文件名，因为 `ls` 位于你的 `/bin` 目录中。同时，你希望让 FTP 用户能够使用 `ls` 命令列出文件名。新的 FTP 守护进程（如 `vsftpd` 和 `ProFTPD`）通过创建对系统命令和文件的访问，同时将远程用户限制在 FTP 站点的目录内来解决这个问题。此外，确保 FTP 主目录属于 `root` 用户，而不是 `ftp` 用户。使用 `ls -d` 命令检查 FTP 目录的所有权。

```bash
ls -d /var/ftp
```

要更改目录的所有权，你使用 `chown` 命令，如示例所示：

```bash
chown root:root /var/ftp
```

另一种传统做法是创建远程用户所需的常用系统目录和文件的副本，并将它们放置在用户可以访问的 `ftp` 目录中。一个 `bin` 目录被放置在 `ftp` 目录中并将远程用户限制其中，而不是系统的 `bin` 目录。每当他们使用 `ls` 命令时，远程用户使用的都是你放在 `/bin` 中的那一个。例如，如果你自己设置匿名 FTP 目录，你必须使用 `chmod` 命令更改远程用户无法访问的目录访问权限。

## 匿名 FTP 文件

位于 FTP 主目录的名为 `pub` 的目录通常存放你供远程用户下载的文件。当 FTP 用户登录时，他们被放置在 FTP 主目录（`/var/ftp`），然后他们可以访问 `pub` 目录。在 `pub` 目录下的每个存放 FTP 文件的子目录中，你应该创建一个 `README` 文件和一个 `INDEX` 文件，以方便 FTP 用户。`README` 文件包含该目录下文件的简要描述。`INDEX` 文件包含文件列表以及每个文件的功能描述。

## 使用 rsync 使用 FTP

许多 FTP 服务器支持使用 `rsync` 进程进行 `rsync` 操作。这允许从 FTP 服务器进行智能增量更新。你可以更新目录或单个文件（例如大型 ISO 镜像）。

## 使用 rsync 访问 FTP 站点

要访问运行 `rsync` 的 FTP 服务器，输入 `rsync` 命令，主机名后输入双冒号，然后输入你想访问的目录路径或 FTP 服务器的模块之一。在以下示例中，用户从 `mytrek.com` FTP 站点更新本地的 `myproject` 目录：

```bash
rsync mytrek.com::/var/ftp/pub/myproject /home/myproject
```

要确定哪些目录支持 `rsync`，请检查该站点上的 `rsync` 模块。这些由站点的 `/etc/rsync.conf` 配置文件定义。一个模块只是包含其所有子目录的目录。要查找可用的模块，你输入 FTP 站点加双冒号。

```bash
rsync mytrek.com::
```

这会告诉你 `mytrek.com` 站点有一个 `ftp` 模块。要列出模块中的文件和目录，你可以使用 `rsync` 命令配合 `-r` 选项。

```bash
rsync -r mytrek.com::ftp
```

# 第六部分：互联网与网络服务

许多运行 `rsync` 服务器的站点，其 `rsync` 协议可能已设置为访问可用的 `rsync` 模块（目录）。例如，可以使用以下 URL 配合 `rsync` 访问你所在 Linux 发行版的 `ibiblio` 位置。对于 `Fedora`，该模块命名为 `fedora-linux-core`，紧跟在主机名之后。

```bash
rsync://distro.ibiblio.org/fedora-linux-core/
```

你可以使用 `rsync` 更新单个文件，例如可能已经更改的 ISO 镜像。以下示例更新了 `Fedora` 7 ISO 磁盘。`--progress` 选项将显示下载进度。

```bash
rsync -a --progress rsync://distro.ibiblio.org/fedora-linux-core/7/i386/iso/fc7-i386-discl.iso
```

## 配置 rsync 服务器

为了配置你的 FTP 服务器以允许客户端在你的站点上运行 `rsync`，你首先需要以服务器模式运行 `rsync`。使用 `chkconfig` 或 `sys-rc-conf` 开启 `rsync` 守护进程（通常称为 `rsync`）。你通过 `xinetd` 运行 `rsync` 守护进程，使用 `/etc/xinetd.d` 中的 `rsync` 脚本来启动它并设置参数。

```bash
chkconfig rsync on
```

当作为守护进程运行时，`rsync` 会读取 `/etc/rsyncd.conf` 文件来获取配置选项。你可以指定 FTP 选项，例如 FTP 站点文件的位置。配置文件被划分为多个模块，每个模块都有自己的选项。模块是条目（目录及其子目录）的符号表示。模块名包含在括号中，例如用于 FTP 模块的 `[ftp]`。然后你可以为模块输入选项，比如通过使用 `path` 选项指定你 FTP 站点目录和文件的位置。用户 ID 和组 ID 可以通过 `uid` 和 `gid` 选项指定。默认值是 `nobody`。这里显示了一个用于匿名访问的 FTP 模块示例：

```bash
[ftp]
path = /var/ftp/pub
comment = ftp site
```

对于更严格的访问，你可以添加 `auth` 选项来指定授权用户；`rsync` 默认允许所有用户匿名访问。使用 `rsync` 访问 FTP 站点上的区域可以通过密码文件（如 `/etc/rsyncd.secrets`）进行进一步控制。这是一个冒号分隔的用户名和密码列表。

```bash
aleina:mypass3
larisa:your5
```

与受控区域对应的模块看起来如下：

```bash
[specialftp]
path = /var/projects/special
command = restricted access
auth users = aleina,larisa
secrets file = /etc/rsyncd.secrets
```

## 查看可用模块

如果你位于一个 FTP 服务器上并想查看哪些模块可用，可以运行带有 `localhost` 选项的 `rsync`，且双冒号后不跟跟任何内容。

```bash
$ rsync localhost::
ftp
specialftp
```

远程用户只需通过输入你的主机名和双冒号即可知道你拥有哪些模块。

```bash
rsync mytrek.com::
```

## rsync 镜像

某些站点允许你使用 `rsync` 执行镜像操作。通过 `rsync`，你不需要复制整个站点，只需复制那些更改的文件。以下示例将 `mytrek` FTP 站点镜像到本地站点的 `/var/ftp/mirror/mytrek` 目录。

```bash
rsync -a --delete ftp.mytrek.com:ftp /var/ftp/mirror/mytrek
```
