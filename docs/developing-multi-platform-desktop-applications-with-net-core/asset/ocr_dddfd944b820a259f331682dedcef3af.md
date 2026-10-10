```
```xml
<AllFruits Include="Pear"
    Condition="$ (Pear) == true" />
</ItemGroup>
...
<Message Text="@ (AllFruits)"/>
</Target>
```
```

+   - Default compilation includes

MSBuild have predefined folder and file type who imply default behavior during the compilation and the building process. The default includes and excludes configuration are built-in the .NET Core SDK. This default compiling behavior simplify the list items definition in the .csproj file.

The following table shows which items (file types) are processed and what the MSBuild processing do:

| | Include File types | Exclude File types |
| :--- | :---: | :---: |
| Compiled | .cs | .user, .proj, .sln, .vscc |
| Embedded resources | .res | .user, .proj, .sln, .vscc |
| None | The rest of files types ... | |

(source Microsoft)

(The folders “/bin” and “/obj” are also exclude from the MSBuild process.)

You can enable/disable the default compiled files type by setting a property in the PropertyGroup as described below.