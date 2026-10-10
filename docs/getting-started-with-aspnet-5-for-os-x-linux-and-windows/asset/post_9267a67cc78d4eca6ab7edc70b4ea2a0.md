
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

The next step is to create a main program. Create a file, **Program.cs**, and write this code.

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

Save all files.

The following is our project structure.

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_52_0.png)

## 5.2.3 Testing

Now you can test the program. Firstly, we load all required libraries using `dnu`. Then, we execute the program using `dnx`.

```bash
dnu restore
dnx . run .
```

If success, you can see the program output.

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_53_0.png)

## 5.3 Building ASP.NET 5 MVC Application

The second demo is to build an ASP.NET 5 MVC application. We develop a simple entry form and utilize ASP.NET MVC session. The following is our scenario:

- User fills a form to create a new project
- User clicks Save button to save the data
- The data will be stored to a session stack
- Then, the data will be shown in another page

Let’s start to develop.

### 5.3.1 Creating a Project

Firstly, we create a project by creating a folder, called WebDemo. Then, you create the following folders:

- Controllers
- Models
- Properties
- Views
- wwwroot

You can see the project structure on the Figure below.

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_55_0.png)

We need a config file, called **project.json**, in the project root folder. It consists of required libraries. Please write this script for project.json file.

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

App will start by executing **Startup.cs** file. Create this file and write this code.

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

We also add **launchSettings.json** to configure how to execute the program. Store it on Properties folder. Write this script for **launchSettings.json** file.

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

### 5.3.2 Writing Program

In this section, we write our ASP.NET 5 MVC program.

#### 5.3.2.1 Creating Model

A model holds a data. In our case, we create a model, called Product, which consists of four properties. Create a file, called **Product.cs**, and write this code.

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

Save this file into Models folder.

#### 5.3.2.2 Creating Controller

Now we create MVC controller, called Home controller. Create a file, called **HomeController.cs**, and write this code.

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

#### 5.3.2.3 Creating View

We create three pages:

- Index.cshtml
- Create.cshtml
- Save.cshtml

We also create a layout, called **Shared.cshtml**. Write this script.

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

The following is a script for **Index.cshtml** file.

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

The following is a script for **Create.cshtml** file.

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
