```
break;
case 'd':
    dstport = atoi(optarg);
    break;
case 'n':
    numpacks = atoi(optarg);
    break;
case 'p':
    psize = atoi(optarg);
    break;
case 'w':
    wait = atoi(optarg);
    break;
case 'o':
    srcport = atoi(optarg);
    break;
default:
    usage(argv[0]);
    break;
}
if (!dstport)
{
    dstport = DSTPORT;
}
if (!srcport)
{
    srcport = SRCPORT;
}
if (!psize)
{
    psize = PSIZE;
}
if (!argv[optind])
{
    puts( "[*] Specify a target host, doof!" );
    exit(EXIT_FAILURE);
}

target = (char *)malloc(strlen(argv[optind]));
if (!target)
{
    puts( "[*] Agh! Out of memory!" );
    perror( "malloc" );
    exit(EXIT_FAILURE);
}
strcpy(target, argv[optind]);
}
memset(&dstaddr, 0, sizeof(struct sockaddr_in));
dstaddr.sin_family = AF_INET;
dstaddr.sin_addr.s_addr = inet_addr(target);
if (dstaddr.sin_addr.s_addr == -1)
{
    host = gethostbyname(target);
    if (host == NULL)
```