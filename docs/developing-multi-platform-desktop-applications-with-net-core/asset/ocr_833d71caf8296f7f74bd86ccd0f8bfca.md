https://docs.microsoft.com/en-us/visualstudio/msbuild/

/docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-
project-file-schema-reference

https://docs.microsoft.com/en-
us/dotnet/core/tools/csproj

# 9.4  CORDER (AHEAD OF TIME) COMPILATION

**Warning**: CoreRT is an experimental tool from Microsoft and there is no plan that it will be released as a standalone tool in the future. This has been said, CoreRT is an amazing tool allowing the generation of a machine native executable for a .NET Core 3 project.

CoreRT is an Opensource tool from Microsoft who bring native compilation possibilities to .NET Core applications. The production of a native executable file is big achievement in the managed development world.

CoreRT can be used for targetting a wide range of platform OS Windows, Linux and macOS. This tool provides the same performances level for .NET Core software as a native C++ solution can provides. CoreRT provides to the .NET Core 3 the same features as .NET Natives furnish for the .NET framework.

Even if many constraints and bugs have been found for the compilation of a Web application, CoreRT seems to work just fine for console and libraries projects (these are the types we are interested in).

This is a new technology, introduces by Microsoft for improving the performances of .NET Core software whatever the platform OS the software is running on. This tool is still under heavy development