
## Advanced Server 配置菜单

7. Advanced Server cluster name: `VMSOWNE`

8. Advanced Server OpenVMS cluster alias: `VMSOWNE_ALIAS`

9. Advanced Server comment: Advanced Server V7.3 for OpenVMS

10. Advanced Server language: English (USA)

11. Enable HT style printing: NO

Enter item number, or RETURN to use these values [DONE]:

Figure 7-57 This menu shows your definitions for your server and domain. You may need to change some of these for your domain and/or recognized.

7. Advanced Server computer name: `VMSONE`

7a. Advanced Server OpenVMS cluster alias: `VMSONE_ALIAS`

8. Server announce comment: Advanced server V7.3 for OpenVMS

9. Advanced server language: English (USA)

10. Enable NT type: NO

Enter item number, or RETURN to use these values [DONE]: 5

********************************************************************

You choose item number 5 from the menu. Changing the domain name will cause the existing SAM databases to be RE-INITIALIZED resulting in the loss of any data currently in these databases (for) example, user accounts (name).

********************************************************************

Do you want to continue with item number 5 (Y/N): y

The Advanced Server domain is a collection of computers that share a common database and policy. Each domain has a unique name. A network can have many domains.

The Advanced Server domain name can be up to 15 characters.

The domain name must be different than the computer name.

Enter Advanced Server domain name for this cluster [LANGGROUP]: WKSI

Figure 7-58 Change LANGGROUP to your domain or workgroup name!

The Advanced Server comment can be up to 48 characters long.

Enter server comment [no comment]: "I can say it is VMS!"

Illegal character "，请重新输入。

Enter server comment: I can say it is VMS!

Your Advanced Server for OpenVMS is presently configured to:

+ 1. Run the license server: NO

2. Enable Timeservice service: NO

3. Alert alert service: YES

4. Enable netlog service: YES

5. Advanced Server domain: LANDGROUP

6. Advanced Server role: PRIMARY

7. Advanced Server computer name: VMSONE

7a. Advanced Server OpenVMS cluster alias: VMSONE_ALIAS

8. Server announce comment: I can say it is VMS!

9. Advanced server language: English (USA)

10. Enable NT type: NO

## 第 5 ：将 OpenVMS 高级服务器配置为域控制器

![](img/a26aae01e7657faca13785a7eb03624a_148_0.png)

![](img/a26aae01e7657faca13785a7eb03624a_148_1.png)

| 日期 | 名称 | 类型 | 大小 | 时间 | 所有者 | 组 | 权限 |
|---|---|---|---|---|---|---|---|
| 20200418 | TCIPSROUTED | LEF | 6 | 00:00:00.02 | 283 | 125 | |
| 20200419 | TCIPSFTP_1 | LEF | 10 | 167 | 00:00:00.06 | 537 | 296 |
| 20200420 | TCIPHSINT_1 | NIB | 9 | 109 | 00:00:00.12 | 552 | 516 |
| 20200421 | TCIPSFWIP_1 | NIB | 10 | 246 | 00:00:00.09 | 380 | 624 |
| 20200422 | TCIPSFWIP_ACP | NIB | 10 | 72 | 00:00:00.03 | 138 | 161 |
| 20200423 | VMS_SERVER | NIB | 8 | 86 | 00:00:00.08 | 315 | 81 |
| 20200424 | REGISTRY_SERVER | NIB | 9 | 11 | 00:00:00.01 | 203 | 222 |
| 20200425 | DGTSERVER_0 | NIB | 9 | 686 | 00:00:00.13 | 833 | 938 |
| 20200426 | DTLUI | LEF | 5 | 229 | 00:00:00.09 | 463 | 372 |
| 20200427 | SYSTEM | LEF | 4 | 289 | 00:00:00.04 | 439 | 524 |
| 20200428 | DEWCSTE_0425 | NIB | 6 | 577 | 00:00:00.16 | 877 | 626 |
| 20200429 | | COM | 4 | 8967 | 00:00:01.36 | 748 | 755 |
| 20200430 | SYSTEM_248 | CUR | 7 | 6840 | 00:00:15.63 | 5919 | 1660 |
| 20200431 | | | | 46 | 59 | 00:00:00.05 | 67 | 58 |
| 20200446 | PWRKSHBIDOWN | NIB | 11 | 42 | 00:00:00.01 | 269 | 293 |
| 20200447 | PWRKADMIN_ | NIB | 12 | 83 | 00:00:00.03 | 268 | 312 |
| 20200448 | PWRKLUSER_LR | NIB | 11 | 616 | 00:00:00.03 | 4660 | 320 |
| 20200449 | PWRKMASTER | NIB | 11 | 162 | 00:00:00.04 | 363 | 94 |
| 20200450 | PWRKCOMPILER | NIB | 11 | 616 | 00:00:00.04 | 711 | 488 |
| 20200451 | PWRKSHIL_O | NIB | 5 | 51 | 00:00:00.02 | 145 | 96 |
| 20200452 | PWRKSHLRV | NIB | 7 | 778 | 00:00:00.19 | 1273 | 827 |
| 20200453 | PWRKLISHOWER | NIB | 9 | 169 | 00:00:00.05 | 762 | 521 |

图 7-6 现在使用 `$SHOW` 检查并验证
