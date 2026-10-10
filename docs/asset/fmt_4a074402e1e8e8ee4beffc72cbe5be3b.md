
```c
communicate(sfd,cfd){

char *head, *ctail, *shead, *stail;

int num, nfd, spos, cpos;

extern int errno;

fd_set rd, wr;

head = ctail = cbuf;
cpos = 0;
shead = stail = sbuf;
spos = 0;

while (1) {
    FD_ZERO(&rd);
    FD_ZERO(&wr);

    if (spos < sizeof(sbuf)-1) FD_SET(sfd, &rd);
    if (ctail > head) FD_SET(sfd, &wr);
    if (cpos < sizeof(cbuf)-1) FD_SET(cfd, &rd);
    if (stail > shead) FD_SET(cfd, &wr);

    nfd = select(256, &rd, &wr, 0, 0);
    if (nfd <= 0) continue;

    if (FD_ISSET(sfd, &rd)) {
        num=read(sfd,stail,sizeof(sbuf)-spos);
        if ((num==-1) && (errno != EWOULDBLOCK)) return;
        if (num==0) return;
        if (num>0) {
            spos += num;
            stail += num;
            if (!--nfd) continue;
        }
    }

    if (FD_ISSET(cfd, &rd)) {
        num=read(cfd,ctail,sizeof(cbuf)-cpos);
        if ((num==-1) && (errno != EWOULDBLOCK)) return;
        if (num==0) return;
        if (num>0) {
            cpos += num;
            ctail += num;
            if (!--nfd) continue;
        }
    }

    if (FD_ISSET(sfd, &wr)) {
        num=write(sfd,head,ctail-head);
        if ((num==-1) && (errno != EWOULDBLOCK)) return;
        if (num>0) {
            head += num;
            if (head == ctail) {
                head = ctail = cbuf;
                cpos = 0;
            }
            if (!--nfd) continue;
        }
    }

    if (FD_ISSET(cfd, &wr)) {
        num=write (cfd,shead,stail-shead);
        if ( (num==-1) && (errno != EWOULDBLOCK) ) return;
        if (num>0) {
            shead += num;
            if (shead == stail) {
                shead = stail = sbuf;
                spos = 0;
            }
            if (!--nfd) continue;
        }
    }
}
```

## 有状态过滤器

采用这种类型数据包过滤器的路由器和网关会迫使黑客通过隧道或用于从安全网络发起连接到其外部 Tiger Box（在第 6 部分中描述）的程序进行攻击。以下摘录展示了一个 IP 隧道攻击程序：

`fwtunnel.c`
