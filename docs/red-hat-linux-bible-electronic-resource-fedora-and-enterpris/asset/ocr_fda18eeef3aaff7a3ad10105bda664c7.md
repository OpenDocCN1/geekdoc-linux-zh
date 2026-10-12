```
-----BEGIN CERTIFICATE-----
MIIEFjCCAwgAwIBAgIOMI26ZZd6njZgn97tJAVFODANBgqkhgiG9w0BAQQFADCB
ujEIMB0GA1UECWMhWmVyAaNpZ24gVHlc3QgTmdVddiEludcglBnybFm0aW9wYWxwgDUzVy
dmNP2Z24siE1uL4y4xAxMzxBgNVBASTkTLZ1iCmlTawDuEIudzglcymFoaW9wYXwgUDFVv
dmVjIENBC0gZ2xxc3MgMzFJMEc1orYZG0d3d3LnZlLnlZdWd3dWMlaB0W9uXwgUFJmg
SW5jb3JwLWm5JfJLZ1igTE1B0klMSVRZilZEUXC4gYyk5NyBWZZXJPuZ1njbAeFw0w
MzXZKBuWdAWDMDaEFvm0wNDMwMTYu5UNTETAMVQMQswcqDVQ2N1E2VUZtUETmBEG
A1UECBMKV2F2aGlud33RvHiTxErE371UEBXQLRmVcZXZxJbCbcXYKxGzAZBgNVBAOU
Ek1ETS7TZXj2aWmLcwngSW51LJjEMMAG0AIUECQxd3d3MTMwMwQYDVQQFCpUZXJtcI
cyBviZB1c2UyYXQgd3d3LnZlcm1zLnB5cGEcgEGKGMPMDAXFDASBgNVBAMUC2lkbX
N1cm5uY29M1uMIGEMAOGCSQGS1b3DQBEQAQUAA4GNADCBiOQKBgQDaHsk+uZO/
7jjDPFEnqT80BaIL3yPILxFjhj3xPMXLGwZLmkDmdQjXsa4x7AhEpr1ubuVnhVJiO
FnLDopsx4p7r4n+P8FyS4M5ggrbcQOzyYNk2jjqyVF/7yOW2pd13ot4eacyYaza4Og
g9PTxhU2jEG4twvKCAFWhuEogUICMV2gQIDAQABo41BJTCCASEwQCDVRO7bTA1w
A DEBgbNVHSAePTA7mDMGGCGCSAGAG+EBBxbcDMCoKAYIkwYBBOUHAgEWGHOdHBz
Oia8vd3d3LnZ1cm1laWdDuLmnNvB5yc6EwCWyDVRPBAqADAgWgMCGAJLUdJQJHM8G
CwcGSA G+EIEMO0CoW1YQBuAwGGCCcGAQuFBNXwmCQMDOCGCCAGQFbWBEBbCGwJ/Ak
BpgBrEBPGCoaYYA/XROcDovL29jczAudlOclb1FAj5xP17B68wxLKTeRu4Novu13
06As5OdeGNW0dAHA6LY9jcMwuDMVyaxNpZ24uY2R0LON5XXNzm01udGVybFbmFoW9w
YXkXZKXZZXXIuYj3UsMBkgCcSMCgSAG+E+eF4Cec3zYJODASzNmwMTeYMa0GSCsq
GSB13 DQEBBAUAAG4BAJ/Psvtcm1dSkQi5nuEudLc0b1FAj5xP17B68wxLKTeRu4Novu13
8lLLZnAr+acHCCwK0l3rQpJgV2y1mwj/kPnC1WjoYefXdh7+Mbg/6f6mmlK9auW
TRIPW/+aBO8RyOJLMA2VQQvhX42njJGpcWNY9AGSHm1UEBjSyvtb1lX
```

Copy and paste this certificate into an empty file called `server.crt`, which must reside in the `/etc/httpsd/conf/ssl.crt` directory, and restart your Web server:

```
`# service httpsd restart`
```

Assuming your Web site was previously working fine, you can now view it in a secure fashion by placing an "s" after the `http` in the Web address. So if you previously viewed your Web site at `http://www.acmerarina.com`, you can now view it in a secure fashion by going to `https://www.acmerarina.com`.

# ## Creating Self-Signed Certificates

Generating and running a self-signed SSL certificate is much easier than having a signed certificate. To generate a self-signed SSL certificate, do the following:

+   1.  Remove the key and certificate that currently exist:

```
`# cd /etc/httpd/conf`
`# rm ssl.key/server.key ssl.crt/server.crt`
```

+   2.  Create your own server key:

```
`# /usr/bin/openssl genrsa 1024 > ssl.key/server.key`
```

+   3.  Make the `server.key` file readable and wrable only by root: