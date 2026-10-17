
```html
@{
    Layout = "_Shared/_Layout";
    ViewBag.Title = "Home Page";
}
<div class="jumbotron">
  <h1>ASP.NET MVC Demo</h1>
  <p class="lead">Access ASP.NET API.</p>
  <p><a href="#" id="get-data" class="btn btn-primary">Get JSON data</a></p>
  <span id="show-data"></span>
</div>
<table id="myTable" class="table">
  <thead>
    <tr>
      <th>Product Name</th>
      <th>Quantity</th>
      <th>Is Discount</th>
    </tr>
  </thead>
  <tbody>
    <!-- Data will be loaded -->
  </tbody>
</table>

<script>
$(document).ready(function () {
  $('#get-data').click(function () {
    var showData = $('#show-data');

    $.getJSON('/product/get', function (data) {
      console.log(data);

      var tableRef = document.getElementById('myTable').getElementsByTagName('tbody')[0];
      for (var i = 0; i < data.length; i++) {
        var newRow = tableRef.insertRow(tableRef.rows.length);
        var newCell1 = newRow.insertCell(0);
        var newText1 = document.createTextNode(data[i].name);
        newCell1.appendChild(newText1);
        var newCell2 = newRow.insertCell(1);
        var newText2 = document.createTextNode(data[i].productCode);
        newCell2.appendChild(newText2);
        var newCell3 = newRow.insertCell(2);
        var newText3 = document.createTextNode(data[i].quantity);
        newCell3.appendChild(newText3);
        var newCell4 = newRow.insertCell(3);
        var newText4 = document.createTextNode(data[i].isDiscount);
        newCell4.appendChild(newText4);
      }
    });
    showData.text('Loading the JSON file.');
  });
});
</script>
```

# ASP.NET Core MVC 演示

访问 ASP.NET Core API。

```
获取 JSON 数据 »
```

| 产品名称 | 编码 | 数量 | 是否有折扣 |
|---|---|---|---|
| 产品 0 | PR0 | 0 | true |
| 产品 1 | PR1 | 1 | true |
| 产品 2 | PR2 | 2 | true |
| 产品 3 | PR3 | 3 | true |
| 产品 4 | PR4 | 4 | true |
| 产品 5 | PR5 | 5 | true |
| 产品 6 | PR6 | 6 | true |
| 产品 7 | PR7 | 7 | true |
| 产品 8 | PR8 | 8 | true |
| 产品 9 | PR9 | 9 | true |

# 5. ASP.NET Core 与 Angular 2

在本章中，我将介绍如何配合 ASP.NET Core MVC 和 Angular 2 进行工作。

## 5.1 入门

在本节中，我们将开发一个简单的应用程序来配合 ASP.NET RESTful 和 AngularJS 使用。

AngularJS 是由 Google 维护的开源 JavaScript 框架，你可以访问其官方网站 `http://angularjs.org/`。

在本章中，我们将探索如何将 Angular 2 集成到 ASP.NET Core 中。

## 5.2 ASP.NET Core 和 Angular 2 项目模板

你可以在官方网站 `https://angular.io` 学习 Angular 2。我们使用 JavaScript 和 TypeScript 开发 Angular 2。

将 ASP.NET Core MVC 和 Angular 2 整合的思路是将这两个项目（ASP.NET Core 和 Angular 2）合并。幸运的是，我们可以使用 `aspnetcore` `spa` 模板，`https://github.com/aspnet/JavaScriptServices`。

你可以在终端中输入此命令来使用该模板。

```
$ npm install -g yo generator-aspnetcore-spa
```

如果完成，你可以从此项目模板构建一个示例项目。

## 5.3 运行演示：ASP.NET Core Angular SPA

在本节中，我们运行 `aspnetcore` `spa` 模板中的程序示例。

### 5.3.1 创建项目

你可以通过输入以下命令创建带有 Angular 2 的 ASP.NET Core。

```
$ yo aspnetcore-spa
```

选择 Angular 2 作为框架。

# aspnetcore_angular2 — yo TERM_PROGRAM=Apple_Terminal — 80x24

```
agusk$$ cd aspnetcore_angular2/
agusk$$ yo
? 'Allo Agus! 你想做什么? Aspnetcore Spa

请确保你处于想要脚手架的目录中。
此生成器也可以通过以下命令运行：yo aspnetcore-spa
```

![](img/03410162e36ac22ee4df2780b4d3848c_41_0.png)

- 框架
- Angular 2
- Aurelia
- Knockout
- React
- 带 Redux 的 React

给项目命名命名，称为 ProductAng。

# aspnetcore_angular2 — yo TERM_PROGRAM=Apple_Terminal — 80x24

```
agusk$$ cd aspnetcore_angular2/
agusk$$ yo
? 'Allo Agus! 你想做什么? Aspnetcore Spa

请确保你处于想要脚手架的目录中。
此生成器也可以通过以下命令运行：yo aspnetcore-spa
```

![](img/03410162e36ac22ee4df2780b4d3848c_41_1.png)

- 框架 Angular 2。
- 你想创建什么类型的项目？`project.json` (兼容 .NET Core 工具预览 2 和 Visual Studio 2015)
- 你想包含单元测试吗？否
- 你的项目名称 (`aspnetcore_angular2`) ProductAng

### 5.3.2 运行程序

要运行程序，像往常一样操作。打开终端并导航到项目文件夹。然后输入这些命令。

```
$ dotnet restore
$ dotnet build
$ dotnet run
```

打开浏览器并导航到 `http://localhost:5000/`。你应该能看到带有 Angular 2 的 SPA。

![](img/03410162e36ac22ee4df2780b4d3848c_42_0.png)

## Hello, world!

欢迎来到你的新单页应用，它构建于：

- 用于跨平台服务器代码的 ASP.NET Core 和 C#
- 用于客户端代码的 Angular 2 和 TypeScript
- 用于构建和打包客户端资源的 Webpack
- 用于布局和样式的 Bootstrap

为了帮助你入门，我们已经设置了：

- 客户端导航。例如，点击 Counter 然后点击 Back 返回此处。
