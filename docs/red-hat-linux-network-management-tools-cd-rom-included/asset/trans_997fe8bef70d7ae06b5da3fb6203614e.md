
**对象名称：** dot3ErrorInitError
**OID：** dot3Errors.1
**对象类型：** Counter
**访问模式：** read-only
**描述：** 标识与芯片组测试失败相关的错误

**对象名称：** dot3StateIndex
**OID：** dot3StateEntry.1
**对象类型：** Counter
**访问模式：** read-only
**描述：** 与运行回环测试相关的错误

## SNMP 组

SNMP 组包含与 SNMP 的操作和实现相关的信息。该组中的某些对象与 SNMP 站管理或代理功能相关。因此，每个 SNMP 实现都可能使用表中的特定对象。代理不支持的那些对象包含零值。

除 snmpEnableAuthenTraps 对象为读写外，所有其他对象均为只读。此对象控制代理是否被允许生成认证失败陷阱，通常由网络管理应用程序设置。认证失败是管理实体尝试在代理上执行某些特权功能，但没有正确的安全权限或凭据来执行该操作的结果。图 6.16 显示了 snmp 表的树视图。

请注意，位置 7 和 8 均未列出，因为 MIB 未为这些槽位定义任何对象。如图 6.16 所示，许多 SNMP 对象以灰色列出，而少数以黑色列出。这是因为该表的原始版本包含所有灰色对象以及其他一些对象。当 SNMPv2 规范发布时，许多对象被废弃。然而，由于许多代理继续支持 SNMPv1，这些对象仍在使用中。这是较新的 MIB 规范对过去实现影响甚微的一个例子。较旧的 snmp 组对象将长期伴随我们。snmp 表包含以下对象：

![](img/f265c9d1f2610aca197c430cbfcd51f5_346_0.png)

图 6.16 SNMP 组视图。

**对象名称：** snmpInPkts
**OID：** snmp.1
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的 SNMP 消息数量

**对象名称：** snmpOutPkts **(已废弃)**
**OID：** snmp.2
**对象类型：** Counter
**访问模式：** read-only
**描述：** 从代理传递到传输层的 SNMP 消息数量

**对象名称：** snmpInBadVersions
**OID：** snmp.3
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的不受支持的 SNMP 消息数量

**对象名称：** snmpInBadCommunityNames
**OID：** snmp.4
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的包含未知团体名称的 SNMP 消息数量

**对象名称：** snmpInBadCommunityUses
**OID：** snmp.5
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的包含所提供 SNMP 团体名称不允许的 SNMP 操作的消息数量

**对象名称：** snmpInASNParseErrs
**OID：** snmp.6
**对象类型：** Counter
**访问模式：** read-only
**描述：** 解码传入 SNMP 消息时遇到的 BER 和 ASN 错误数量

**对象名称：** snmpInTooBig (已废弃)
**OID：** snmp.8
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的发生 tooBig 错误的 SNMP PDU 数量

**对象名称：** snmpInNoSuchName (已废弃)
**OID：** snmp.9
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的发生 noSuchName 错误的 SNMP PDU 数量

**对象名称：** snmpInBadValues (已废弃)
**OID：** snmp.10
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的发生 badValue 错误的 SNMP PDU 数量

**对象名称：** snmpInReadOnlys (已废弃)
**OID：** snmp.11
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的发生 readOnly 错误的 SNMP PDU 数量

**对象名称：** snmpInGenErrs (已废弃)
**OID：** snmp.12
**对象类型：** Counter
**访问模式：** read-only
**描述：** 传递给代理的发生 genErr 错误的 SNMP PDU 数量

**对象名称：** snmpInTotalReqVars (已废弃)
**OID：** snmp.13
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理因有效的 SNMP get-request 和 getnext-request 而成功检索的 MIB 对象数量

**对象名称：** snmpInTotalSetVars (已废弃)
**OID：** snmp.14
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理因有效的 SNMP set-request 而成功修改的 MIB 对象数量

**对象名称：** snmpInGetRequests (已废弃)
**OID：** snmp.15
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理接受并处理的 SNMP get-request 数量

**对象名称：** snmpInGetNexts (已废弃)
**OID：** snmp.16
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理接受并处理的 SNMP getnext-request 数量

**对象名称：** snmpInSetRequests
**OID：** snmp.17
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理接受并处理的 SNMP set-request 数量

**对象名称：** snmpInGetResponses (已废弃)
**OID：** snmp.18
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理接受并处理的 SNMP get-response 数量

**对象名称：** snmpInTraps (已废弃)
**OID：** snmp.19
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理接受并处理的 SNMP trap 数量

**对象名称：** snmpOutTooBig
**OID：** snmp.20
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的发生 tooBig 错误的 SNMP PDU 数量

**对象名称：** snmpOutNoSuchNames (已废弃)
**OID：** snmp.21
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的发生 noSuchName 错误的 SNMP PDU 数量

**对象名称：** snmpOutBadValues **(已废弃)**
**OID：** snmp.22
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的发生 `badValue` 错误的 SNMP PDU 数量

**对象名称：** snmpOutGenErrs **(已废弃)**
**OID：** snmp.24
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的发生 `genErr` 错误的 SNMP PDU 数量

**对象名称：** snmpOutGetRequests **(已废弃)**
**OID：** snmp.25
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的 SNMP `get-request` PDU 数量

**对象名称：** snmpOutGetNexts **(已废弃)**
**OID：** snmp.26
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的 SNMP `getNext-request` PDU 数量

**对象名称：** snmpOutSetRequests **(已废弃)**
**OID：** snmp.27
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的 SNMP set-request PDU 数量

**对象名称：** snmpOutGetResponses **(已废弃)**
**OID：** snmp.28
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的 SNMP get-response PDU 数量

**对象名称：** snmpOutTraps **(已废弃)**
**OID：** snmp.29
**对象类型：** Counter
**访问模式：** read-only
**描述：** 代理生成的 SNMP trap 数量

**对象名称：** snmpEnableAuthenTraps
**OID：** snmp.30
**对象类型：** Integer
**访问模式：** read-write
**描述：** 是否应生成认证失败陷阱。有效值为 `enabled(1)` 或 `disabled(2)`。当 SNMP 实体尝试使用无效的团体字符串或认证令牌查询代理时，如果已启用，代理将发出 SNMP 陷阱
