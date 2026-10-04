# Attacking and Defending Microsoft SQL Server • Chapter 12

4. Enable full auditing to monitor both successful and failed access to the SQL Server.
```
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\MSSQLServer',N'AuditLevel',
N'REG_DWORD',3
```

5. Disable SQLAgent and the Microsoft Distributed Transaction Coordinator (MSTC) since they might be abused and we cannot assume they are a requirement.
```
EXECUTE msdb..sp_set_sqlagent_properties @auto_start = 0
EXECUTE master..xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'System\CurrentControlSet\Services\MSTC', N'Start', N'REG_DWORD', 3
```

6. Disable ad hoc queries for each data provider since this functionality is ripe for abuse.
```
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\Providers\SQLOLEDB',N'DisallowAdHocAccess',N'REG_DWORD',1
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\Providers\Microsoft.Jet.Oledb.4.0',N'DisallowAdHocAccess',N'REG_DWORD',1
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\Providers\MSDAORA',N'DisallowAdHocAccess',N'REG_DWORD',1
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\Providers\ADSDSOject',N'DisallowAdHocAccess',N'REG_DWORD',1
EXECUTE master.dbo.sp_regwrite N'HKEY_LOCAL_MACHINE',\N'Software\Microsoft\MSSQLServer\Providers\DB20LEDB',N'DisallowAdHocAccess',N'REG_DWORD',1
```

![](bbox=[0.713, 0.941, 0.931, 0.966])