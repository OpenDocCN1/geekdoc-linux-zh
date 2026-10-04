```
FUNCTION rcui::AgiPassword::scalar deleting
destructor'::'1':dtor1
FUNCTION calculate_new_password_hash
FUNCTION shift_password_to_history
FUNCTION rcui::AgiPassword::GetType
FUNCTION found_password_in_history
FUNCTION 'rcui::AgiPassword::scalar deleting
destructor'::'1':dtor0
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

根据提示信息，接下来我们在调试信息里搜索关键词“password”和“locked”。通过分析后，作者发现
password_attempt_limit_exceeded()函数用关键字字符串“user was locked by subsequently failed password login attempts”。

这个函数会在日志记录“password login attempt will be rejected immediately (preventing dictionary attacks)”“failed-logon lock: expired (but not removed due to ‘read-only operation)”以及“failed-logon lock: expired => removed”。

进一步的研究表明，这个函数是登录保护密码函数。它会被密码验证函数——chckpass()函数调用。

首先要确认上述推测是否正确。使用用户开发的的tracer程序进行分析：

```
tracer64.exe -a=disp+work.exe
bpf=disp+work.exechckpass,args:3,unicode
PID=2236|TID=2248|(0) disp+work.exechckpass (0x202c770,L"Breweredl",0x41)
  \ 0x1402f1060 (disp+work.exeusrexit+0x3c0)
PID=2236|TID=2248|(0) disp+work.exechckpass -> 0x35
```

# 调用逻辑是

sysmini()->DylSigni()->dychkusr()->usrexit()->chckpass()

数字0x35是chckpass()返回的错误信息编号：