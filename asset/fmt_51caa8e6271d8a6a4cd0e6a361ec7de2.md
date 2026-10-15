
```c
struct statestr {
  int num;
  char *name;

const state[] = {
    {TCP_ESTABLISHED
    {"snmp", 161, UDPIDX},
    {"route", 520, UDPIDX},
    {"socks", 1080, TCPIDX},

    {"mount", 635, UDPIDX},
    {"nfs", 2049, TCPIDX},
    {"nfs", 2049, UDPIDX},

    {"http", 80, TCPIDX},
    {"https", 443, TCPIDX},

    {"dtk", 365, TCPIDX},
    {"dtku", 365, UDPIDX},

    {"snews", 563, TCPIDX},
    {"ingresslock", 1524, TCPIDX},

    {"squid", 3128, TCPIDX},

    {"smbd", 1048, UDPIDX},
    {"netbios1", 137, TCPIDX},
    {"netbios2", 138, TCPIDX},
    {"netbios3", 139, TCPIDX},

    {"wrapt", 421, TCPIDX},    /* 木马程序 */

    {"subven", 1243, TCPIDX},
    {"subven", 1234, TCPIDX},
    {"subven", 2734, TCPIDX},
    {"dephrat", 2140, UDPIDX},

    {"socdi", 3137, TCPIDX},
    {"backorice", 3137, UDPIDX},
    {"mstream_1", 6838, UDPIDX},
    {"mstream_2", 9325, UDPIDX},
    {"mstream_z1", 1049, UDPIDX},
    {"mstream_z2", 7983, UDPIDX},
    {"portxd", 2400, TCPIDX},
    {"shmd2", 7890, TCPIDX},
    {"trino", 2744, UDPIDX},
    {"windowstoo", 3455, UDPIDX},
    {"windowstocl", 3555, UDPIDX},
    {"barwire1", 1660, TCPIDX},
    {"barwire1", 1660, UDPIDX},
    {"barwire2", 6001, TCPIDX},
    {"barwire2", 6001, UDPIDX},
    {"barwire_agent", 6500, TCPIDX},
    {"barwire_agent", 6500, UDPIDX};
/* 某些已知端口：添加自己的。 */
int badports[] = {
  421,
  1234,
  1243,
  1524,
  2140,
  2400,
  6838,
  7890,
  7983,
  9325,
  1049,
  1666,
  2734,
  2744,
  3137,
  3455,
  3555,
  6001,
  6500
};

int main(int argc, char **argv) {
  char *s;
  char *t;
  int i;
  int j;
  FILE *fp;
  static int ret;
  struct hostent *hostptr;
  const char *alert;

  argc--;
  argv++;

  /* 确保文件一致。 */
  if (sizeof(file)/sizeof(*file) != sizeof(proto)/sizeof(*proto) ||
      sizeof(proto)/sizeof(*proto) != sizeof(protol)/sizeof(*protol))
    fprintf(stderr, "bug\n"), exit(1);

  /* 处理每个文件。 */
  for (i=0; i<sizeof(file)/sizeof(*file); i++) {
    fp = fopen(file[i], "r");
    if (!fp)
      perror(file[i]), exit(2);

    /* 跳过第一行（头部）。 */
    if (!fgets(line, LINEMAX, fp) || !strchr(line, '\n'))
      printf(stderr, "syntax error\n"), exit(3);

    if (i)
      putchar('\n');
    printf("%s\n", proto[i]);
    /* 将 printf '.' 替换为 ' ' */
    printf("...Lcl port.......Rmt port....Status\n"
           "....Rmt IP........Rmt host...\n");
    /* 处理数据的每一行。 */
    for (;;) {
      if (!fgets(line, LINEMAX, fp))
        break;
      s = strchr(line, '\n');
      if (!s) {
        printf(stderr, "%s: line too long\n", file[i]);
        if (!ret)
          ret = 3 + i;
      }
      /* 去除末部空格。 */
      while (s > line && s[-1] == ' ')
        s--;

      s = 0;
      /* 截断字符串。 */
      alert = 0;
      /* 初始化. 警示标记。 */

      s = strchr(line, ':');
      for (j=0; j<5; j++) {
        if (!s) {
          printf(stderr, "%s: Syntax error\n", proto[i]);
          exit(5 + i);
        }
      }

      /* 跳过冒号和空格。 */
      while (*s == ' ' || *s == ':')
        s++;
      data[j] = strtol(s, &t, 16);
      if (!t || !*t)
        goto synerr;
      s = t;
    }

    /* 找到枚举（最后一个字段）。 */
    s = strchr(s, ' ');
    if (!s)
      goto synerr;
    while (*s == ' ')
      s++;
    data[D_INUM] = atoi(s);

    /* 标记疑点。 */
    alert = look(i);
    if (alert)
      putchar('*');
    else
      putchar(' ');

    /* 本地 远程，状态。 */
    putport(data[D_LPORT], i);
    putport(data[D_RPORT], i);
    printf("%0X\n", data[D_STATE]);

    for (j=0; j<sizeof(state)/sizeof(*state); j++) {
      if (state[j].num == data[D_STATE]) {
        printf("%-10s", state[j].name);
        break;
      }
    }

    /* 远程 IP。 */
    aconv.i = data[D_RADDR];
    s = inet_ntoa(aconv.str);
    if (data[D_RADDR]) {
      hostptr = gethostbyaddr((char *)data[D_RADDR], AF_INET);
      if (hostptr)
        t = hostptr->h_name;
      else
        t = "IP?";
    } else {
      t = "local";
    }
    printf("%15s %s\n", s, t);
    if (alert) {
      printf("%s\n", alert);
      alerts++;
    }
    close(fp);
  }

  if (alerts) {
    printf("%nd alerts: possible breach\n", alerts);
    exit(-1);
  }

  exit(0);
}

/* 打印端口号和服务名。 */
void
putport(int port, int idx) {
  struct servant *srv;
  const char *s = 0;
  int i;
  /*
   * 优先使用内部名称
   * 即使 /etc/services 被修改过。
   */
  for (i=0; i<sizeof(ports)/sizeof(*ports); i++) {
    if (ports[i].num == port
      && ports[i].idx == idx) {
      s = ports[i].name;
      break;
    }
  }
  if (!s) {
    setenv(1);
    srv = getservbyport(htons(port), protol[idx]);
    if (srv) {
      s = srv->s_name;
    }
  }
  if (!s) {
    s = "?";
  }
  printf("%d=%7s ", port, s);
}
```
