# # 2.3 Testing

To test our ASP.NET 5, we use code samples from [https://github.com/aspnet/Home](https://github.com/aspnet/Home) . We clone this code samples and then restore all required libraries using dnu command. Type these commands.

```
$ git clone https://github.com/aspnet/Home
$ cd Home
$ dnu restore
```

If you don’t git on your OS X, you can install it via brew.

```
$ brew install git
```

![](bbox=[0.13, 0.39, 0.87, 0.71])

Now you are ready to run code samples.

# ## 2.3.1 ASP.NET Console

To run ASP.NET Console, we can use dnx. Firstly, navigate to ConsoleApp project. Type these commands.