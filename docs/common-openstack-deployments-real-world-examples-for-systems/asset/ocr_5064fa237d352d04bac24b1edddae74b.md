# Tip

If you have configured your instances to be online via a real public floating IP address, you can clone the repository directly on the instance and have no need to scp the files over. We haven't made the assumption in these deployment scenarios that your instances have Internet access, so this is how we've configured things.

You will now have a swift directory in the ubuntu user home directory of your instance. You will want to edit the swift/index.html file to include the URL for your object in Swift, so take the URL you created earlier with your image and add it to the img src line like so:

```
<img src='http://10.190.0.8:8080/v1/KEY_A49446773bf4b7bab30b3c4bca06d82d/zoo/eagle.jpg'
    alt='Image loaded from Swift'>
```

To launch a simple http server, run the following on your instance:

```
$ cd swift
$ python -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...
```

As you can see, by default, this will load a simple HTTP server using Python on port 8000. You can navigate to this on a system that has access to your instance by navigating to http://10.190.0.8:8000 in your browser, where 10.190.0.8 is the IP of your instance, or your floating IP. The resulting page will look something like what you see in Figure 9.9. Congratulations! You have now used an image object served up by Swift on a web page.

# Welcome to the...
## Common OpenStack Deployments
Swift Demonstration

![](bbox=[0.1, 0.61, 0.86, 0.83])

Common OpenStack Deployments is brought to you by Elizabeth K. Joseph and Matt Fischer.



Figure 9.9 A simple web site referencing an object from Swift