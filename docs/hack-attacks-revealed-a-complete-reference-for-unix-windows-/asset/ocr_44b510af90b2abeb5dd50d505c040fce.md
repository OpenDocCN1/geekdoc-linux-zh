```
FragPct = atof(optarg);
break;
case 'I':
IPopts = atof(optarg);
break;
case 'i':
ICMPCksm = atof(optarg);
break;
case 'x':
repeat = atoi(optarg);
break;
case 'v':
printf("Version %s\n", VERSION);

exit(0);
}
}

if ( !src_ip || !dst_ip ) {
usage(argv[0]);
exit(EXIT_FAILURE);
}

printf("Compiled against Libnet %s\n", LIBNET_VERSION);
printf("Installing Signal Handlers.\n");
if ( signal(SIGTERM, &sighandler) == SIG_ERR )
printf("Failed to install signal handler for SIGTERM\n");
if ( signal(SIGINT, &sighandler) == SIG_ERR )
printf("Failed to install signal handler for SIGINT\n");
if ( signal(SIGQUIT, &sighandler) == SIG_ERR )
printf("Failed to install signal handler for SIGQUIT\n");

printf("Seeding with %i\n", seed);
srand(seed);
max_pushed *= 1024;

if ( (buf = malloc(IP_MAXPACKET)) == NULL ) {
peror("Malloc: ");
exit( -1 );
}

if ( (sock = libnet_open_raw_sock(IPPROTO_RAW)) == -1 ) {
peror("Socket: ");
exit(EXIT_FAILURE);
}

if ( max_pushed >= 10000000 )
printf("No Maximum traffic limiter\n");
else printf("Maximum traffic rate = %.2f k/s\n", max_pushed/1024.0
);

printf("Bad IP Version\t= %.0f%%\t\t", BadIPVer);
printf("IP Opts Pcnt\t= %.0f%%\n", IPopts);
```