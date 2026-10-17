
```
openssl des -salt -in originalfile.txt -out encrypted.txt
```

要解密，唯一的区别是使用`-d`选项（表示解密），并将加密的文件名放在未加密的输出文件之前。示例如下：

```
openssl des -d -salt -in encryptedfile.txt -out decrypted.txt
```
