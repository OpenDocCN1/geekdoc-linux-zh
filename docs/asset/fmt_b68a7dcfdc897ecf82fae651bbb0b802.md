
一些聪明的程序员，为了更加完善和省力地实现`JavaScript`标准化，更进一步。为什么不用您的服务器端编程语言为您生成`JavaScript`？也就是说，如果您使用`Ruby on Rails`，也许您可以编写`Ruby`命令并将其翻译为`JavaScript`。这样做将允许您在所有模板中使用大致相同的代码，而无需在模板的不同部分切换语法。

这听起来可能像个怪念头，但越想越觉得它不错。`RJS`（`Ruby JavaScript`的缩写）模板就是这种理念的一种体现。如果您更喜欢用`Java`创建`JavaScript`，不妨看看`Google Web Toolkit`，它现已采用开源许可证发布，并在`Java`界赢得了众多粉丝。

本月，我们将探讨`RJS`及其如何让`Web`开发者的生活变得轻松许多。虽然我认为`JavaScript`不会消失，`Web`开发者也无法完全无视它，但`RJS`等技术意味着它可能变得像今天的机器代码——可用且位于金字塔底层，但通常被高级程序员忽略。

![](img/526fd434dcfcf1b461b94c24ea170f36_19_1.png)

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
<html>  
 <head>  
 <title id="title">Sample HTML page</title>  
 <% javascript_include_tag 'prototype' %>  
  
 <script type="text/javascript">  
 function updateHeadline()  
 {  
 var headline = $('headline');  
 var new_headline_text = $('future-headline');  
 Element.update(headline, new_headline_text);  
 }  
 </script>  
 </head>  
  
 <body>  
 <h1 id="headline">Headline</h1>  
 <p><input type="text" id="future-headline" /></p>  
 <p><input type="button" onclick="updateHeadline();" value="Update headline" /></p>  
 </body>  
</html>
```

# Ajax 与 Rails

要创建一个名为`ajaxdemo`的新`Rails`项目，请输入：

```bash
rails ajaxdemo
```

现在，让我们创建一个名为`showme`的简单控制器：

```bash
script/generate controller showme
```

该系统不会有任何模型，但您可能仍需在`config/database.yml`中定义一行或多行。相反，让我们在`showme`控制器中创建一个新视图，存储为`app/views/showme/index.rhtml`，如清单 1 所示。

如您所见，`index.rhtml`页面是一个相对标准的`HTML`页面，包含一些使用`Prototype`库的`JavaScript`代码。该页面由一个标题、一个文本框和一个按钮组成。按下按钮会调用

![](img/526fd434dcfcf1b461b94c24ea170f36_20_0.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_20_1.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_20_2.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_20_3.png)

>>>>> 低至$789 <<<<<

使用`Pogo`的网络附加存储设备，与最流行操作系统实现最大程度的互操作性变得更容易。通过易于使用的图形管理界面、多个快照、内置备份、`IP`故障转移和增强安全性，掌控您不断增长的存储需求。由`Intel`双核`Xeon`处理器和快速`64`位操作系统提供动力。今日致电了解更多。

![](img/526fd434dcfcf1b461b94c24ea170f36_20_4.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_20_5.png)

`www.pogolinux.com`

经验、想象力与支持。

`Pogo Linux`是专为`Linux`构建、专为您的硬件解决方案。

要开始合作，请联系`888.828.POGO`或`inquries07@pogolinux.com`

`Pogo Linux, Inc.` `701 Fifth Ave. Suite 6850, Seattle, WA 98104`

`Intel`、`Intel logo`、`Intel Inside logo`、`Pentium`、`Xeon`和`Xeon Inside`是`Intel corporation`或其子公司在美国和其他国家的商标或注册商标。更多条款和条件请访问`www.pogolinux.com`

更棒的是，因为我们返回的是`JavaScript`程序，而非单个`HTML`元素的内容，我们可以修改页面的多个部分，甚至加入一些`Scriptaculous`效果以助一臂之力。

`function updateHeadline`。此函数获取`future-headline`文本框的当前值，并更改标题以反映其内容。

# 使用远程调用

到目前为止，我们还没做什么特别的事。然而，现在我们要做点稍微复杂的事：通过`Ajax`调用将文本框的内容发送到服务器。服务器的响应将是我们标题的猪猪语（`Pig Latin`）翻译。

进行此更改需要做两件事。首先，我们需要在应用程序控制器中编写一个方法，该方法接收标题，将其转换为猪猪语，然后返回该文本。其次，我们需要修改模板，使其从服务器获取更新后的文本，而不是从本地`JavaScript`函数获取。

我们更新后的模板如清单 2 所示。我们做了许多更改，首先是我们的表单现在关联了一个名为`theForm`的`id`属性。表单包含单个元素，即名为`future_headline`的文本框。请注意，我们需要使用`name`属性而不是`id`属性，以便表单元素随我们的`Ajax`调用一起提交。还要注意，我们将名称更改为对`Ruby`友好的`future_headline`（带下划线），而非对`CSS`友好的`future-headline`（带连字符）。

## 清单 2. index.rhtml (Ajax 版本)

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title id="title">Sample HTML page</title>
<%= javascript_include_tag 'prototype' %>
</head>
<body>
<h1 id="headline">Headline</h1>
<form id="theForm">
<p><input type="text" name="future_headline" /></p>
</form>
<p><%= submit_to_remote "submit-button",
"Pig Latin it!",
:url => { :action => "piglatin_sentence" },
:submit => "fakeForm",
:update => "headline" %></p>
</body>
</html>
```

我们还用对`submit_to_remote`辅助方法的调用替代了按钮。

```erb
<p><%= submit_to_remote "submit-button",
"Pig Latin it!",
:url => { :action => "piglatin_sentence" },
:submit => "fakeForm",
:update => "headline" %></p>
```

上述代码执行了多项操作：

- 创建一个按钮，其`DOM ID`为`submit-button`。
- 按钮的标签为`"Pig Latin it!"`。
- 点击该按钮时，使用`Ajax`在服务器上的当前控制器中调用`piglatin_sentence`动作。

## 清单 3. showme_controller.rb
