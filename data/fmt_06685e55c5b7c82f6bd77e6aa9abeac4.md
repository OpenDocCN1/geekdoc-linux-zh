
```xml
<volume_trustees>

  <inherited_rights_mask path="/.trustee_work.dat">

    <rights>S</rights>

  </inherited_rights_mask>

  <inherited_rights_mask path="/.trustee_database.xml">

    <rights>S</rights>

  </inherited_rights_mask>

</volume_trustees>
```

在进行几次受托分配后，`.trustee_database.xml` 文件看起来如下所示：

# 图 5-10

```xml
<volume_trustees>

  <trustee path="RLajoie">

    <name>RLajoie.IS.SLC.Da</name>

    <rights>RWNCEM</rights>

  </trustee>

  <trustee path="Keeetch">

    <name>Keeetch.IS.Da</name>

    <rights>RWNCEM</rights>

  </trustee>

  <inherited_rights_mask path="/.trustee_work.dat">

    <rights>S</rights>

  </inherited_rights_mask>

  <inherited_rights_mask path="/.trustee_database.xml">

    <rights>S</rights>

  </inherited_rights_mask>

</volume_trustees>
```
