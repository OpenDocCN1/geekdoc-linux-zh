# AUTHENTICATION AGENT

**pkcheck**, like any other polkit application, will use the authentication agent registered for the process in question. However, if no authentication agent is available, then **pkcheck** can register its own textual authentication agent if the option `—enable-internal-agent` is passed.