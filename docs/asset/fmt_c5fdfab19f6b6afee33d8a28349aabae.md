
```ruby
class ShowmeController < ApplicationController
  def piglatin_sentence
    # Get the headline
    sentence = params[:future_headline]
    words = sentence.split
    sentence = ""

    # Go through each word, applying the secret
    # Pig Latin algorithm
    words.each do |word|
      if word =~ /[^aeiou]/
        word << "way"
      else
        first_letter = word.slice(0, 1)
        rest = word.slice(1..)
        word = "#{$rest}#{$first_letter}ay"
      end
      sentence << word
      sentence << " "
    end

    render :text => sentence
  end
end
```

# 你是否对 iSCSI 和光纤通道存储的高昂成本感到震惊？

![](img/526fd434dcfcf1b461b94c24ea170f36_22_0.png)

# AoE 是你的答案！

ATA-over-Ethernet = 简单、低成本、可扩展的存储。

www.coraid.com

![](img/526fd434dcfcf1b461b94c24ea170f36_22_1.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_22_2.png)

**EtherDrive® SR1520**

- 支持 RAID 的 3U 设备，拥有 15 个热插拔 SATA 磁盘插槽

- 查看我们的其他存储设备和 NAS 网关

- 1. 以太网存储 – 没有 TCP/IP 开销！

- 2. 无限扩展能力，且价格处于最低水平！！

- 3. 你需要更多存储...只需购买更多磁盘 – 就是这么简单！！！

**请访问 www.coraid.com 获取更多信息。**

# 专栏

# 在锻造之中

# 列表 4. index.html (为 HTTP 响应中的 JavaScript 更新)

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title id="title">Sample HTML page</title>
<%= javascript_include_tag 'prototype' %>
</head>
<body>
<form id="fakeForm">
<h1 id="headline">Headline</h1>
<p><input type="text" name="future_headline" /></p>
</form>

<p><%= submit_to_remote 'submit-button',
"Pig Latin it!",
:url => { :action => "piglatin_sentence" },
:submit => "fakeForm" %></p>
</body>
</html>
```

# 列表 5. showme_controller.rb (更新以返回 JavaScript)

```ruby
class ShowmeController < ApplicationController
  def piglatin_sentence
    # Get the headline
    sentence = params[:future_headline]
    words = sentence.split
    sentence = ""
    # Go through each word, applying the
    # secret Pig Latin algorithm
    words.each do |word|
      if word =~ /[aeiou]/i
        word << "way"
      else
        first_letter = word.slice(0, 1)
        rest = word.slice(1..-1)
        word = "#{$rest}#{$first_letter}ay"
      end
      sentence << word
      sentence << " "
    end
    output = "Element.update($('headline'), "#{$sentence}");"
    render :text => output, :content_type => "text/javascript"
  end
end
```

具有 ID `fakeForm` 的表单内容被提交。

从 Ajax 调用返回的值用于更新具有 ID `headline` 的 HTML 元素的内容。

我们只需要进一步检查我们的控制器，如列表 3 所示。控制器并不一定知道它是被后台 Ajax 进程调用的，或者其内容将被用于更新标题元素。相反，它就像调用任何方法一样被调用，将单词转换为猪语言（Pig Latin）。翻译后的句子以纯文本文件的形式返回给用户浏览器。

# 返回 JavaScript

现在，真正的魔术开始了。正如我们刚才看到的，我们的控制器（`piglatin_sentence`）向其调用者返回一个纯文本文档。当然，我们可以自由选择以任何我们喜欢的格式返回数据。一种可能的格式是 XML。确实，Ajax 这个术语应该代表异步 JavaScript 和 XML（Asynchronous JavaScript and XML），所以 XML 作为返回值的一种常见格式并不令人惊讶。另一种日益流行的格式是 JSON（JavaScript Object Notation），它是 JavaScript 对象的文本版本，使得数据交换快速且容易。

但是，在 Ruby on Rails 的世界中，控制器可能还会向用户浏览器返回另一种类型的数据，即 JavaScript。这可能听起来没那么聪明，但请考虑 Prototype 如何处理它。如果控制器通过 `link_to_remote` 或 `submit_to_remote` 被调用，并且 HTTP 响应具有 `xml/javascript` 的内容类型，那么 JavaScript 将被执行。

这潜在地节省了时间——而不是返回应使用于标题的文本，然后使用 JavaScript 来插入它。（是的，通过使用 `submit_to_remote` 调用中的 `:update` 参数，我们能够简练地表达这一点。但代码仍然存在。）相反，我们可以简单地返回使用 DOM 修改文档的 JavaScript 代码。这将大大简化我们的代码。

要看到实际效果，请查看列表 4 和 5。列表 4 是我们模板 `index.html` 的更新版本，除了我们现在可以从对 `submit_to_remote` 的调用中移除 `:update` 参数外，基本上与之前版本没有变化：

```erb
<p><%= submit_to_remote 'submit-button',
"Pig Latin it!",
:url => { :action => "piglatin_sentence" },
:submit => "fakeForm" %></p>
```

我们没有指示客户端应该更改什么，而是在服务器端执行此操作：

```ruby
output = "Element.update($('headline'), "#{$sentence}");"
render :text => output, :content_type => "text/javascript"
```

换句话说，我们告诉控制器生成类型为 `text/javascript` 的响应，知道我们发送的任何内容都将被用户浏览器执行。然后我们发送一个响应，使用 `Element.update` 将标题更改为我们翻译的句子。果然，一旦安装了软件的这个新版本，标题继续被更改。

与此相关的功能巨大。例如，我们可以有条件地更新标题，通过检查服务器数据库中禁用词的字典。我们可以记录最常使用的单词。我们可以限制用户每天更新标题的次数。

更棒的是，因为我们返回的是一个 JavaScript 程序，而不是单个 HTML 元素的内容，我们可以修改页面的多个部分，甚至加入一些 Scriptaculous 效果以增强效果。返回 JavaScript 是 Prototype 提供的一个看似简单的功能，但它为巨大的可能性打开了大门。

# RJS

现在，你一直在等待的时刻来临——你可能会觉得：它功能强大，但在 Ruby 控制器中创建和维护 JavaScript 代码很麻烦。需要在里面包含 SQL 已经够糟了；在单个文件中使用三种语言似乎有点过头了。
