# ## 6.3 Writing Program

In this section, we write our ASP.NET 5 MVC program.

# ### 6.3.1 Creating Model

Firstly, we create a model, called Product. The following is code implementation.

```
```
using System.ComponentModel.DataAnnotations;

namespace WebDemo.Web.Models
{
    public class Product
    {
        [Required]
        [MinLength(4)]
        [Display( Name = "Name" )]
        public string Name { get; set; }
        [Display( Name = "Product Code" )]
        public string ProductCode { get; set; }
        [Display( Name = "Quantity" )]
        public int Quantity { get; set; }
        [Display( Name = "Price" )]
        public double Price { get; set; }
    }
}
```
```

Save this code into a file, called Product.cs and store it into Models folder.

# ### 6.3.2 DUMMY Database

In this case, we don't access database directly so we create a dummy database which generates product data. Create a file, called DumpDatabase.cs and write this code.

```
```
using System;
using System.Collections.Generic;

using WebDemo.Web.Models;
namespace WebDemo.Web.Database
{
    public class DumpDatabase
    {
        private DumpDatabase(){}
        public static List<Product> GetAllProducts()
```
```