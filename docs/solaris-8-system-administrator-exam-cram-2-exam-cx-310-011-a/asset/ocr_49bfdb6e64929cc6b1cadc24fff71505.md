# Question 7

Match each command with its operation:

| Command | Operation |
|---|---|
| a. `cachefswssize` | 1. Displays the cache file system statistics |
| b. `cachefslog -h` | 2. Displays the cache status |
| c. `cachefslog -f` | 3. Displays the cache working set size |
| d. `cachefsstat` | 4. Starts cache logging |
| e. `cfsadmin -l` | 5. Stops cache logging |

Answers a-3, b-5, c-4, d-1, and e-2 are correct. The **cachefswssize** command displays the size of the cache working set. For the **cachefslog** command, **-h** stops logging and **-f** starts logging. The **cachefsstat** command displays statistics relating to the cache contents, and **cfsadmin -l** displays the status of the cache itself.

# Question 8

+   Which of the following commands can be used to determine any mounted NFS resources? (Select all that apply.)
+   
+   - [ ] a. `share`
+   - [ ] b. `dfmounts`
+   - [ ] c. `nfsmounts`
+   - [ ] d. `mountall`
+   - [ ] e. `mount`

Answers b and e are correct. You can use the **dfmounts** and **mount** commands to determine any mounted NFS resources. **share** is used to share NFS resources. Therefore, answer a is incorrect. **nfsmounts** does not exist. Therefore, answer c is incorrect. **mountall** is used to mount resources, not to list NFS resources. Therefore, answer d is incorrect.

# Question 9

+   When using NFS, which of the following results are true? (Select all that apply.)
+   
+   - [ ] a. Introduces redundancy
+   - [ ] b. Improves consistency
+   - [ ] c. Reduces administration
+   - [ ] d. Reduces network traffic