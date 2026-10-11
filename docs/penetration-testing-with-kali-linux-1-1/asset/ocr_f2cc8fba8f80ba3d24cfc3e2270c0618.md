This vulnerability is post-authentication, however, we discovered valid application credentials (admin / HUYfaw763) on another machine during the enumeration process.

# ### 15.2.3 Changing Connectivity Information

As we inspect the code, we realize the *base_url* variable needs to be changed to match our environment:

```
base_url = "http://192.168.1.10/cmsms/admin" 

_Listing 448 - base_url variable as defined in the original exploit_
```

We must modify the IP address and the protocol to HTTPS.

```
base_url = "https://19.11.0.128/admin" 

_Listing 449 - base_url variable updated to match our case_
```

We also notice that when browsing the target website, we are presented with a SEC_ERROR_UNKNOWN_ISSUER^393 error. This error indicates that the certificate on the remote host can not be validated. We need to account for this in the exploit code.

Specifically, the exploit is using the requests Python library to communicate with the target. The code makes three post requests on lines 34, 55 and 80:

```
. . . 
response = requests.post(url, data=data, allow_redirects=False) 
. . . 
response = requests.post(url, data=data, files=txt, cookies=cookies) 
. . . 
response = requests.post(url, data=data, cookies=cookies, allow_redirects=False) 
. . . 

_Listing 450 - All three post requests as defined in the original exploit_
```

The official documentation^394 indicates that the SSL certificate will be ignored if we set the verify parameter to False:

```
. . . 
response = requests.post(url, data=data, allow_redirects=False, **verify=False**) 
. . . 
response = requests.post(url, data=data, files=txt, cookies=cookies, **verify=False**) 
. . . 
response = requests.post(url, data=data, cookies=cookies, allow_redirects=False, **v** 
erify=False**) 
. . . 

_Listing 451 - Modified post requests to ignore SSL verification._
```

Finally, we also need to change the credentials used in the original exploit to match those found during the enumeration process. These are defined in the username and password variables at lines 15 and 16 respectively:

^393 (Mozilla, 2019). https://support.mozilla.org/en-US/kb/error-codes-secure-websites?as=u&utm_source=product
^394 (python-requests.org, 2019). http://docs.python-requests.org/en/master/user/advanced/#ssl-cert-verification