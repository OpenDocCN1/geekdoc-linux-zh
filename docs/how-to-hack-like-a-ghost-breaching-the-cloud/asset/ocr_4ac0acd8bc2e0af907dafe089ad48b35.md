Jackpot! The blob has yielded many passwords to access Cassandra clusters (Cassandra is a highly resilient NoSQL database usually deployed to handle large-scale data with minimal latency). We also get two obscure passwords holding untold promise. Of course, passwords alone are not enough. We need the associated host machines and usernames, but so does the application, so we can assume the second environment file from Listing 5-4, env.file, should contain all the missing pieces.

Scrolling further down user-data, however, we find no definition of env.file. But we do come across a shell script, get-region-params.sh, that seems to reset our precious env.file (see Listing 5-6).

```
--snip--
- command: start
  content: |-
    [Unit]
    Description=Discover IPs for external services
    [Service]
    Type=oneshot
    ExecStartPre=/usr/bin/rm -f /etc/env.file
    ExecStart=/conf_files/get-region-params.sh
  name: define-region-params.service
--snip--
```

Listing 5-6: A discovery service that seems to interact with env.file

It seems likely this script will create env.file. Let’s dive into the content of get-region-params.sh, created three lines below (see Listing 5-7).

```
--snip--
write_files:
  ① - content: H4sIAAAAAAC/7yabW/aShbH3/
    tTFmu0mjXOIml6Xoj9b8AQ6wSG9l0peyDrME+...
    encoding: gzip+base64
    path: /conf_files/define-region-params.sh
```

Listing 5-7: The lines in charge of creating get-region-params.sh in the user-data script

We have another encoded blob ①. Using some base64 and gunzip magic, we translate this pile of garbage to a normal bash script that defines various endpoints, usernames, and other parameters, depending on the region where the machine is running (see Listing 5-8). I will skip over the many conditional branches and case switch statements to only print the relevant parts.

```
root@Point1:~# echo H4sIAAA...|base64 -d |gunzip

AZ=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
REGION=${AZ%?}

case $REGION in
  ap-southeast-1...
  ;;
  eu-west-1
    echo "S3BUCKET=mxradr-d1" >> /etc/env.file ①
```