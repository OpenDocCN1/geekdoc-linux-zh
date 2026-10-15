
![](img/03410162e36ac22ee4df2780b4d3848c_23_0.png)

我们还创建了一个布局文件 `_Shared.cshtml`。它用于视图模板。编写此脚本。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ViewBag.Title - 我的 ASP.NET MVC Core </title>
    <link rel="stylesheet" href="https://cdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVvYiISFekIdGmRYakcuHARgR32EdUcww7n3YJgdV4PmStssz/K8vdbE4jh4u" />
</head>
<body>
    <div class="navbar navbar-inverse navbar-fixed-top">
        <div class="container">
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="navbar">
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
            </div>
            <div class="navbar-collapse collapse">
                <ul class="navbar-nav">
                    <li><a href="/">首页</a>a></li>
                </ul>
            </div>
        </div>
    </div>
    <div class="container body-content">
        @RenderBody()
    </div>
    <footer>
        <p>@copy Date.Now.Year - 我的 ASP.NET MVC Core 应用程序</p>
    </footer>
</body>
</html>
```

### `Index.cshtml` 文件的脚本

```razor
{
  Layout = "/Views/Shared/_Layout.cshtml";
  ViewBag.Title = "首页";
}
<div class="jumbotron">
  <h1>ASP.NET Core MVC 演示</h1>
  <p class="lead"> 填写并提交表单。</p>
  <p><a href="/Home/Create" class="btn btn-primary btn-large">创建 &rsquo;</a</p>
</div>
```

### `Create.cshtml` 文件的脚本

```razor
@using ProductApp.Models
@model Product
{
  Layout = "/Views/Shared/_Layout.cshtml";
  ViewBag.Title = "创建产品";
}
<div class="jumbotron">
  <h1>ASP.NET MVC Core</h1>
  <p class="lead">创建一个新产品。填写此表单。完成后，点击保存按钮。</p>
</div>
@using Html.BeginForm() {
  <fieldset>
    <legend>创建一个新产品</legend>
    <div class="editor-label">
      @Html.LabelFor(model => model.Name)
    </div>
    <div class="editor-field">
      @Html.TextBoxFor(model => model.Name)
    </div>
    <br/>
    <div class="editor-label">
      @Html.LabelFor(model => model.ProductCode)
    </div>
    <div class="editor-field">
      @Html.TextBoxFor(model => model.ProductCode )
    </div>
    <br/>
    <div class="editor-label">
      @Html.LabelFor(model => model.Quantity)
    </div>
    <div class="editor-field">
      @Html.TextBoxFor(model => model.Quantity )
    </div>
  </fieldset>
<div class="editor-label">
  <div style="float: left;">
    @Html.CheckboxFor(model => model.IsDiscount)
  </div>

  @Html.LabelFor(model => model.IsDiscount)
</div>
<br/>

  <input type="submit" value="保存" />
</fieldset>
```

### `Save.cshtml` 文件的脚本

```razor
@using ProductApp.Models
@model Product
{
  Layout = "/Views/Shared/_Layout.cshtml";
  ViewBag.Title = "保存产品";
}
<div class="jumbotron">
  <h1>ASP.NET Core MVC 演示</h1>
  <p class="lead"> 保存产品。</p>
  <p><a href="/Home/Create" class="btn btn-primary btn-large">创建 &rsquo;</a</p>
</div>
```

App 将通过执行 `Startup.cs` 文件启动。请修改此文件并写入以下代码。
