
该脚本通过标准环境变量 `CGI_PATH_INFO` 和 `PATH_TRANSLATED` 接收所请求文档的 URL 和文件路径。这在开发过滤脚本时很有用。本节讨论其中一个这样的过滤脚本。

当通过 Web 请求文本文件（`.txt`）时，它在 Web 浏览器上的显示格式并不理想，因为大多数 Web 浏览器不会以任何方式转换换行符。通常，大多数文本文件显示为一个大的段落。通过使用 `Action` 指令，你可以开发更好的解决方案。

举一个更有趣的例子，假设你现在想要开发一个解决方案，不仅要在 Web 浏览器上更好地显示文本文件，还要在每个文本文件的末尾插入版权声明。为了实现这一点，你需要做两件事。首先，在 `httpd.conf` 文件中添加以下指令：

```apache
Action plain/text /cgi-bin/textfilter.pl
```

然后，开发 Perl 脚本 `textfilter`，该脚本将以你希望的方式显示文本文件。列表 5-1 显示了这样一个脚本。你可以在随附 CD-ROM 的 `Scripts/Chapter 5` 目录中找到此脚本。

#### 列表 5-1：textfilter.pl

```perl
#!/usr/bin/perl

#
# Script: textfilter.pl
#
# Purpose: This filter script converts plain text files
#         into an HTML document but keeps the text layout
#         as is.
#
# Copyright (c) 2001 by Mohammed J. Kabir
#
# License: GPL
#
# The copyright message file is always stored in
# the server's document root
# directory and is called copyright.html.

my $copyright_file = $ENV{DOCUMENT_ROOT} . "/copyright.html";

# Get the requested document's path
my $path_translated = $ENV{PATH_TRANSLATED};

# Other variables needed for storing data
my $line;
my @text;
my @html;

# Store the path info and the file name of requested doc in an
# array
@filename = split(/\/\/.{$path_translated};

# Because HTML tags are used to display the text file,
# lets print the text/html content header.
print "Content-type: text/html\n\n";

# Read the document requested and store the data
# in @text array variable
@text = &readFile($path_translated);

# Now print the following HTML document tags.
# These tags will be sent before the actual document content

print <<HEAD;
<HTML>
<HEAD><TITLE>$filename[-1] </TITLE> </HEAD>
<BODY BGCOLOR="white">
<BLOCKQUOTE>
<PRE>
HEAD

# Now print each line stored in the @text array
# (that is, the content of the document requested)
foreach $line (@text) { print $line; }

# Now read the copyright file and store the content
# in the @html array variable
@html = &readFile($copyright_file);

# Print each line stored in the @html array (that is,
# the content of the copyright message file)
foreach $line (@html){ print $line; }

# Exit the filter
exit 0;

sub readFile {
    #
    # Subroutine: readFile
    # Purpose: Reads a file if it exists or else prints
    # an error message and exits script
    #
    # Get the name of the passed file name and store
    # it in variable $file
    my $file = shift;
    # Local buffer variable
    my @buffer;
    
    # If the file exists, open it and read all the
    # lines into the @buffer array variable
    if(-e $file) {
        open(FP,$file) || die "Can not open $file:";
        while(<FP>){
            push(@buffer,$_);
        }
        close(FP);
    } else {
        push(@buffer,"$file is missing.");
    }
    # Return the content of the buffer.
    return (@buffer);
}
```

前面的脚本读取请求的文本文件，并输出内容，内容被包裹在几个 HTML 标签内，以使其能够按原样显示。这是通过使用 HTML 标签 `<PRE>` 来实现的。在内容输出后，版权声明文件内容会被插入到输出的末尾。这使得每次请求的文本文件都能附带打印一条版权声明。图 5-1 展示了一个示例输出，其中文本文件正在 Web 浏览器上显示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_151_0.png)

正如你所见，请求的文件名显示为标题。文档被块引用（block quote），并打印了一条自定义的版权声明。版权声明文件存储在文档的根目录中。本例中使用的文件如下：

```html
</PRE>
</BLOCKQUOTE>
<CENTER>
<HR>
Copyright (c) 2001 Mohammed J. Kabir (kabir@mobidac.com)
</CENTER>
</BODY>
</HTML>
```

## `Script` 指令

`Script` 指令类似于 `Action` 指令，但它不是将操作关联到 MIME 类型，而是将操作关联到 HTTP 请求，例如 `GET`、`POST`、`PUT` 或 `DELETE`。CGI 脚本通过标准的 CGI `PATH_INFO` 和 `PATH_TRANSLATED` 环境变量获取所请求文档的 URL 和文件路径。

**语法：** `Script method cgi-script`

**上下文：** 服务器配置、虚拟主机、目录

该指令定义默认操作。换句话说，如果你定义了如下配置：

```apache
Script POST /cgi-bin/default_post.pl
```

在 Apache 配置文件（如 `srm.conf`）中，那么每当通过 HTTP `POST` 方法发出请求时，它都会按常规处理，除非需要使用该指令指定的默认操作。例如，以下 HTML 表单没有指定 CGI 脚本作为其操作：

```html
<FORM METHOD="POST">
    Enter Name: <INPUT TYPE=TEXT NAME="name" SIZE=25>
    <INPUT TYPE=SUBMIT VALUE="Click Here">
</FORM>
```

如果用户通过此表单提交了一个姓名，由于没有指定用于处理该信息的 CGI 脚本，此时将运行默认的 `POST` 操作 `/cgi-bin/default_post.pl` 脚本。然而，如果将 `<FORM ...>` 标签修改为：

```html
<FORM ACTION="/cgi-bin/form_processor.pl" METHOD="POST">
```
