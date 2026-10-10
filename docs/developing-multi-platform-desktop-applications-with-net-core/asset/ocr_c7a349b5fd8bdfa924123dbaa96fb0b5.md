```
```xml
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.0</TargetFramework>
<EnableDefaultCompileItems>false</EnableDefaultCompileItems>
```
```
```
```

+   Platform build target specification

An important variable to set in the .csproj file, is the PID (for Platform Identification, optional). This variable specifies the OS platform for building a native .NET Core binary for the platform specified (not machine native).

+   Single Exe

The .csproj file allow you also to produce a single exe for your project, this can be done by setting the suitable variable as described below.

A single executable can be produced by the build process when you specify simultaneously “PublishSingleFile” and the platform you target (Rid) “RuntimeIdentifier” (as described in the snippet below).

```
```xml
<PropertyGroup>
<PublishSingleFile>true</PublishSingleFile>
<RuntimeIdentifier>win-x64</RuntimeIdentifier>
</PropertyGroup>
```
```
```

The “PublishTrimmed” option allow to use only dependencies that are actually used in the program, but you have to specify them (as described in the snippet below). You have to specify the dependencies reflection used as well.

```
```xml
<ItemGroup>
```
```
```