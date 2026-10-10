```
<TrimmerRootAssembly_Include="System.IO">
</ItemGroup>
```

TIPS: Here is the useful example (that you can reuse in your own project) of .csproj file for the creation of a single small executable with no dependencies.

```
<Project Sdk="Microsoft.NET.sdk">
<PropertyGroup>
<OutputType>Exe</OutputType>
<TargetFramework>netcoreapp3.0</TargetFramework>
<PublishTrimmed>true</PublishTrimmed>
<PublishReadyToRun>true</PublishReadyToRun>
<PublishSingleFile>true</PublishSingleFile>
<RuntimeIdentifier>win-x64</RuntimeIdentifier>
</PropertyGroup>
</Project>
```

The example above, .csproj file will trigger the build of a Windows native compiled single file application.

This is only an overview of the possibilities offered by using the .csproj file (and MSBuild) options, this tool is very flexible and can be adapted to many project requirements.

You can consult the very well-done documentation about the .csproj file configuration and MSBuild on the Microsoft's reference links below.