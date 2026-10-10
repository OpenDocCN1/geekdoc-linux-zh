# Persisting Grid Settings

Users expect customizations to be persistent across program invocations, and grid settings are no exception. When your users resize or reorder the columns in a grid, they usually expect the column order and size to be the same the next time they run the application.

It isn't difficult to persist grid column settings. There are two approaches that you can take:

+   - Save the settings to a stream or to a separate file.
+   - Save the settings to the Windows registry or to an ini file.

The first option is simpler, so I'll cover it first. TDBGrid's Columns property provides SaveToFile and SaveToStream methods that you can use to save column configurations, to either a file or a stream, with a minimum of fuss. The following code snippet shows how you can save column settings to a file:

```
TDBGrid.Columns.SaveToFile( 'GRID.CFG' );
```

Similarly, to reload the settings:

```
TDBGrid.Columns.LoadFromFile( 'GRID.CFG' );
```

The drawback to this approach is that if you have many different grids in your application, you need separate configuration files to persist each one. If that is the case, you might want to look at SaveToStream instead of SaveToFile. With a little effort, you can use SaveToStream to save a grid's column configuration to an ini file or to the Windows registry. The following procedure saves column information to an ini file:

```
procedure SaveColumnConfiguration(const FileName: string; Grid: TDBGrid;
  const SectionName: string; const Name: string);
var
  ini: TIniFile;
  MemStream: TMemoryStream;
begin
  MemStream := TMemoryStream.Create;
  try
    Grid.Columns.SaveToStream(MemStream);
    MemStream.Seek(0, soFromBeginning);

    ini := TIniFile.Create(FileName);
    try
      ini.WriteBinaryStream(SectionName, Name, MemStream);
    finally
      ini.Free;
    end;
  finally
    MemStream.Free;
  end;
```