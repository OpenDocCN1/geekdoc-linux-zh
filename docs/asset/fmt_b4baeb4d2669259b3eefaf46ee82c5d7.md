...[/content]`. No extra explanation.

**Analysis of the Input Text:**

*   **Headings:**
    *   `## 构建套接字地址` -> Good.
    *   `## 检查通用套接字地址` -> Good.
    *   `### 清单 2.1：通用套接字地址` -> Good.
    *   `## 构建本地地址` -> Good.
    *   `### 清单 2.2：`sockaddr_un` 地址结构体` -> The input has backticks around `sockaddr_un` inside the heading. I should probably keep the heading clean but apply backticks to the identifier. The rule says "Reorganize heading levels". It doesn't say "Clean up heading styling", but rule 4 says add backticks to class/struct names. So `### 清单 2.2：`sockaddr_un` 地址结构体` is appropriate.
    *   `## 构建传统本地地址` -> Good.
    *   `### 清单 2.3：af_unix.c——...` -> `af_unix.c` is a file name/path, should it be backticked? Yes, it's a path/file.

*   **Inline Code Candidates:**
    *   `socketpair(2)` -> Function/Command.
    *   `AF_LOCAL`, `AF_UNIX` -> Constants/Defines.
    *   `PF_LOCAL` -> Constant.
    *   `AF_INET` -> Constant.
    *   `(void *)` -> Type syntax.
    *   `sa_family_t` -> Type.
    *   `sa_family` -> Variable/Member.
    *   `sa_data[14]` -> Array access.
    *   `lpr(1)` -> Command.
    *   `sockaddr_un` -> Struct name.
    *   `sun_family` -> Member.
    *   `sun_path[108]` -> Member.
    *   `null` -> Constant/Keyword.
    *   `memset(3)` -> Function.
    *   `AF_LOCAL`/`AF_UNIX` -> Constants.
    *   `unix(4)` -> Man page/Command.
    *   `/dev/printer` -> Path.
    *   `lpd` -> Daemon/Command.
    *   `memset(3)` -> Function.
    *   `netstat(1)` -> Command.
    *   `socket(2)` -> Function.
    *   `bind(2)` -> Function.
    *   `af_unix.c` -> File path.
    *   `perror()`, `exit(1)` in code block? The rule says "code blocks ... add backticks". It implies the content *inside* the block stays as is, but identifiers *in the text* get backticks. The example shows a code block remaining just a code block.
    *   `/tmp/my_sock` in code block? Stays as is.
    *   Text identifiers like `uaddr`, `sock_unix`, `adr_unix`, `len_unix`, `ptn_unix` appear in code blocks. Do I backtick them in the code block? No, the rule applies to text *outside* or general mention. The example:
        ```
        if (condVar > someVal) {console.log("xxx")}
        ```
        The identifiers inside the code block are *not* backticked individually; the block itself is the code block. However, identifiers in *prose* need backticks.
    *   Wait, looking at the example again:
        `在 List.of(arg0, arg1, arg2) 中，List 接口的工厂方法 of()...`
        Result: `在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`...`
        So, identifiers in prose are backticked. Identifiers *inside* a fenced code block are NOT backticked individually (the fence handles that).

*   **Bold/Italic conversion:**
    *   `*图 2.1：...*` -> This is a caption. Usually captions are italic. Does it contain code? No. Keep italic? The rule says "If above things (var/func/class/path/cmd) are surrounded by bold/italic, remove stars and add backticks."
    *   `*图 2.2：这是 /dev/printer 的 AF_LOCAL/AF_UNIX 套接字地址。*` -> Contains paths and constants.
        Input: `*图 2.2：这是 /dev/printer 的 AF_LOCAL/AF_UNIX 套接字地址。*`
        Output: `*图 2.2：这是`/dev/printer`的`AF_LOCAL`/`AF_UNIX`套接字地址。*` -> Wait, if I remove the stars, it becomes plain text. The rule says "remove stars **add backticks**". It implies the *identifier* gets backticks. The *sentence* shouldn't necessarily lose its emphasis unless the emphasis was *only* wrapping the identifier.
        Let's look at the example: `cmd arg0 arg1 arg2` was in prose.
        If the input is `*图 2.1：这是通用套接字地址布局的示意图。*`, it has no code identifiers. Keep italic.
        If the input is `*图 2.2：这是 /dev/printer ...*`, it has `/dev/printer` and `AF_LOCAL`.
        Rule: "If the above things [identifiers] ... are surrounded by bold/italic, remove stars add backticks."
        This usually applies when the *entire phrase* is just the identifier, e.g., `**AF_UNIX**` -> `` `AF_UNIX` ``.
        If it's a whole caption containing identifiers, I should backtick the identifiers *within* the caption. The caption itself can remain italic or become plain. The example doesn't show this specific case. Standard practice: Keep caption italic, backtick identifiers inside.
        However, the prompt says "remove stars ... add backticks". This phrasing is tricky.
        Example: `cmd` command: `cmd arg0 arg1 arg2`.
        Input: `cmd` was not bold/italic.
        If input was `**cmd**`, output `` `cmd` ``.
        If input was `*图 2.2：这是 /dev/printer ...*`, the stars wrap the *sentence*. The identifiers are *inside*. I will backtick the identifiers inside the sentence. I will likely remove the stars from the sentence to conform to "standard Markdown" and avoid nested emphasis mess, or keep the sentence italic. Let's look at "Optimize paragraph format". It's safer to make captions plain or just backtick the code parts.
        Actually, looking at the rule strictly: "All standalone appearing ... need backticks."
        If I see `*图 2.2：这是 /dev/printer ...*`, `/dev/printer` is standalone inside the sentence.
        I will process: `图 2.2：这是`/dev/printer`的`AF_LOCAL`/`AF_UNIX`套接字地址。` (Removing the outer stars of the caption seems consistent with cleaning up, or keeping them. The prompt doesn't explicitly forbid italic captions. But it says "remove stars" if identifiers are wrapped. Here identifiers are *not* the sole content of the stars. I will keep the caption style as italic or plain, but definitely backtick the identifiers.)
        Let's check `**注意**`. It's a header-like text.
        Let's check `**提示**`.

    *   Specific case: `sockaddr_un` in `### 清单 2.2：`sockaddr_un` 地址结构体`. The input already has backticks there. I should keep them.

*   **Code Blocks:**
    *   The input has code blocks for C code.
    *   I need to ensure the C code blocks are properly fenced.
    *   The input includes a table in "构建传统本地地址".
        ```
        | sun_family | sun_path |
        | :--- | :--- |
        | `AF_LOCAL` | `/dev/printer` |
        ```
        Table headers `sun_family` and `sun_path` are identifiers. The cells are already backticked in the input (mostly). I need to make sure they are consistent.

**Step-by-Step Processing:**

1.  **Intro:**
    `剩下的就是解释域参数了。对于 `socketpair(2)` 函数，此值必须始终为 `AF_LOCAL` 或 `AF_UNIX`。在上一章中曾指出，宏 `AF_UNIX` 是 `AF_LOCAL` 的等价旧名称。然而，`AF_LOCAL` 到底意味着什么？它选择了什么？`
    -> Identifiers already backticked in input?
    Input: `socketpair(2)` is backticked. `AF_LOCAL` backticked. `AF_UNIX` backticked.
    Wait, the input provided in the prompt *already* has backticks in many places?
    Let's re-read the input carefully.
    Input: `对于 `socketpair(2)` 函数` -> Yes, it has backticks.
    Input: `常量的 `AF_` 前缀` -> Yes.
    Input: `PF_` 前缀 -> `PF_` is backticked.
    Input: `PF_LOCAL` -> backticked.
    Input: `(void *)` -> backticked.
    Input: `sa_family_t` -> backticked.
    Input: `sa_family` -> backticked?
    Input: `char          sa_data[14];` is in a code block.
    Input: `sa_data[14]` in text: `结构体元素 `sa_data[14]` 代表...` -> Backticked.
    
    It seems the input *already* applies a lot of the rules. My job is to:
    1. Verify heading levels.
    2. Clean up paragraph spacing (remove extra newlines).
    3. Ensure *all* remaining identifiers are backticked (e.g. if I missed one in my scan).
    4. Handle the bold/italic vs backtick rule.
    5. Ensure code blocks are fenced.

    Let's check for un-backticked identifiers in the text.
    - `cvar` example in prompt.
    - In target text:
    - `第 4 章“套接字类型和协议”` -> No code.
    - `lpr(1)` -> Backticked in input? `当你使用 `lpr(1)` 命令...` Yes.
    - `AF_UNIX` -> Yes.
    - `sockaddr_un` -> Yes.
    - `sun_family` -> `结构体成员 `sun_family` ...` Yes.
    - `sun_path[108]` -> `结构体成员 `sun_path[108]` ...` Yes.
    - `null` -> `字符数组末尾不需要 `null` 字节。` Yes.
    - `AF_LOCAL`/`AF_UNIX` -> `... `AF_LOCAL`/`AF_UNIX` 地址。` Yes.
    - `unix(4)` -> `... `unix(4)` man 手册页 ...` Yes.
    - `/dev/printer` -> `... 套接字 `/dev/printer` 的物理布局 ...` Yes.
    - `lpd` -> `... `lpd` 打印守护进程 ...` Yes.
    - `memset(3)` -> `... `memset(3)` 函数 ...` Yes.
    - `netstat(1)` -> `... `netstat(1)` 命令 ...` Yes.
    - `socket(2)` -> `... `socket(2)` ...` Yes.
    - `bind(2)` -> `... `bind(2)` ...` Yes.
    - `af_unix.c` -> `... `af_unix.c` ...` Yes.
    
    Okay, the input is *mostly* formatted. I just need to check for:
    1.  Any missed identifiers.
    2.  The "remove stars add backticks" rule for any bold/italic wrapped identifiers.
    3.  Spacing cleanup.
    4.  Code block integrity.
    5.  Heading consistency.

    **Potential Issues:**
    - `*图 2.1：这是通用套接字地址布局的示意图。*` -> No identifiers. Keep italic or make plain? The rule says "remove stars add backticks" IF the thing is an identifier wrapped in stars. This is a caption. It's not an identifier. I will likely keep it as a plain paragraph or italic paragraph. The prompt says "optimize paragraph format". Usually, captions are just text. I'll keep the text as is but maybe remove the italic to be "standard markdown" unless it's a specific style choice. The prompt says "remove stars **add backticks**" for identifiers. It doesn't say "remove all italics". However, "standard Markdown" often treats image captions as plain text. I will leave `*...*` as is if it doesn't contain code, or convert to plain if I want to be clean. Let's look at `*图 2.2：这是 /dev/printer ...*`. This contains code identifiers.
    Rule 4: "If above things... are surrounded by bold or italic, remove stars add backticks."
    Interpretation A: `**/dev/printer**` -> `` `/dev/printer` ``.
    Interpretation B: `*图 2.2：这是 /dev/printer ...*` -> The identifier `/dev/printer` is *inside* the italic text, not *surrounded* by it exclusively. The *sentence* is surrounded.
    However, the prompt likely wants me to identify the code within and backtick it.
    Does it want me to remove the italic from the *whole sentence*?
    "remove stars **add backticks**" (remove the stars, add backticks).
    If I have `*Text with code*`, and I remove stars, I get `Text with code`. Then I add backticks to code: `Text with `code``.
    This seems the most logical interpretation for cleaning up mixed content.
    So: `*图 2.2：这是 /dev/printer 的 AF_LOCAL/AF_UNIX 套接字地址。*`
    Becomes: `图 2.2：这是`/dev/printer`的`AF_LOCAL`/`AF_UNIX`套接字地址。` (Plain text caption with backticked identifiers).
    Same for `*图 2.1...*` -> `图 2.1：这是通用套接字地址布局的示意图。`

    - `**注意**` and `**提示**` -> These are headings or emphasized labels.
    Rule: "Reorganize heading levels".
    If `**注意**` is just bold text acting as a subheader, I might make it a `####` or keep it bold.
    The prompt says "preserve reasonable # ## ### structure".
    The input uses `##` and `###`.
    `**注意**` is in the middle of the text. It looks like a "Note" block.
    I will keep `**注意**` as bold text (or make it a heading `#### 注意`?).
    Given "Reorganize heading levels", if it acts as a section marker, maybe `####`. But the content following it is short.
    Let's look at the structure:
    `## 构建传统本地地址`
    ...
    `**注意**`
    `如果你正确初始化...`
    ...
    `**提示**`
    `有关本地套接字地址...`
    
    These look like admonitions. In Markdown, bold text is fine. I will keep them as `**注意**` and `**提示**` on their own lines, as they function as labels.

    - `第 4 章` and `第 5 章`. No code.

    - Code Blocks:
    The input has:
    ```c
    #include <sys/socket.h>
    ```
    This is fine.
    
    ```c
    struct sockaddr {  
        sa_family_t   sa_family;   /*  地址族  */  
        char          sa_data[14];  /*  地址数据。  */  
    };
    ```
    This is fine.
    
    ```c
    #include <sys/un.h>
    ```
    
    ```c
    struct sockaddr_un {
          sa_family_t  sun_family; /* 地址族 */
          char         sun_path[108]; /* 路径名 */
    };
    ```
    
    ```c
    struct sockaddr_un uaddr;
    memset(&uaddr,0,sizeof(uaddr));
    ```
    
    The last code block in the input is long and cut off in the prompt's "input" section?
    `1: ...`
    The input ends with:
    ```
    46:  * 并不存在）。
    ```
    Wait, the prompt text ends with:
    `46:  * 并不存在）。`
    And then `[/content]`.
    
    I need to make sure the code block closes with ```c or just ```.
    
    **Refining the "Remove stars add backticks" rule:**
    
    Example from prompt:
    Input: `cmd` command: `cmd arg0 arg1 arg2`.
    
    If I see `**AF_LOCAL**` in text, I change to `` `AF_LOCAL` ``.
    If I see `*图 2.2 ...*` containing paths, I change to plain text with backticks for paths.
    
    Let's check the table in `## 构建传统本地地址`.
    `| sun_family | sun_path |`
    These are headers. Should they be backticked? `| `sun_family` | `sun_path` |`?
    Yes, they are identifiers.
    
    `| `AF_LOCAL` | `/dev/printer` |`
    These are already backticked.
    
    **Final Plan:**
    1.  Iterate through the text.
    2.  Maintain heading structure (`##`, `###`).
    3.  Clean up extra newlines between paragraphs.
    4.  Ensure all identifiers (constants, types, functions, files, commands) are backticked.
    5.  Convert italic/bold *captions* containing identifiers into plain text with backticked identifiers. Convert simple bold labels like `**注意**` to remain bold (or `####`? No, stick to bold for labels unless they are clearly headings. The prompt says "preserve reasonable # ## ### structure", implying existing #s are good. It doesn't explicitly ask to convert bold to #. I will keep `**注意**` as bold).
    6.  Ensure code blocks are properly fenced.
    7.  Wrap result in `[content]...[/content]`.

    **Detailed Check of Text:**

    *   `剩下的就是解释域参数了。` -> OK.
    *   `对于 `socketpair(2)` 函数...` -> OK.
    *   `... `AF_LOCAL` 或 `AF_UNIX` ...` -> OK.
    *   `... `AF_UNIX` 是 `AF_LOCAL` 的等价旧名称 ...` -> OK.
    *   `常量的 `AF_` 前缀...` -> OK.
    *   `... `PF_` 前缀的 C 宏，例如 `PF_LOCAL` ...` -> OK.
    *   `... `AF_` 前缀的宏视为与带 `PF_` 前缀的宏等价 ...` -> OK.
    *   `## 构建套接字地址` -> OK.
    *   `... `AF_LOCAL`（`AF_UNIX`）...` -> OK.
    *   `... `AF_INET` ...` -> OK.
    *   `... `AF_LOCAL` 地址时 ...` -> OK.
    *   `## 检查通用套接字地址` -> OK.
    *   `... `(void *)` ...` -> OK.
    *   `代码块`:
        ```c
        #include <sys/socket.h>
        ```
        OK.
    *   `### 清单 2.1：通用套接字地址` -> OK.
    *   Code block with `struct sockaddr`. OK.
    *   `数据类型 `sa_family_t` ...` -> OK.
    *   `结构体元素 `sa_data[14]` ...` -> OK.
    *   `![](img/961a0296fe36074690a9847b79332eff_55_0.png)` -> Image. OK.
    *   `*图 2.1：这是通用套接字地址布局的示意图。*` -> No identifiers. Remove stars? Or keep? "Optimize paragraph format". I'll remove stars to make it plain text, standard for captions in this context. Or keep italic? The rule about removing stars specifically applies to identifiers. For captions without identifiers, it's ambiguous. I will make it plain text to be safe and clean, or just keep the text. Let's look at `*图 2.2...*` which *does* have identifiers. I will definitely backtick those. For consistency, I will treat captions as plain text paragraphs.
    *   `> 通用套接字地址结构体...` -> Blockquote.
    *   `... 定义 `sa_family` 成员 ...` -> `sa_family` is backticked?
    *   Input: `... 定义 `sa_family` 成员 ...`
    *   Actually, looking at input: `... 定义 `sa_family` 成员 ...`
    *   Wait, the input provided in the prompt *does* have backticks around `sa_family`?
    *   Let's check the raw input provided:
        `... 所有地址必须在结构体的完全相同的位置定义 `sa_family` 成员 ...`
        Yes, it seems `sa_family` is backticked in the input I was given?
        Let me re-read the *input block* carefully.
        
        Input:
        ```
        > 通用套接字地址结构体本身对程序员来说并不是特别有用。然而，它确实提供了一个参考模型，所有其他地址结构体都必须符合该模型。例如，你将了解到所有地址必须在结构体的完全相同的位置定义 `sa_family` 成员，因为这个元素决定了如何解释地址的剩余字节。
        ```
        It *is* backticked in the input.
        
        Let's check `## 构建本地地址`.
        `... 使用 `lpr(1)` 命令 ...` -> Backticked.
        `... `AF_UNIX` 域 ...` -> Backticked.
        `... `sockaddr_un` ...` -> Backticked.
        `### 清单 2.2：`sockaddr_un` 地址结构体` -> Backticked in heading.
        `... `sun_family` ... `AF_LOCAL` 或 `AF_UNIX` ...` -> Backticked.
        `... `sun_path[108]` ...` -> Backticked.
        `... `null` 字节 ...` -> Backticked.
        `**注意**` -> Bold.
        `... `AF_LOCAL`/`AF_UNIX` 地址 ...` -> Backticked.
        `**提示**` -> Bold.
        `... `unix(4)` man 手册页 ...` -> Backticked.
        `## 构建传统本地地址`
        `... 路径名 ...` -> "路径名" is Chinese word, not code.
        `... 套接字 `/dev/printer` ...` -> Backticked.
        `... `lpd` 打印守护进程 ...` -> Backticked.
        
        Table:
        `| sun_family | sun_path |` -> **NOT backticked** in input.
        `| :--- | :--- |`
        `| `AF_LOCAL` | `/dev/printer` |` -> Backticked.
        
        So I need to backtick `sun_family` and `sun_path` in the table header.
        
        `*图 2.2：这是 /dev/printer 的 AF_LOCAL/AF_UNIX 套接字地址。*`
        In input: `*图 2.2：这是 /dev/printer 的 AF_LOCAL/AF_UNIX 套接字地址。*`
        Identifiers: `/dev/printer`, `AF_LOCAL`, `AF_UNIX`.
        They are *not* backticked in the input inside the italic caption.
        I need to backtick them.
        And remove the stars? "remove stars add backticks" applies to identifiers wrapped in stars. Here the *sentence* is wrapped.
        I will produce: `图 2.2：这是`/dev/printer`的`AF_LOCAL`/`AF_UNIX`套接字地址。`
        
        `... 前两个字节表示地址类型 `AF_LOCAL` ...` -> Backticked in input?
        Input: `... 前两个字节表示地址类型 `AF_LOCAL`。` Yes.
        
        `... 使用 `memset(3)` 函数 ...` -> Backticked.
        `... `memset(3)` 函数完成 ...` -> Backticked.
        
        `## 注意` -> This is a `##` heading in the input?
        Input:
        ```
        ## 注意
        如果你正确初始化...
        ```
        Wait, in my previous scan I saw `**注意**`. Let me check the input text provided again.
        
        Input text section:
        ```
        **注意**
        
        请注意，`sockaddr_un` 地址的总大小远大于通用地址结构体的 16 字节。如果在代码中处理多个地址族，请确保分配足够的存储以容纳 `AF_LOCAL`/`AF_UNIX` 地址。
        
        在接下来的各节中，你将学习如何初始化 `AF_LOCAL` 地址并定义其长度。
        
        **提示**
        
        有关本地套接字地址的信息可在 `unix(4)` man 手册页中找到。
        
        ## 构建传统本地地址
        ```
        
        Ah, the `**注意**` and `**提示**` are in the `## 构建本地地址` section (implied by context, they appear before `## 构建传统本地地址`).
        Then later:
        ```
        ## 注意
        如果你正确初始化了强制要求的地址元素...
        ```
        Wait, looking at the very end of the input:
        ```
        ## 注意
        
        如果你正确初始化了强制要求的地址元素，那么将地址结构体清零并非必须。...
        ```
        Is `## 注意` a heading?
        The prompt says "Reorganize heading levels".
        If `## 注意` is intended as a heading, it should probably be `###` if it's under a section, or `##` if it's top level.
        Given the flow:
        `## 构建传统本地地址`
        ...
        `**注意**` (Bold text)
        ...
        `## 注意` (Heading) ??
        
        Let's look at the structure of the input again.
        The input provided in the prompt is:
        ```
        ## 构建本地地址
        ...
        **注意**
        ...
        **提示**
        ...
        ## 构建传统本地地址
        ...
        ## 注意
        如果你正确初始化...
        ```
        
        The `## 注意` near the end looks like a misplaced heading or a section header.
        Contextually, "Note" is often an admonition, not a main section.
        However, the instruction says "preserve reasonable # ## ### structure".
        If the input has `## 注意`, I should probably keep it as a heading or demote it if it doesn't fit.
        But wait, the `**注意**` earlier was bold. The `## 注意` later is a heading.
        Maybe I should standardize?
        "Reorganize heading levels" implies I have some freedom.
        A "Note" section inside a chapter is often `###` or just a bold block.
        Given the depth of `## 构建传统本地地址`, a `## 注意` sibling to it is weird if it's just a tip.
        I will change `## 注意` to `### 注意` or just `**注意**`?
        Actually, looking at the content "如果你正确初始化... 在本章中，使用 memset(3) ... 清单 2.3 ...", this seems like a sub-section of "构建传统本地地址" or a standalone "Notes" section.
        Since `清单 2.3` is referenced *after* this note, and `清单 2.3` is a `###`, the `## 注意` might be a bit too high.
        I will change `## 注意` to `### 注意` to fit under the main topic or keep it `##` if it's a major break.
        Actually, the text says "In this chapter, we use memset...". It's general.
        I'll stick to the existing level `##` to avoid over-interpretation, OR I'll make it `###` if it feels like a sub-topic.
        Let's look at the other headings:
        `## 构建套接字地址`
        `## 检查通用套接字地址`
        `## 构建本地地址`
        `## 构建传统本地地址`
        `## 注意`
        
        These are all parallel. I will keep `## 注意`.
        
        One more thing: The code block at the end is incomplete in the prompt input?
        `46:  * 并不存在）。`
        And then `[/content]`.
        I need to close the code block.
        
    **Table Formatting:**
    `| sun_family | sun_path |`
    -> `| `sun_family` | `sun_path` |`
    
    **Code Block Content Check:**
    The code block in `### 清单 2.3` starts with `1: /* af_unix.c:`.
    I should preserve the line numbers if they are part of the text content?
    Usually, source listings in books have line numbers.
    The rule says "Preserve core content".
    I will keep the text as is inside the code block.
    
    **Final Polish on Identifiers:**
    - `sa_family` in `### 清单 2.1` code block: Not backticked (correct, it's in code).
    - `sa_family` in text: Backticked.
    - `sun_family` in table header: Needs backticks.
    - `sun_path` in table header: Needs backticks.
    - `/dev/printer` in italic caption: Needs backticks, remove stars.
    
    Let's construct the output.

[content]
剩下的就是解释域参数了。对于`socketpair(2)`函数，此值必须始终为`AF_LOCAL`或`AF_UNIX`。在上一章中曾指出，宏`AF_UNIX`是`AF_LOCAL`的等价旧名称。然而，`AF_LOCAL`到底意味着什么？它选择了什么？

常量的`AF_`前缀表示地址族。域参数用于选择要使用的地址族。

第 4 章“套接字类型和协议”将进一步阐述域参数。在那一章中，你将了解到带有`PF_`前缀的 C 宏，例如`PF_LOCAL`。不过，就本章而言，你可以将带`AF_`前缀的宏视为与带`PF_`前缀的宏等价。

## 构建套接字地址

每个通信协议都规定了其网络地址的格式。因此，地址族用于指示使用的是哪种寻址类型。常量`AF_LOCAL`（`AF_UNIX`）指定地址将按照本地（UNIX）地址规则构建。常量`AF_INET`表示地址将符合 IP 地址规则，等等。这些都是地址族的示例。

在一个地址族内，可能存在变体。当你学习如何构建`AF_LOCAL`地址时，你会看到这种变体的示例。

在接下来的各节中，你将研究各种地址族的格式和物理布局。这是一个需要掌握的重要部分。人们在 BSD 套接字接口方面遇到的许多困难都与地址初始化有关。

## 检查通用套接字地址

由于 BSD 套接字接口是在采用 ANSI C 标准之前开发的，因此没有可以接受任何结构体地址的`(void *)`数据指针类型。因此，BSD 选定的解决方案是定义一个通用地址结构体。通用结构体由 C 语言语句定义如下：

```c
#include <sys/socket.h>
```

清单 2.1 说明了该结构体在 C 语言中的定义方式。

### 清单 2.1：通用套接字地址

```c
struct sockaddr {  
    sa_family_t   sa_family;   /*  地址族  */  
    char          sa_data[14];  /*  地址数据。  */  
};
```

目前，数据类型`sa_family_t`是一个无符号短整型，在 Linux 下长度为两个字节。结构体的总大小为 16 字节。结构体元素`sa_data[14]`代表剩余的 14 个字节地址信息。

图 2.1 提供了通用套接字地址结构的物理视图。

![](img/961a0296fe36074690a9847b79332eff_55_0.png)

图 2.1：这是通用套接字地址布局的示意图。

> 通用套接字地址结构体本身对程序员来说并不是特别有用。然而，它确实提供了一个参考模型，所有其他地址结构体都必须符合该模型。例如，你将了解到所有地址必须在结构体的完全相同的位置定义`sa_family`成员，因为这个元素决定了如何解释地址的剩余字节。

## 构建本地地址

这种地址格式被用于本地于你的主机（运行 Linux 的个人电脑）的套接字。例如，当你使用`lpr(1)`命令排队打印文件时，它使用本地套接字与 PC 上的打印后台作业处理服务通信。虽然也可以将 TCP/IP 用于本地通信，但事实证明效率较低。

传统上，本地地址族被称为`AF_UNIX`域（例如，UNIX 套接字地址）。这是因为这些地址使用本地 UNIX 文件名作为套接字名称。Linux 内核 2.2.0 及更高版本支持抽象套接字名称，你很快就会了解到相关内容。

`AF_LOCAL`或`AF_UNIX`地址的结构体名称为`sockaddr_un`。要在 C 程序中包含该结构体的定义，需引入以下语句：

```c
#include <sys/un.h>
```

`sockaddr_un`结构体的一个示例如清单 2.2 所示。

### 清单 2.2：`sockaddr_un` 地址结构体

```c
struct sockaddr_un {
      sa_family_t  sun_family; /* 地址族 */
      char         sun_path[108]; /* 路径名 */
};
```

结构体成员`sun_family`必须被赋值`AF_LOCAL`或`AF_UNIX`（这些宏代表相同的值，尽管现在建议使用`AF_LOCAL`）。此值指示该结构体遵循`sockaddr_un`规则进行格式化。

结构体成员`sun_path[108]`包含一个有效的 UNIX 路径名。你会发现，字符数组末尾不需要`null`字节。

**注意**

请注意，`sockaddr_un`地址的总大小远大于通用地址结构体的 16 字节。如果在代码中处理多个地址族，请确保分配足够的存储以容纳`AF_LOCAL`/`AF_UNIX`地址。

在接下来的各节中，你将学习如何初始化`AF_LOCAL`地址并定义其长度。

**提示**

有关本地套接字地址的信息可在`unix(4)` man 手册页中找到。

## 构建传统本地地址

传统本地地址的名称空间是文件系统路径名。进程可以使用任何有效路径名为其本地套接字命名。然而，要使其有效，为套接字命名的进程必须有权访问路径名的所有目录组件，并且具有在指定目录中创建最终套接字对象的权限。图 2.2 展示了套接字`/dev/printer`的物理布局，你的系统中可能正在使用它。`lpd`打印守护进程监听此本地套接字地址。

| `sun_family` | `sun_path` |
| :--- | :--- |
| `AF_LOCAL` | `/dev/printer` |

图 2.2：这是`/dev/printer`的`AF_LOCAL`/`AF_UNIX`套接字地址。

请注意，前两个字节表示地址类型`AF_LOCAL`。其余字节是字符`/dev/printer`，没有空字节。现在，我们将把注意力转向初始化此类地址的 C 代码。

一些程序员喜欢在执行赋值操作之前将地址结构体完全初始化为零。这通常使用`memset(3)`函数完成，并且这很可能是一个好主意：

```c
struct sockaddr_un uaddr;
memset(&uaddr,0,sizeof(uaddr));
```

此函数调用会为你将地址结构体的所有字节清零。

## 注意

如果你正确初始化了强制要求的地址元素，那么将地址结构体清零并非必须。然而，它确实使调试更容易，因为它消除了可能残留的其他数据。

在本章中，使用`memset(3)`将地址结构体清零，以演示如何进行此操作。

清单 2.3 展示了一个小型 C 程序，该程序初始化`sockaddr_un`结构体，然后调用`netstat(1)`命令以证明其有效性。请记住，该程序调用了尚未介绍的`socket(2)`和`bind(2)`函数。`socket(2)`函数在第 4 章中详细讲解。`bind(2)`函数将在第 5 章“将地址绑定到套接字”中讲解。

### 清单 2.3：`af_unix.c`——将 `AF_LOCAL`/`AF_UNIX` 套接字地址初始化为 `/dev/printer`

```c
1:  /* af_unix.c:
2:   *
3:   * AF_UNIX 套接字示例：
4:   */
5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <errno.h>
9:  #include <string.h>
10: #include <sys/types.h>
11: #include <sys/stat.h>
12: #include <sys/socket.h>
13: #include <sys/un.h>
14:
15: /*
16:  * 此函数报告错误
17:  * 并退出返回到 shell：
18:  */
19: static void
20: bail(const char *on_what) {
21:  perror(on_what);
22:  exit(1);
23: }
24:
25: int
26: main(int argc, char **argv, char **envp) {
27:  int z;             /* 状态返回码 */
28:  int sock_unix;     /* 套接字 */
29:  struct sockaddr_un adr_unix; /* AF_UNIX */
30:  int len_unix;      /* 长度 */
31:  const char ptn_unix[] /* 路径名 */
32:   = "/tmp/my_sock";
33:
34: /*
35:  * 创建一个 AF_UNIX（即 AF_LOCAL）套接字：
36:  */
37:  sock_unix = socket(AF_UNIX, SOCK_STREAM, 0);
38:
39:  if (sock_unix == -1)
40:   bail("socket()");
41:
42: /*
43:  * 在这里我们移除套接字的
44:  * 路径名，以防它来自
45:  * 之前的运行。忽略错误（它可能
46:  * 并不存在）。
```
