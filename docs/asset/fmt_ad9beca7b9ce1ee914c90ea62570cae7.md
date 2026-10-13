
© 1999-2000 Gerard Mourani and Open Network Architecture ®

关于本书的意见和建议请邮件至 `gmourani@videotron.ca`

证书有效期至 2000年12月1日 14:59:29 GMT (365天)
是否签名证书？[y/n]y

1 个/1 个证书请求已通过认证，提交？[y/n]y
写入带有1 个新条目的数据库
数据库已更新
CA 验证：`server.crt` <-> CA cert
`server.crt`: OK

这会签名 CSR 并生成一个 `server.crt` 文件。
```
[root@deep ssl]# mv server.crt/
```

现在你有两个文件：`server.key` 和 `server.crt`。它们现在可以如下方式在你的 Apache 的 `httpd.conf` 文件中使用：

`SSLCertificateFile` `/etc/ssl/server.crt` 我们的服务器公钥
`SSLCertificateKey` `/etc/ssl/private/server.key` <-- 我们的服务器私钥

`server.csr` 文件不再需要。
```
[root@deep ssl]# rm -f server.csr
```

## SSL 加固

将你的密钥设置为 "root" 可“读写”。这很重要，因为没有人需要触碰这些文件。

- 使用以下命令将你的密钥设置为"root" 可“只读”：
```
[root@deep ssl]## chmod 600 /etc/ssl/certs/ca.crt
[root@deep ssl]$# chmod 600 /etc/ssl/certs/server.crt
[root@deep ssl]$# chmod 600 /etc/ssl/certs/ca.key
[root@deep ssl]$# chmod 600 /etc/ssl/private/server.key
```

### OpenSSL 软件的一些可能用途
OpenSSL 可用于：

- 1. 创建你自己的证书服务器。
- 2. 为用户提供传输过程数据机密性、完整性、认证和电子签名。
- 3. 安全电子贸易交易。

## 安装的文件

```
/etc/ssl > /usr/man/man1/verify.1

/etc/sslc > /usr/man/man1/version.1

/etc/ssl/certs > /usr/man/man1/x509.1

/etc/ssl/private > /usr/man/man3/BN_CTX_new.3

/etc/ssl/openssl.conf > /usr/man/man3/BN_CTX_start.3

/usr/bin/openssl > /usr/man/man3/BN_add.3

/usr/bin/rehash > /usr/man/man3/BN_add_word.3

/usr/bin/sign_ha > /usr/man/man3/BN_decbin.3

/usr/bin/hash > /usr/man/man3/BN_cmp.3

/usr/bin/info > /usr/man/man3/BN_copy.3

/usr/bin/issuer > /usr/man/man3/BN_generate_prime.3

/usr/bin/name > /usr/man/man3/BN_inverse.3

/usr/bin/printer_chop > /usr/man/man3/BN_mul_montgomery.3

/usr/bin/openssl > /usr/man/man3/BN_mul_reciprocal.3

/usr/include/openssl/e_os.h

/usr/include/openssl/a_os.h

/usr/include/openssl/crypto.h

/usr/include/openssl/tmdff.h

/usr/include/openssl/opensiv.h

/usr/include/openssl/sslconf.h

/usr/include/openssl/dh.h

/usr/include/openssl/md32.h

/usr/include/openssl/md5.h

/usr/include/openssl/sha.h

/usr/include/openssl/hmac.h

/usr/include/openssl/ripemd.h

/usr/include/openssl/des.h

/usr/include/openssl/rc2.h

/usr/include/openssl/rc4.h

/usr/include/openssl/rc5.h

/usr/include/openssl/blowfish.h

/usr/include/openssl/cast.h

/usr/include/openssl/bn.h

/usr/include/openssl/rsa.h

/usr/include/openssl/dh.h

/usr/include/openssl/buffer.h

/usr/include/openssl/stack.h

/usr/include/openssl/safestack.h

/usr/include/openssl/hash.h

/usr/include/openssl/rand.h

/usr/include/openssl/aes.h

/usr/include/openssl/objects.h

/usr/include/openssl/evp.h

/usr/include/openssl/aes1.h

/usr/include/openssl/sha1_mac.h

/usr/include/openssl/pem.h

/usr/include/openssl/pem2.h

/usr/include/openssl/x509.h

/usr/include/openssl/x509_v3.h

/usr/include/openssl/conf.h

/usr/include/openssl/bt_db.h

/usr/include/openssl/pkcs7.h

/usr/include/openssl/pkcs12.h

/usr/include/openssl/comp.h

/usr/include/openssl/obj.h

/usr/include/openssl/ssha2.h

/usr/include/openssl/ss53.h

/usr/include/openssl/ts1.h

/usr/include/openssl/x5.h

/usr/include/openssl/rehash.h

/usr/lib/libcrypto.a

/usr/lib/libssl.a

/usr/lib/libdg5.a

/usr/man/man1/CA.1

/usr/man/man1/asn1parse.1

/usr/man/man1/ca.1

/usr/man/man1/ciphers.1

/usr/man/man1/ecf.1

/usr/man/man1/cr12pkcs7.1

/usr/man/man1/dgam1.1

/usr/man/man1/dhamparam.1

/usr/man/man3/BN_new.3

/usr/man/man3/BN_num_bytes.3

/usr/man/man3/BN_rand.3

/usr/man/man3/BN_set_bit.3

/usr/man/man3/BN_zero.3

/usr/man/man3/CRYPTO_set_ex_data.3

/usr/man/man3/DH_generate_key.3

/usr/man/man3/DH_generate_new_index.3

/usr/man/man3/DH_new.3

/usr/man/man3/DH_set_method.3

/usr/man/man3/DSA_SIG_new.3

/usr/man/man3/DSA_do_sig.3

/usr/man/man3/DSA_dap_DH.3

/usr/man/man3/DSA_generate_key.3

/usr/man/man3/DSA_get_new_index.3

/usr/man/man3/DSA_new.3

/usr/man/man3/DSA_set_method.3

/usr/man/man3/DSA_sign.3

/usr/man/man3/DSA_size.3

/usr/man/man3/ERR_LIB.3

/usr/man/man3/ERR_clear_error.3
```
