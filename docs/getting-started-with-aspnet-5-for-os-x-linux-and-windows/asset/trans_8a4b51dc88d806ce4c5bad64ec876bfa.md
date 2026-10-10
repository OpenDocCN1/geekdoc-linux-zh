

```csharp
public double Add(double a, double b)
{
    return a + b;
}

public void DemoMath(double a, double b)
{
    Console.WriteLine("cos({0}) = {1}", a, Math.Cos(a));
    Console.WriteLine("sin({0}) = {1}", b, Math.Sin(b));
    Console.WriteLine("exp({0}) = {1}", a, Math.Exp(a));
}
```

下一步是创建主程序。创建一个文件，**Program.cs**，并编写以下代码。

```csharp
using System;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("===Demo Simple Math===");
        double a = 0.2;
        double b = 3.5;

        SimpleMath o = new SimpleMath();
        double result = o.Add(a, b);
        Console.WriteLine("{0} + {1} = {2}", a, b, result);

        o.DemoMath(a, b);

        Console.WriteLine("Done");
    }
}
```

保存所有文件。

以下是我们的项目结构。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_52_0.png)

## 5.2.3 测试

现在您可以测试该程序了。首先，我们使用 `dnu` 加载所有必需的库。然后，使用 `dnx` 执行该程序。

```bash
dnu restore
dnx . run .
```

如果成功，您将看到程序的输出。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_53_0.png)

## 5.3 构建 ASP.NET 5 MVC 应用程序

第二个演示是构建一个 ASP.NET 5 MVC 应用程序。我们开发一个简单的输入表单并利用 ASP.NET MVC 会话。以下是我们的场景：

- 用户填写表格以创建新项目
- 用户点击保存按钮以保存数据
- 数据将被存储到一个会话堆栈中
- 然后，数据将在另一个页面中显示

让我们开始开发吧。

### 5.3.1 创建项目

首先，我们通过创建一个名为 WebDemo 的文件夹来创建项目。然后，您创建以下文件夹：

- Controllers
- Models
- Properties
- Views
- wwwroot

您可以在下图中看到项目结构。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_55_0.png)

我们需要在项目的根目录中有一个配置文件，称为 **project.json**。它包含必需的库。请为 project.json 文件编写此脚本。

```json
{
  "version": "1.0.0-*",
  "webroot": "wwwroot",
  "exclude": [
    "wwwRoot"
  ],
  "packExclude": [
    "**.kproj",
    "**.user",
    "**.vspcc"
  ],
  "dependencies": {
    "Kestrel": "1.0.0-*",
    "Microsoft.AspNet.Diagnostics": "1.0.0-*",
    "Microsoft.AspNet.Mvc": "6.0.0-*",
    "Microsoft.AspNet.Server.IIS": "1.0.0-*",
    "Microsoft.AspNet.Server.WebListener": "1.0.0-*",
    "Microsoft.AspNet.Session": "1.0.0-*"
  },
  "commands": {
    "web": "Microsoft.AspNet.Hosting --server Microsoft.AspNet.Server.WebListener --server.urls http://localhost:5001",
    "kestrel": "Microsoft.AspNet.Hosting --server Kestrel --server.urls http://localhost:5004"
  },
  "frameworks": {
    "dnx451": {},
    "dnxcore50": {}
  }
}
```

应用程序将通过执行 **Startup.cs** 文件启动。创建此文件并编写以下代码。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Framework.DependencyInjection;

namespace WebDemo
{
    public class Startup
    {
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
        }
        
        public void Configure(IApplicationBuilder app)
        {
            // handle error page
            app.UseErrorPage();
            // handle session
            app.UseInMemorySession();
            // aspNet routing
            app.UseMvc(routes =>
            {
                routes.MapRoute("default", "{controller=Home}/{action=Index}");
            });
        }
    }
}
```

我们还添加 **launchSettings.json** 来配置如何执行程序。将其存储在 Properties 文件夹中。请为 **launchSettings.json** 文件编写此脚本。

```json
{
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNET_ENV": "Development"
      }
    },
    "kestrel": {
      "commandName": "kestrel",
      "launchBrowser": true,
      "launchUrl": "http://localhost:5004"
    },
    "web": {
      "commandName": "web",
      "launchBrowser": true,
      "launchUrl": "http://localhost:5001"
    }
  }
}
```

### 5.3.2 编写程序

在本节中，我们将编写我们的 ASP.NET 5 MVC 程序。

#### 5.3.2.1 创建模型

模型持有数据。在我们的情况下，我们创建一个名为 Product 的模型，它由四个属性组成。创建一个文件，称为 **Product.cs**，并编写以下代码。

```csharp
using System.ComponentModel.DataAnnotations;

namespace WebDemo.Web.Models
{
    public class Product
    {
        [Required]
        [MinLength(4)]
        [Display(Name = "Name")]
        public string Name { get; set; }
        [Display(Name = "Product Code")]
        public string ProductCode { get; set; }
        [Display(Name = "Quantity")]
        public int Quantity { get; set; }
        [Display(Name = "Is Discount")]
        public bool IsDiscount { get; set; }
    }
}
```

将此文件保存到 Models 文件夹中。

#### 5.3.2.2 创建控制器

现在我们将创建名为 Home 控制器的 MVC 控制器。创建一个文件，称为 **HomeController.cs**，并编写以下代码。

```csharp
using System;
using Microsoft.AspNet.Mvc;
using Microsoft.AspNet.Http;
using WebDemo.Web.Models;

namespace WebDemo.Web.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return View();
        }

        public IActionResult Create()
        {
            var product = new Product();
            return View(product);
        }

        [HttpPost]
        public IActionResult Create(Product obj)
        {
            // do database processing
            /////////////////
            // for testing, save it into a session
            Context.Session.SetString("name", obj.Name);
            Context.Session.SetString("code", obj.ProductCode);
            Context.Session.SetInt("quantity", obj.Quantity);
            Context.Session.SetString("discount", obj.IsDiscount.ToString());

            return RedirectToAction("Save");
        }

        public IActionResult Save()
        {
            var product = new Product();
            product.Name = Context.Session.GetString("name");
            product.ProductCode = Context.Session.GetString("code");
            product.Quantity = (int)Context.Session.GetInt("quantity");
            product.IsDiscount = Convert.ToBoolean(Context.Session.GetString("discount"));
            return View(product);
        }
    }
}
```

#### 5.3.2.3 创建视图

我们创建三个页面：

- Index.cshtml
- Create.cshtml
- Save.cshtml

我们还创建一个布局，称为 **Shared.cshtml**。编写此脚本。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewBag.Title - My ASP.NET Application</title>
    <link rel="stylesheet" href="//netdna.bootstrapcdn.com/bootstrap/3.0.3/css/bootstrap.min.css" />
</head>
<body>
    <div class="navbar navbar-inverse navbar-fixed-top">
        <div class="container">
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
            </div>
            <div class="navbar-collapse collapse">
                <ul class="nav navbar-nav">
                    <li><a href="/">Home</a></li>
                </ul>
            </div>
        </div>
    </div>
    <div class="container body-content">
        @RenderBody()
        <footer>
            <p>&copy; @DateTime.Now.Year - My ASP.NET Application</p>
        </footer>
    </div>
</body>
</html>
```

以下是 **Index.cshtml** 文件的脚本。

```html
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "Home Page";
}

<div class="jumbotron">
    <h1>ASP.NET MVC Demo</h1>
    <p class="lead">Filling and submitting a form.</p>
    <p><a href="/Home/Create" class="btn btn-primary btn-lg">Create</a></p>
</div>
```

以下是 **Create.cshtml** 文件的脚本。

```html
@using WebDemo.Web.Models
@model Product
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "Create Product";
}

<div class="jumbotron">
    <h1>ASP.NET</h1>
    <p class="lead">Create a new product. Fill this form. Then, click Save.</p>
</div>

@using (Html.BeginForm())
{
    <fieldset>
        <legend>Create a new Product</legend>

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
            @Html.TextBoxFor(model => model.ProductCode)
        </div>
        <br/>

        <div class="editor-label">
            @Html.LabelFor(model => model.Quantity)
        </div>
        <div class="editor-field">
            @Html.TextBoxFor(model => model.Quantity)
        </div>
        <br/>

        <div class="editor-label">
            <div style="float: left;">
                @Html.CheckBoxFor(model => model.IsDiscount)
            </div>
            @Html.LabelFor(model => model.IsDiscount)
        </div>
        <br/>
        <div>
            <input type="submit" value="Save" />
        </div>
    </fieldset>
}
```

