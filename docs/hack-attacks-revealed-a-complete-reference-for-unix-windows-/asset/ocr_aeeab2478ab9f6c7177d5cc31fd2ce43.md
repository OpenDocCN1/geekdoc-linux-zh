```
printf("Frag'd Pcnt\t= %.0f%%\t\t", FragPct);
printf("Bad ICMP Cksm\t= %.0f%%\n", ICMPCKsm);
printf("\n\n");

/* Drop them down to floats so we can multiply and not overflow */
BadIPVer  /= 100;
FragPct   /= 100;
IPOpts    /= 100;
ICMPCKsm  /= 100;

/**** **** **** **** **** ***
* Main Loop *
**** **** **** **** **** ***/
gettimeofday(&tv, NULL);
gettimeofday(&starttime, NULL);

for(acx = 0; acx < num_to_send; acx++) {
packet_len = IP_H + 4;

tos = rand() & 0xff;
id  = acx & 0xffff;
ttl = rand() & 0xff;

if ( rand() <= (RAND_MAX * FragPct) )
    frag_off = rand() & 0xffff;
else frag_off = 0;

/* We're not going to pad IP Options */
if ( rand() <= (RAND_MAX * IPOpts) ) {
  ipopt_len = 10 * (rand() / (float) RAND_MAX);
  ipopt_len = ipopt_len << 1;
  ip_opts = (u_short *) (buf + IP_H);
  packet_len += ipopt_len << 1;

  for ( cx = 0; cx < ipopt_len; cx++ )
    ip_opts[cx] = rand() & 0xffff;
  icmp = (struct icmp *)(buf + IP_H +(ipopt_len << 1));
  ipopt_len = ipopt_len >> 1;
  } else {
  ipopt_len = 0;
  icmp = (struct icmp *) (buf + IP_H);
  }

if ( src_ip_rand == 1 )
  src_ip = ((rand() & 0xffff) << 15) + (rand() & 0xffff);
if ( dst_ip_rand == 1 )
  dst_ip = ((rand() & 0xffff) << 15) + (rand() & 0xffff);

if ( rand() <= (RAND_MAX * BadIPVer ) )
  ver = rand() & 0xf;
else ver = 4;

payload_s = rand() & 0x4ff;           /* length of 1279 */
packet_len += payload_s;
```