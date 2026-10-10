Once you have chosen the platform you want to perform the building process among those RIDs, you can use the “publish” command. The RID can be specified in the publish command line or inside the .csproj file.

Here is a sample command line instruction for actually generating the final native executable for windows 64, this command is working if you are in the application folder, if this is not the case you have to specify the path where the compiler can find the .csproj file of the project.

```
```text
C:\appFolder> dotnet publish -c release -r win-x64
```
```

Here is the same command line example for targeting macOS (on macOS).

```
```bash
$ dotnet publish -c release -r osx-x64
```
```

**Be careful**, you cannot build a release targeting the macOS or Linux platform on the Windows since CoreRT does not provide cross-platform build feature.

# C) Publishing with CoreRT using Visual Studio

Cherry on top, you can actually build the machine native executable (for Windows) of your .NET Core 3 application directly from Visual Studio 2019 by using the “Publish” option of the contextual menu