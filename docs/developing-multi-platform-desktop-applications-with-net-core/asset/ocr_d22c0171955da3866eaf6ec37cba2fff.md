Here is a simple sample of a .csproj file :

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.0</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference
Include="Microsoft.Extensions.Configurations" >
</ItemGroup>
</Project>
```

> (csproj figure 1)

The “.csproj” file consists in two sections; these sections are child of the main node**<Project>** (see csproj figure 1):

+   **<PropertyGroup>:** This section contains a set of properties relatives to the project; these properties are used by MSBuild for the generation of an executable (MSIL or Native).

You have also the possibility to add a conditional attribute regarding the environment where the build is performed or the options chosen in the code.

+   **<TargetFramework>:** Specify the framework used by the application, this is a mandatory entry of the .csproj file. You can specify multiple frameworks (comma separated).

+   **<OutputType>:** Specify the executable output type

+   **<AssemblyName>:** This is the assembly name.

+   **<OutputPath>:** This is the path where the output file built will be copied.