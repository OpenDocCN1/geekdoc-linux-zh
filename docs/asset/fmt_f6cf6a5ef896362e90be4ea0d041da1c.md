
最后，点击“本地化（Localisation）”标签页查看最后一个类别。在这里，你可以更改区域设置（它控制着树莓派 OS 使用的语言和数字显示方式）、更改时区、更改键盘布局并为 WiFi 设置国家。现在，只需点击“取消（Cancel）”在不进行任何更改的情况下关闭工具。

![](img/0aff4cdab15427839fb48fd7c6f677d3_50_1.png)

### 警告！

不同国家对 WiFi 无电电设备使用的频率有不同的规定。将树莓派配置工具中的 WiFi 国家设置为与你所在地不同的国家，可能会导致它难以连接到你的网络，甚至可能在无线电许可法下属于违法 – 所以不要这样做！

### 关机

现在你已经探索了树莓派 OS 桌面，是时候学习一项非常重要的技能了：安全地关闭你的树莓派。像任何计算机一样，树莓派将你正在工作的文件保存在易性内存中 – 系统关闭时该内存会被清空。对于你创建的文档，只需依次保存每个 – 这会将文件从易性内存移动到非易失性内存 microSD 卡 – 以确保你不会丢失任何内容。

你正在工作的文档并不是唯一打开的文件，树莓派 OS 在运行时会保持许多文件打开，在这些文件仍处于打开时拔掉树莓派的电源线可能会导致操作系统损坏，从而导致重新安装。

为了防止这种情况发生，你需要确保告诉树莓派 OS 保存其所有文件并准备好断电 – 这一过程被称为关闭操作系统。

点击桌面左角的树莓派图标，然后点击“关机（Shutdown）”。将弹出一个带有三个选项的窗口（图 3-22）：关机（Shutdown）、重启（Reboot）和注销（Logout）。关机是你最常使用的选项：点击此将告诉树莓派 OS 关闭所有打开的软件和文件，然后关闭树莓派。一旦屏幕变黑，等待几秒钟直到树莓派上闪烁的绿灯熄灭；就可以安全地关闭电源了。

要重新开启树莓派，只需重新连接电源线，或切换墙上插座的电源。

![](img/0aff4cdab15427839fb48fd7c6f677d3_51_0.png)

图 3-22：关闭树莓派

重启的过程与关机类似，但它会自动重启系统。这在你安装了新软件或更改了需要重启的设置后非常有用。注销会结束当前用户会话但让电脑运行，如果你想在不关闭整个系统的情况下切换用户，这非常有用。

bit out of the bottom connects into the hole at the top of your `say Hello!` block until you see a white outline, then let go of the mouse. You don't have to be precise; if it's close enough, the block will snap into place just like a jigsaw piece. If it doesn't, click and hold on it again to adjust its position until it does.

```
when clicked
say Hello!
```

Your program is now complete. To make it work, known as running the program, click on the green flag on the top-left of the stage. If all has gone well, the cat sprite on the stage will greet you with 'Hello!' (Figure 4-2) your first program is a success!

![](img/0aff4cdab15427839fb48fd7c6f67d3_56_0)

> Figure 4-2: Click the green flag above the stage and the cat will say 'Hello'

Before moving on, save your program. Click on the File menu, then ‘Save to your computer. Type in a name and click the Save button (**Figure 4-3**).

![](img/0aff4cdab15427839fb48fd7c6f67d3_57_0)

**Figure 4-3:** Save your program with a name

> WHAT CAN IT SAY?

Some blocks in Scratch can be changed. Try clicking on the word ‘Hello’ and typing something else, then click the green flag. What happens on the stage?

# Next steps: sequencing

While your program has two blocks, it has only one instruction: to say ‘Hello’ every time the flag is clicked and the program runs. You need to know about *sequencing*. Computer programs, at their simplest, are a list of instructions, just like a recipe. Each instruction follows the last in a logical progression known as a *linear sequence*.

Start by clicking and dragging the `when Hello` block from the code area back to the blocks palette (**Figure 4-4**). This deletes the block, removing it from your program and leaving the trigger block, `when clicked`.

![](img/0aff4cdab15427839fb48fd7c6f67d3_58_0)

**Figure 4-4:** To delete a block, simply drag it out of the code area

Click on the Motion category in the blocks palette, then click and drag the `move 10 steps` block so it locks into place underneath the trigger block on the code area. As the name suggests, this tells your sprite – the cat – to move a number of steps in the direction it's currently facing.

![](img/0aff4cdab15427839fb48fd7c6f_51)

Add more instructions to your program to create a sequence. Click on the Sound palette, colour-coded pink, then click and drag the `play sound Meow until done` block so it locks underneath the `move 10 steps` block. Keep going: click back on the Motion category and drag another `move 10 steps` block underneath your Sound block, but this time click the '10' to select it and create a `move -10 steps` block.

![](img/0aff4cdab15427839fb48fd7c6f_52)

Click on the green flag above the stage to run the program. You'll see the cat move to the right, make a meow sound – make sure you've got speakers or headphones to hear it – move back to the start again. Click the green flag, and the cat will repeat its actions.
