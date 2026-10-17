
[-l `max_lv`] [-p `max_pv`] [-s `pe_size`] [-g `pvg_name`]

`vg_name` `pv_path` ...

# `vgdisplay`(1M)

## 名称

`vgdisplay` - 显示 LVM 卷组的信息

## 摘要

```
/sbin/vgdisplay [-v] [vg_name ...]
```

# `vgexport`(1M)

## 名称

`vgexport` - 导出 LVM 卷组及其关联逻辑卷

## 摘要

```
/sbin/vgexport [-m mapfile] [-p] [-v] vg_name
/sbin/vgexport -m mapfile -s -v vg_name
```

# `vgextend`(1M)

## 名称

`vgextend` - 通过添加物理卷来扩展 LVM 卷组

## 摘要

```
/sbin/vgextend [-A backup] [-g pvg_name] [-x extensibility]
vg_name pv_path ...
```

# `vgimport`(1M)

## 名称

`vgimport` - 将 LVM 卷组导入到系统

## 摘要

```
/sbin/vgimport [-m mapfile] [-p] [-v] vg_name pv path ...
/sbin/vgimport -m mapfile -s -v vg_name
```
