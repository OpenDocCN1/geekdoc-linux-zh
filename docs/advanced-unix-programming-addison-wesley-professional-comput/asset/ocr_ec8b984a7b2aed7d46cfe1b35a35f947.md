```
```
                    else
                        printf("%s = l_onoff: %d; l_linger: %d secs.\n", name,
                            lng_l_onoff, lng_l_linger);
                    break;
        case OT_TIMEVAL:
            len = sizeof(tv);
            if (getsockopt(skt, level, option, &tv, &len) == -1)
                printf("%s FAILED (\n", name, strerror(errno));
            else
                printf("%s = %ld secs., %ld usecs.\n", name,
                    (long)tv.tv_sec, (long)tv.tv_usec);
        }
    }
    static void showall(int skt, const char *caption)
    {
        printf("\n%s\n", caption);
        show(skt, SOL_SOCKET, SO_ACCEPTCONN, "SO_ACCEPTCONN", OT_INT);
        show(skt, SOL_SOCKET, SO_BROADCAST, "SO_BROADCAST", OT_INT);
        show(skt, SOL_SOCKET, SO_DEBUG, "SO_DEBUG", OT_INT);
        show(skt, SOL_SOCKET, SO_DONTROUTE, "SO_DONTROUTE", OT_INT);
        show(skt, SOL_SOCKET, SO_ERROR, "SO_ERROR", OT_INT);
        show(skt, SOL_SOCKET, SO_KEEPALIVE, "SO_KEEPALIVE", OT_INT);
        show(skt, SOL_SOCKET, SO_LINGER, "SO_LINGER", OT_LINGER);
        show(skt, SOL_SOCKET, SO_OOBINLINE, "SO_OOBINLINE", OT_INT);
        show(skt, SOL_SOCKET, SO_RCVDUB, "SO_RCVDUB", OT_INT);
        show(skt, SOL_SOCKET, SO_RCVLOWAT, "SO_RCVLOWAT", OT_INT);
        show(skt, SOL_SOCKET, SO_RCVTIMEO, "SO_RCVTIMEO", OT_TIMEVAL);
        show(skt, SOL_SOCKET, SO_REUSEADDR, "SO_REUSEADDR", OT_INT);
        show(skt, SOL_SOCKET, SO_SNDBUB, "SO_SNDBUB", OT_INT);
        show(skt, SOL_SOCKET, SO_SNDBUFWAIT, "SO_SNDBUFWAIT", OT_INT);
        show(skt, SOL_SOCKET, SO_SNDTIMEO, "SO_SNDTIMEO", OT_TIMEVAL);
        show(skt, SOL_SOCKET, SO_TYPE, "SO_TYPE", OT_INT);
    }

    int main(void)
    {
        int skt;

        ec_neg1( skt = socket(AF_INET, SOCK_STREAM, 0) )
        showall(skt, "AF_INET SOCK_STREAM");
        ec_neg1( close(skt) )

        ec_neg1( skt = socket(AF_INET, SOCK_DGRAM, 0) )
        showall(skt, "AF_INET SOCK_DGRAM");
        ec_neg1( close(skt) )

        exit(EXIT_SUCCESS);
    }
EC_CLEANUP_BGN

    exit(EXIT_FAILURE);
EC_CLEANUP_END
```
```