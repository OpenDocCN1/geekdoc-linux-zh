# 6.5.2 Configuration data

As it currently stands, anti-theft motes lose their settings when they are switched off. We can fix this by storing the settings in a small configuration volume:

```
```text
<volume_table>
  <volume name="AT_SETTINGS" size="512"/>
</volume_table>

configuration AntiTheftAppC {
  implementation {
    ...
    components new ConfigStorageC(VOLUME_AT_SETTINGS) as AtSettings;
    MovingC.Mount -> AtSettings;
    MovingC.ConfigStorage -> AtSettings;
  }
}
```
```

Configuration volumes must be mounted before use, using the split-phase Mount interface:

```
```c
interface Mount {
  command error_t mount();
  event void mountDone(error_t error);
}
```
```

![](bbox=[0.358, 0.535, 0.651, 0.548])

Once mounted, the volume is accessed using the ConfigStorage interface:

```
```c
interface ConfigStorage {
  command error_t read(storage_addr_t addr, void* buf, storage_len_t len);
  event void readDone(storage_addr_t addr, void* buf, storage_len_t len,
                      error_t error);

  command error_t write(storage_addr_t addr, void* buf, storage_len_t len);
  event void writeDone(storage_addr_t addr, void* buf, storage_len_t len,
                       error_t error);
  command error_t commit();
  event void commitDone(error_t error);

  command storage_len_t getSize();
  command bool valid();
}
```
```

![](bbox=[0.357, 0.869, 0.653, 0.882])

ConfigStorage volumes are somewhat unusual in that they effectively keep two copies of their contents: the contents as of the last commit and the new, as-yet-to-be-committed