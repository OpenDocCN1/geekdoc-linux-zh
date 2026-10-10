```
else
p.src = 0;

/* packet size redundant if not using echo port */
if (argc >= 8)
p.ps = atoi(argv[7]);
else
p.ps = 1;
/* other variables */
num = atoi(argv[3]);
delay = atoi(argv[4]);
/* resolve host */
if (isdigit(*argv[1]))
sin.sin_addr.s_addr = inet_addr(argv[1]);
else
{
if ((he = gethostbyname(argv[1])) == NULL)
{
fprintf(stderr, "Can't resolve hostname!\n\n");
exit(-1);
}
memcpy( (caddr_t) &sin.sin_addr, he->h_addr, he->h_length);
}
sin.sin_family = AF_INET;
sin.sin_port = htons(0);
/* open bcast file and build array */
if ((bfile = fopen(argv[2], "r")) == NULL)
{
perror("Opening broadcast file");
exit(-1);
}
n = 0;
while (fgets(buf, sizeof buf, bfile) != NULL)
{
buf[strlen(buf) - 1] = 0;
if (buf[0] == '#' || buf[0] == '\n' || !isdigit(buf[0]))
continue;

bcast[n] = malloc(strlen(buf) + 1);
strcpy(bcast[n], buf);
n++;
}
bcast[n] = '\0';
fclose(bfile);

/* check for addresses */
if (!n)
{
fprintf(stderr, "Error: No valid addresses in file!\n\n");
exit(-1);
}
/* create our raw socket */
if ((s = socket(AF_INET, SOCK_RAW, IPPROTO_RAW)) <= 0)
```