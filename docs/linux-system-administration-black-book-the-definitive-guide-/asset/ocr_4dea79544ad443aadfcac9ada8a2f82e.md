**Table 18.6 Popular options used in individual Samba share definitions (continued).**

| Option | Purpose | Value(s) | Example |
| :--- | :--- | :--- | :--- |
| **preserve case** | Sets whether to leave file name cases as is or convert them to the **default** case. | **yes or no** | **preserve case = no** |
| **read list** | Sets a list of users who have read-only access to this share, even if everyone else has write access. | Comma-separated list of users, or groups in the **@group** format | **read list = bob sue @temps** |
| **short preserve case** | Sets whether files in the ABCDEFGH.ZYX format stay in their original case or are altered to the **default case**. | **yes or no** | **short preserve case = yes** |
| **valid users** | Sets which users are allowed to access this share. | Comma-separated list of users, or groups in the **@group** format | **valid users = @project, supervisor, @staff** |
| **write list** | Sets a list of users who have write access to this share, even if everyone else has only read access. | Comma-separated list of users, or groups in the **@group** format | **write list = admin @project** |
| **writable** | Sets whether clients can write data to this share. | **yes or no** | **writable = yes** |

+   9. After you examine the list, complete your share definition. For example, perhaps you want only the ProjectP staff to be able to write to the share you are creating, but want other project staff to be able to read it. The final share definition might look like this:

```
```
[ProjectP]
  comment = Documents needed by ProjectP staff
  path = /Projects/P/
  writable = no
  write list = @projectp
  valid users = @project
```
```



![](bbox=[0.9, 0.77, 0.99, 0.94])