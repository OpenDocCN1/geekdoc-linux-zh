Forget about breaking free from this single insignificant host. How about crushing the entire floor—nay, the entire building—with a single stroke? Now that would be a tale worth telling.

Remember how we dumped environment variables in “Arbitrary Code Execution” on page 92? We confirmed the template injection vulnerability and focused on Django-related variables because that was the main task at hand, but if you paid close attention, you may have caught a glimpse of something tremendously more important. Something much more grandiose.

Let me show you the output once more:

```
shell> env

PATH=/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOME=/root
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
--snip--
```

We are running inside a container managed by a Kubernetes cluster! Never mind this lonely, overstaffed worker machine; we have a chance of bringing down the whole kingdom!

# Resources

+   - Burp is famous for its Active Scanner, which automates much of the parameter reconnaissance phase. Alternatively, you can try some extensions that fuzz for various vulnerabilities. Snoopy Security maintains an interesting compilation of such extensions at https://github.com/snoopyscurity/awesome-burp-extensions/.
- Check out James Kettle’s talk “Server-Side Template Injection: RCE for the Modern Webapp” to learn about various exploitation techniques: https://www.youtube.com/watch?v=3cT0uE7Y87s.
- The Docker reference is available at https://dockr.ly/2sgaVhj.
- A great article about container breakout is “The Route to Root: Container Escape Using Kernel Exploitation,” where Nimrod Stoler uses CVE-2017-7308 to escape isolation: http://bit.ly/2TfJZHV1.
- Find descriptions of other exploits at https://unit42.paloaltonetworks.com/.