
# 第十八章

## 购买

**亚马逊 UK**

购买《异形夺魂》视频
购买《异形夺魂》DVD
购买《异形》系列装视频
购买《异形》系列装 DVD

**亚马逊 US**

购买《异形夺魂》视频
购买《异形夺魂》DVD
购买《异形》系列装视频
购买《异形》系列装 DVD

## 相关物品

异形
异形2集
异形3
异形系列盒装

**另参阅：** 科幻
恐怖
动作

该文档同时包含传统的 XML 数据和一些 HTML 特有的链接信息。例如，有指向其他评论文件的链接，以及链接到 Amazon 上可购买物品所需的 ID 和主机信息的详情。

列表 18.3 中的脚本将 XML 文档翻译为 HTML。该脚本通过使用单个哈希（`hash`）工作，该哈希包含了 HTML 标签和属性，当看到特定的 XML 标签时输出它们。`handler_start(function)` 识别标签并构建等效的 HTML 标签。

# 列表 18.3：一个 XML 到 HTML 的转换器

```perl
#!/usr/local/bin/perl -w

use strict;

use XML::Parser;

# %elements 哈希存储了解析器找到的

# XML 标签的配置信息。输出的

# 是 HTML。由于单个 XML 标签可以生成

# 多个 HTML 标签，因此基础键链接到一个列表。

# 在列表中，每个 HTML 标签都有独立的哈希引用，

# 且哈希包含了标签和属性

# 信息。

# 例如，<title> XML 标签产生：

# <tr bgcolor="#000094" align="left">

# <font face="Arial, Helvetica" color="#ffffff"><b>

my %elements = (

  'video' => [

    'title' => [[ tag => 'tr'],

      { tag => 'td',

        attr => {

          'bgcolor' => '#000094',

          'align' => 'left',

        }

      },

      { tag => 'font',

        attr => {

          'face' => 'Arial, Helvetica',

          'color' => '#ffffff',

        }

      },

      { tag => 'b' }],

  ],

  'paneltitle' => [[ tag => 'tr'],

    { tag => 'td',

      attr => {

        'bgcolor' => '#000094',

        'align' => 'left',

      }

    },

    { tag => 'font',

      attr => {

        'face' => 'Arial, Helvetica',

        'color' => '#ffffff',

      }

    },

    { tag => 'b' }],

  'stars' => [[ tag => 'tr'],

    { tag => 'td' }],

  'description' => [[ tag => 'tr'],

    { tag => 'td',

      attr => {

        'bgcolor' => '#000094',

        'align' => 'left',

      }

    },

    { tag => 'font',

      attr => {

        'face' => 'Arial, Helvetica',

        'color' => '#ffffff',

      }

    },

    { tag => 'b' }],

  'review' => [[ tag => 'tr'],

    { tag => 'td' },

    { tag => 'p' }],

  'b' => [[ tag => 'b' }],

  'br' => [[ tag => 'br' }],

  'main' => [[ tag => 'td',

    attr => {

      'width' => '66%',

      'valign' => 'top',

    }

  },

    { tag => 'table',

      attr => {

        'border' => '0',

        'cellspacing' => '0',

        'cellpadding' => '2',

        'width' => '100%',

      }

    }

  ]],

  'para' => [[ tag => 'tr'],

    { tag => 'td' }],

  'azus' => [[ tag => 'a',

    href => 'http://www.amazon.com/exec/obidos/%%ID%%']],

  'azuk' => [[ tag => 'a',

    href => 'http://www.amazon.co.uk/exec/obidos/%%ID%%']],

  'keyref' => [[ tag => 'a',

    href => '/cgi/reviews?t=%%ID%%' }],

  'realref' => [[ tag => 'a',

    href => '/cgi/reviews?t=%%ID%%' }],

  'img' => [[ tag => 'img',

    src => '/img/reviews/',

    end => 0]],

  'panel' => [[ tag => 'td',

    attr => (

      'width' => '34%',

      'valign' => 'top',

    )

  },

  { tag => 'table',

    attr => (

      'width' => '100%',

      'border' => '0',

      'cellspacing' => '0',

      'cellpadding' => '2',

    )

  ]],

);

# 因为这是一个 CGI 脚本，我们在开始解析过程之前

# 输出 Content-type 头。
```

```perl
print "Content-type: text/html\n\n";
print "<<html><head></body>\n";
show_review('alien_r.xml');
print "</</body></html>\n";
```

# `show_review()` 函数在屏幕上格式化评论

```perl
sub show_review
{
    my $title = shift;
    # 评论通常是另一个页面的一部分，
```
