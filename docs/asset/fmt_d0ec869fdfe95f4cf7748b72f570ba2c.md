
## 第 21 章

系统的未来扩展可能包括使用 Python 的 `shelf` 或 `pickle` 类，它们提供了更复杂的数据结构序列化方法，或者最终让 DVD 服务器与 PostgreSQL 服务器通信。

让我们通过为错误消息表建立关联数组并运行 `maxforall` 函数来建立记录创建计数器，以完成非 CORBA 组件的设置：

```python
disk=DVD.DISKS.dvddis(sdisk)

(st, did)=string.split(sdisk, "\n")

disk.diskid=string.atoi(st)

disk.titleid=string.atoi(did)

return disk
```

```python
def destringizedisk(disk):
    return.string.join("%s%%disk.titleid, %s%%disk.title, "\n")
```

```python
def destringizetitle(title):
    return.string.join("%s%%title, %s%%title.titletext, %s%%title.asin,
    title.director,title.genre,title.classification,title.actor1,ti-actor2,
    title.released,title.titlecost,title.image), "\n")=string.split(stile, "\n")
    title.titleid=string.atoi(mti)
    return title
```

```python
def destringizember(member):
    return.string.join("%s%%member.memberid, %s%%member.memberno,
    member.title,member.fname,member.lname,
    member.houselafref,member.address),
    member.address2,member.town,member.state,
    member.phone,member.zipcode, "\n")
```

```python
def destringizember(smember):
    member=DVD.MEMBERSHIP.storemembers(smember)
    (mid,member.memberno,member.title,member.fname,member.lname,
    member.houselafref,member.address,member.address2,
    member.town,member.state,member.phone,member.zipcode)=string.split(smember, "\n")
    member.memberid=string.atoi(mid)
    return member
```

*** 初始化非 ORB 相关内容...*

```python
FACTORYOBJECT = {}
DBMAX = {}
ERRNDICT = {
  0: "DVD_SUCCESS",
  -1: "DVD_ERR_NO_FILE",
  -2: "DVD_ERR_BAD_TABLE",
  -3: "DVD_ERR_NO_MEMBER_TABLE",
  -4: "DVD_ERR_BAD_MEMBER",
  -5: "DVD_ERR_BAD_TITLE",
  -6: "DVD_ERR_BAD_DISK_TABLE",
  -7: "DVD_ERR_BAD_SEEK",
  -8: "DVD_ERR_NULL_POINTER",
  -9: "DVD_ERR_BAD_WRITE",
  -10: "DVD_ERR_BAD_READ",
  -11: "DVD_ERR_NO_FOUND",
  -12: "DVD_ERR_NO_MEMORY",
  -13: "DVD_ERR_BAD_RENTAL_TABLE",
  -14: "DVD_ERR_BAD_RESERVE_TABLE" }
```

```python
ERRMSGODICT = {
  "DVD_SUCCESS": "no error",
  "DVD_ERR_NO_FILE": "cannot open file",
  "DVD_ERR_BAD_TABLE": "corrupt table file",
  "DVD_ERR_NO_MEMBER_TABLE": "no member table",
  "DVD_ERR_BAD_MEMBER_TABLE": "corrupt member table",
  "DVD_ERR_BAD_TITLE": "corrupt title table",
  "DVD_ERR_BAD_DISK_TABLE": "corrupt disk table",
  "DVD_ERR_BAD_RENTAL_TABLE": "corrupt rental table",
  "DVD_ERR_BAD_RESERVE_TABLE": "corrupt reserve table",
  "DVD_ERR_BAD_SEEK": "cannot seek in file",
  "DVD_ERR_NULL_POINTER": "null data pointer",
  "DVD_ERR_BAD_WRITE": "cannot write to file",
  "DVD_ERR_BAD_READ": "cannot read file",
  "DVD_ERR_NO_FOUND": "no match found",
  "DVD_ERR_NO_MEMORY": "out of memory" }
```

```python
SETUP-SetupCounters()
SETUP-maxforall()
```

Python 类 `Factory` 提供了初始化并为客户端提供 DVD 接口对象引用的函数：

```python
class Factory:
  def generateFactory(self, name, instance):
    new_instance = instance
    poa.activate_object(new_instance)
    FACTORYOBJECT[name] = poa.servant_to_reference(new_instance)
    return FACTORYOBJECT[name]
```

```python
def DISKSFactory(self):
    if FACTORYOBJECT.has_key("disks"):
        return FACTORYOBJECT["disks"]
    else:
        logit("Factory", "Create Disks Interface")
        return self.generateFactory("disks", POA.DVD.DISKS(Disks()))
```

```python
def UTILITIESFactory(self):
    if FACTORYOBJECT.has_key("utilities"):
        return FACTORYOBJECT["utilities"]
    else:
        logit("Factory", "Create utilities interface")
        return self.generateFactory("utilities", POA.DVD.UTILITIES(Utilities()))
```

```python
def MEMBERSHIPFactory(self):
    if FACTORYOBJECT.has_key("membership"):
        return FACTORYOBJECT["membership"]
    else:
        logit("Factory", "Create membership interface")
        return self.generateFactory("membership", POA.DVD.MEMBERSHIP(Membership()))
```

```python
def TITLINGFactory(self):
    if FACTORYOBJECT.has_key("titling"):
        return FACTORYOBJECT["titling"]
    else:
```
