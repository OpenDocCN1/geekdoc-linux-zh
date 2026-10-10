# **9.1** .NET Core CLI LOCAL TOOLS

.NET Core application development, the dependencies are managed by NuGet packages providing a better way than in the classical .NET framework to keep your dependencies up to date.

This architecture provides consistency and maintainability of the dependencies used for the application you develop. This is key foundation of the .NET Core framework; every specialized functionality has to be integrated via a specific NuGet package.

You can resolve the update of the packages with the restore command of the dotnet CLI on the project.

If you tried local tools in .NET Core 3.0, such as running “dotnet tool restore” or “dotnet tool install”, delete the local tools cache folder. Otherwise, local tools won’t work on any newer release. This folder is located at:

**On macOS and Linux:**

```
`@user>rm -r $HOME/.dotnet/toolResolverCache`
```

**On Windows:**

```
```console
C:\>rmdir  /s
%USERPROFILE%\ .dotnet\toolResolverCache```
```

Local tools rely on a manifest file named “dotnet-tools.json” in the current project directory (dotnet folder). This manifest file defines if the tool(s) is available. You can distribute the manifest file with your code to ensure that anyone who works with your code can restore and use the same tools.