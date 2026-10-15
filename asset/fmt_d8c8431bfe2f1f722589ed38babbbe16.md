
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using PostgresDemo.Data;
using PostgresDemo.Models;

namespace PostgresDemo.Controllers
{
    public class ProductController : Controller
    {
        private readonly ProductRepo _productRepository;
        public ProductController(DemoDbContext databaseContext)
        {
            _productRepository = new ProductRepo(databaseContext);
        }

        public IActionResult Index()
        {
            return View();
        }

        public IActionResult Create()
        {
            return View();
        }
        [HttpPost]
        public IActionResult Create(ProductViewModel obj)
        {
            // 数据库处理
            ////
            Product o = new Product();
            o.Id = obj.Id;
            o.Name = obj.Name;
            o.ProductCode = obj.ProductCode;
            o.Quantity = obj.Quantity;
            o.IsDiscount = obj.IsDiscount;
            _productRepository.Save(o);
            return RedirectToAction("Save");
        }

        public IActionResult Save()
        {
            return View();
        }

        public IActionResult ActionResult ListProduct()
        {
            return View(new ProductViewModel());
        }
        [HttpPost]
        public IActionResult List(string code)
        {
            Product obj = _productRepository.GetProductByCode(code);
            ProductViewModel o = new ProductViewModel();
            if(o!=null)
            {
                o.Id = obj.Id;
                o.Name = obj.Name;
                o.ProductCode = obj.ProductCode;
                o.Quantity = obj.Quantity;
                o.IsDiscount = obj.IsDiscount;
            }
            return View(o);
        }
    }
}
```

为了在项目中激活 EF Core，我们在 `Startup.cs` 文件的 `ConfigureServices()` 方法中添加数据库上下文。添加这些代码。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // 添加框架服务。
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlite(Configuration.ConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddMvc();

    // 添加 postgresql
    var connectionString = Configuration["DbContextSettings:ConnectionString"];
    services.AddDbContext<DemoDbContext>(opts => opts.UseNpgsql(connectionString));

    // 添加应用服务。
    services.AddTransient<IEmailSender, AuthMessageSender>();
    services.AddTransient<ISmsSender, AuthMessageSender>();
}
```

### 6.4.6 开发 ASP.NET Core MVC 视图

开发完 Controller 后，我们开发视图。我们在 Views 中创建 Product。然后创建如图所示的四个视图文件。

![](img/03410162e36ac22ee4df2780b4d3848c_52_0.png)

以下是 `Index.cshtml` 文件的实现。

```cshtml
@{
  Layout = "Views/Shared/Layout.cshtml";
  ViewBag.Title = "Home Page";
}

<div class="jumbotron">
  <h1>AS.NET Core MVC Demo //</h1>
  <p class="lead">填写并提交表单。</p>
  <p><a href="/Create" class="btn btn-primary btn-large">Create &raquo;</a></p>
</div
```

以下是 `Create.cshtml` 文件的实现。
