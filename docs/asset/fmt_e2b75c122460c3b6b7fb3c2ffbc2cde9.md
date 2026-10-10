
```python
def op_write(self, code, address=None):
    if address is None:
        address = self.memory.alloc(len(code.build(0)))
    self.request += [
        protocol.f.Uint32(OpType.Write.value),
        protocol.f.Uint64(address),
        tuple(protocol.f.Uint8(x) for x in code.build(address))
    ]
    return address
```

```python
def op_exec(self, address):
    self.request += [
        protocol.f.Uint32(OpType.Exec.value),
        protocol.f.Uint64(address)
    ]
```

```python
def op_commit(self):
    protocol.send(self, protocol.proc.stdin, self.request)
    self.request.clear()
```

```python
def execute(self, code):
    address = self.op_write(code)
    self.op_exec(address)
    self.op_commit(address)
    self.memory.free(address)
```

第一个更改是在 `messages` 方法中。

描述可用内存区域的地址范围被添加到 `memory` 对象中，并且从地址 0 到内核结束的范围被从可用内存中移除。

实现了一些新方法，用于构建组成请求消息的操作：

- `op_write`: 接收一个 `Code` 实例（可选可选基地址），构建代码，并将生成的二进制文件编码到写操作中，然后将其添加到请求的操作列表中。
- `op_exec`: 接收一个地址并将其编码到执行操作中，将其添加到操作列表中。
- `op_commit`: 获取操作列表中的内容以构建并发送请求消息。

这些方法提供了一个底层 API，但我们为最常见的用例实现了一个 `execute` 方法，只需要一个 `Code` 实例。

让我们通过在客端执行一些代码来测试此新功能：

```python
# main.py
import protocol
from guest import Guest
from code import Code
from enum import Enum

class OOBType(Enum):
    Print = 0

with Guest() as g:
    for (msg_type, body) in g.messages():
        if msg_type == protocol.MT.OOB:
            oob_type, *msg = OOBType.Print.value
            fmt, *args = msg
            print(f'{fmt} % tuple(args)}')
        if msg_type == protocol.MT.Boot:
            print('BOOTED')
            g.execute(Code("""
                OOB_PRINT "hello world!"
                REPLY_EMPTY
                ret""", g.symbols))
        if msg_type == protocol.MT.Reply:
            print(f'REPLY: {body}')
```

当启动消息到达时，脚本会将一段代码注入到客端以发送“hello world!”消息。

**注意** `OOB_PRINT` 和 `REPLY_EMPTY` 宏定义在“`macros.asm`”文件中，由于原因代码列表中被省略了。

```bash
root@gh:~$ python3 main.py
BOOTED at 0x4031
PRINT: hello world!
REPLY: []
```

我们可以看到由注入代码生成的“hello world!”消息和一个空回复。

## Fuzzing

使用我们目前的框架，我们现在只需几行代码即可启动虚拟机并在 Ring-0 执行任意代码。现在我们将使用它来模糊化虚拟机！

### Fuzzer 基类

编写 fuzzer 涉及一些重复性任务，我们可以将其抽象到基类中：

```python
# fuzzer.py
import random
import signal
import protocol
from enum import Enum
from guest import Guest
from code import Code

class OOBType(Enum):
    Print = 0
    Assert = 1

class Fuzzer:
    regs = ('rax', 'rbx', 'rcx', 'rdx', 'rsi', 'rdi', 'rbp', 'rsp', 'r8', 'r9', 'r10', 'r11', 'r12', 'r13', 'r14', 'r15')

    def __init__(self, seed=0):
        self.rand = random.Random(seed)
        signal.signal(signal.SIGALRM, Fuzzer.timeout_handler)

    @staticmethod
    def timeout_handler(signum, frame):
        raise Exception('TIMEOUT')

    def context_save(self):
        return '\n'.join(
            f'pop {reg}' + f'\nmword {self.context_area + n*8}, {reg}'
            for (n, reg) in enumerate(self.regs)) + '\n'

    def context_restore(self):
        return '\n'.join(
            f'mov {reg}, qword {self.context_area + n*8}'
            for (n, reg) in enumerate(self.regs)) + '\njmp rax\n'

    def code(self, code):
        return Code(code, self.guest.symbols)

    def fuzz(self, reply):
        raise NotImplementedError

    def on_boot(self, body):
        self.fuzz([])

    def handle_message(self, msg_type, body):
        if msg_type == protocol.MT.OOB:
            ... omitted for brevity
        else:
            if msg_type == protocol.MT.Boot:
                self.context_area = self.guest.memory.alloc(0x1000)
                self.on_boot(body)
            else:
                self.fuzz(body)

    def run(self):
        while True:
            try:
                with Guest() as self.guest:
                    for msg in self.guest.messages():
                        signal.alarm(0)
                        signal.alarm(2)
                        self.handle_message(*msg)
            except Exception as e:
```
