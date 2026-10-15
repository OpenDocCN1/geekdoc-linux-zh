
`.text:6440FB4 mov [esi+24h], eax`

`.text:6440FBC mov [esi+24h], 00000`

`.text:6440FCE cmp [ebp+compression], esi`

`.text:6440FCD4 mov eax, [edi+10h]`

`.text:6440FCD6 jz short set_EAX_to_0`

`.text:6440FCD7 mov al, [edi+14h]`

`.text:6440FCD9 mov [esi+14h], al`

`.text:6440FCE mov al, [edi+15h]`

`.text:6440FD00 mov [esi+15h], al`

`.text:6440FD04 call`

`.text:6440FD05 push [ebp+compression]`

`.text:6440FD06 push [ebp+arg_C]`

`.text:6440FD0C push [ebp+arg_8]`

`.text:6440FD0F push [ebp+arg_4]`

`.text:6440FD12 push [ebp+arg_0]`

`.text:6440FD15 call CNetwork::CNet`

```
Flags: d0

PARAMETER serverName

Address: Reg335+304 Size: 8 bytes Index: 60492

TypeIndex: 60493

Type: unsigned short*

Flags: d0

STATIC LOCAL_VAR func

Address: 12274af0 Size: 8 bytes Index: 60495

TypeIndex: 60496

Type: wchar_*

Flags: 80

LOCAL VAR admhead

Address: Reg335+304 Size: 8 bytes Index: 60498

TypeIndex: 60499

Type: unsigned char*

Flags: 90

LOCAL VAR record

Address: Reg335+64 Size: 204 bytes Index: 60501

TypeIndex: 60502

Type: AD_RECORD

Flags: 90

LOCAL VAR adlen

Address: Reg335+296 Size: 4 bytes Index: 60508

TypeIndex: 60509

Type: int

Flags: 90
```

不仅如此，它解释了结构体的相关信息：

```
STRUCT DBSL STMT

Size: 120 Variables: 4 Functions: 0 Base classes: 0

MEMBER moduletype

Type: DBSL MODULETYPE

Offset: 0 Index: 3 TypeIndex: 38653

MEMBER module

Type: wchar_t module[40]

Offset: 4 Index: 3 TypeIndex: 831

MEMBER stmtnum

Type: long

Offset: 84 Index: 3 TypeIndex: 440

MEMBER timestamp

Type: wchar_t timestamp[15]

Offset: 88 Index: 3 TypeIndex: 6612
```

此外，调试调用（debugging calls）也可提供大量信息。

不久，笔者注意到设置日志详细程度的全局变量 `ct_level`。SAP官方对这个变量有详细的解释：http://help.sap.com/nwpi71/helpdata/en/46/962416a5a6313e8e10000000a155369/content.htm

`disp+work.exe` 文件保留了大量的调试信息：

```
cmp      cs:ct_level, 1

jl       short loc_1400375DA

call     DpLock

lea      rcx, aDpxtool4_c ; "dpxtool4.c"

mov      edx, 4Eh                ; line

call     CTrcSaveLocation

mov      r8, cs:func_48

mov      rcx, cs:hdl             ; hdl

lea      aSDpreadmemvalue ; "%s: DpreadMemValue(%d)"

mov      r9d, ebx

call     DptrErr

call     DpUnlock
```

如果 `ct_level` 的值大于等于程序预设的某个阈值，那么程序将会将对应的细节记录到 `dev_wo,disp_dev` 日志文件。

在使用 `TYPEINFO` 程序将 `PDF` 转换为文本文件之后，我们使用 `grep` 指令搜索与密码相关的函数名称：

```bash
cat "disp.work.db" | grep FUNCTION | grep -i password
```

上述指令的结果如下：

```
FUNCTION rcui::AgiPassword::DiagISelection

FUNCTION ssf_password_encrypt

FUNCTION ssf_password_decrypt

FUNCTION password_logon_disabled

FUNCTION dySignSkipUserPassword

FUNCTION migrate_password_history

FUNCTION password_is_initial

FUNCTION rcui::AgiPassword::IsVisible

FUNCTION password_distance_ok

FUNCTION get_password_downwards_compatibility

FUNCTION dySignSkipUserPassword

FUNCTION rcui::AgiPassword::GetTypeName

FUNCTION 'rcui::AgiPassword::AgiPassword::'1':dtor2

FUNCTION 'rcui::AgiPassword::AgiPassword::'1':dtor0

FUNCTION 'rcui::AgiPassword::AgiPassword::'1':dtor1

FUNCTION usm_set_password

FUNCTION rcui::AgiPassword::TraceTo

FUNCTION days_since_last_password_change

FUNCTION rsecgrp_generate_random_password

FUNCTION rcui::AgiPassword::scalar deleting destructor'

FUNCTION password_attempt_limit_exceeded

FUNCTION handle_incorrect_password

FUNCTION rcui::AgiPassword::scalar deleting destructor'::'1':dtor1

FUNCTION calculate_new_password_hash

FUNCTION shift_password_to_history

FUNCTION rcui::AgiPassword::GetType

FUNCTION found_password_in_history

FUNCTION 'rcui::AgiPassword::scalar deleting destructor'::'1':dtor0

FUNCTION rcui::AgiObj::IsaPassword

FUNCTION password_idle_check

FUNCTION SlichWab_passwordForDay

FUNCTION rcui::AgiPassword::IsaPassword

FUNCTION rcui::AgiPassword::AgiPassword

FUNCTION delete_user_password

FUNCTION usm_set_user_password

FUNCTION Password_API

FUNCTION get_password_change_for_SSO

FUNCTION password_in_USR40

FUNCTION rsec_agrp_abab_generate_random_password
```
