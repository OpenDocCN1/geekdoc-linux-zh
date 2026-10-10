Furthermore, the .NET framework is a part of the Windows system, that's not the case for .NET Core 3 who can be distributed with the application in a self-contain manner and is self-sufficient on its own.

The well though architecture of the .NET Core provides many benefits for its exploitation in a production environment as you can see (figure 1) compared to the classical .NET framework (who is Windows dependent).

| .NET framework | .NET Core 3 |
| Windows Update | Yes | No |
| Deploy Runtime | Depends | Yes |
| Side by Side install | No | Yes |

(figure1)
(Source Microsoft)

A key point in the .NET Core is the use of a dedicated packet manager format: NuGet.

The NuGet packaging system is integrated in Visual Studio 2019 and is like APT for Debian, NPM for Node.js or pip for Python. NuGet allows the availability of every and each library by encapsulating binaries and their dependencies inside a single file. This file (.nupkg extension) is a ZIP archive who contains a manifest with all the associated dependencies and the targeted frameworks information.

Thus, a NuGet package can implement a complete feature on its own for a multiplatform use.