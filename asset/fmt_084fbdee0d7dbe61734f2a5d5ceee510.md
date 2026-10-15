
`pack .list .scroll -side left -fill both -expand yes anchor w`

`wm minsize 11`

## 选择文件进行显示的函数

```
proc selectfile{dir file} {
    if [file exists $file] then
        dispfile $file
    else
        puts stdout "$file isn't a directory or regular file"
    }
}
```

## 检查文件是否存在

## 调用 `dispfile` 显示文件

```
if $argc>0 {set dir [index $arg 0]} else {set dir "."}
```

## 显示文件和目录的函数

```
proc listdirfunc dir {
    .listdir delete 0 end
    .list delete 0 end
    cd $dir
    set ndir [exec ls -a]
    foreach i in $ndir {
        if [file isdirectory $i] {
            .listdir insert end $i
        } else {
            .list insert end $i
        }
    }
}
```

## 框架和标签

```
listdirfunc $dir

# 设置目录和文件的绑定。
bind all <Control-c> {destroy .}
bind .list <Double-Button-1> {set i [selection get]; selectfile $dir $i}
bind .listdir <Double-Button-1> {set i [selection get]; listdirfunc $i}
```

为不同的操作创建新窗口，可以使用单窗口中显示的框架。当一个新操作被选中时，它会替换正在显示的操作。效果是，每个操作都有它自己的框架，选中时显示在窗口底部。当操作完成后，框架会消失，相应地缩小主窗口。图 8–4 显示了窗口中的一些框架。
![](img/3cfc28f62e3fe98d5a49b453e25d689c_319_0.png)

图 8-4 Tk 框架

标签允许你通过鼠标点击窗口中显示的项目。标签让你使用窗口中显示的任何对象创建简单的菜单。在图 8–4 中，主菜单只是由 1、2 和 3 这三行文本组成的。鼠标悬停在其中某行上会改变该行的背景颜色。

目录显示在相应的列表框中。注意看同一个事件（双击）是如何绑定到两个非常不同的操作上的——结果取决于该事件发生在哪个对象上。
`mydir` 脚本的内容所示：

```
#!/usr/bin/wish -f
```

## 将文件加载到窗口文本框的函数

```
proc LoadFile {win filename} {
    set fid [open $filename r]
    while {[read $fid 10000] != ""} 
    close $fid
}
```

## 显示文件的函数。窗口带有它自己的文本框、滚动条和按钮

```
proc dispfile {
    # 创建显示窗口、窗口标题和图标名称。
    set w .dispf
    catch (destroy $w)
    toplevel $w
    wtitle $w "Display File"
    wm iconame $w "Display File"
```

![](img/3cfc28f62e3fe98d5a49b453e25d689c_317_0.png)

创建了顶层窗口框架，名为 `.buttons`。
在 `w.buttons` 中创建了名为 `.dismiss` 的按钮。

## 创建显示窗口按钮

```
frame w.buttons -side bottom -fill x -pady 2
button w.buttons.dismiss -text dismiss -command "destroy $w"
pack w.buttons.dismiss -side left -expand 1
```

## 为文件文本创建滚动条

```
scrollbar w.scroll -command $w.disptext yview
pack w.scroll -side right -fill y
```

滚动条已定义。

## 创建用于显示文本的文本框

```
text $w.disptext -relief sunken -bd 2 -yscrollcommand \
    $w.scroll set -setgrid 1 -height 30 -wrap word -width 80
pack $w.disptext -expand yes -fill both
```

注意这是一个换行行。

## 打开文件并读入文本

```
LoadFileText $w {
}
```

将指定的文件读入文本框。

```
# 为主窗口创建窗口标题。
# 主窗口用点号引用。
# 同时也为主窗口创建图标名称
wm title . "My File Manager"
wm icename . "MyFileManager"
```

# 主窗口的标题和图标名称

## 创建目录列表框和滚动条
