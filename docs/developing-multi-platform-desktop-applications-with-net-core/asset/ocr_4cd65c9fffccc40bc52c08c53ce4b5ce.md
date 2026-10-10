# CHAPTER 5: BASIC CODING TECHNIQUES FOR C# APPLICATION

![](bbox=[0.05, 0.09, 0.95, 0.22])

In conclusion about the use of configuration file with .NET Core3, the basic configuration tools offered by the Microsoft package are quite powerful and fit to most of applications requirements. There are providers for many types of configuration files (JSON, XML, INI ...). And, of course, you can write your own provider if you have special requirement in this matter.

You can retrieve a working example project on the netcore3 GitHub.

![](bbox=[0.05, 0.51, 0.95, 0.6])

# 5.2 LOGGING AND TRACING

.NET Core have a built in Logging/Trace mechanism. This mechanism is really handy for basic logging requirements. But if you have the need of more advanced logging mechanism (for using in error handling automation system for example) you have to use a more advanced tool.

There is a plenty of solution (you can check the NuGet repository) for implementing structured logging system to your application, the most used and popular are Log4NET, NLog and Serilog.