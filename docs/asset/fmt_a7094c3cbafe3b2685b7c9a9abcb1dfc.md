
编号目录中还有其他信息，例如 `maps` 管道，它可以显示进程在内存中映射了哪些共享库和其他可加载模块。这对于包含可加载模块方案以添加功能的程序（如 Apache）非常有用。

```
tschenk@quicksilver:/proc/642 [1007]$ cat maps
00848000-00870000 r-xp 00000000 08:02 143375
→/usr/sbin/httpd
00870000-00871000 rw-p 00027000 08:02 143375
→/usr/sbin/httpd
00871000-00886000 r-xp 00000000 08:00 0
40000000-40012000 r-xp 00000000 08:02 30722
→/lib/ld-2.1.1.so
40012000-40013000 rw-p 00011000 08:02 30722
→/lib/ld-2.1.1.so
40013000-40014000 r-xp 00000000 08:00 0
40014000-40015000 rw-p 00000000 08:00 0
40015000-40016000 r-xp 00000000 08:02 178204
→/usr/lib/apache/mod_env.so
40016000-40017000 rw-p 00000000 08:02 178204
→/usr/lib/apache/mod_env.so
40017000-40018000 r-xp 00000000 08:02 178211
→/usr/lib/apache/mod_log_agent.so
40018000-40019000 rw-p 00000000 08:02 178211
→/usr/lib/apache/mod_log_agent.so
4001a000-40035000 r-xp 00000000 08:02 30740
→/lib/libm-2.1.1.so
40035000-40036000 rw-p 0001a000 08:02 30740
→/lib/libm-2.1.1.so
40036000-4003b000 r-xp 00000000 08:02 30731
→/lib/libcrypt-2.1.1.so
4003b000-4003c000 rw-p 00004000 08:02 30731
→/lib/libcrypt-2.1.1.so
4003c000-4003d000 rw-p 00000000 08:00 0
4003d000-4009b000 r-xp 00000000 08:02 30733
→/lib/libdb-2.1.1.so
4009b000-4009d000 rw-p 00037000 08:02 30733
→/lib/libdb-2.1.1.so
4009d000-4009f000 r-xp 00000000 08:02 30738
→/lib/libdl-2.1.1.so
4009f000-400a0000 rw-p 00001000 08:02 30738
→/lib/libdl-2.1.1.so
400a0000-400a1000 r-xp 00000000 08:00 0
400a1000-400b7000 r-xp 00000000 08:02 30729
→/lib/libc-2.1 (deleted)
401b7000-401dc000 rw-p 00065000 08:02 30729
→/lib/libc-2.1 (deleted)
401dc000-401df000 rw-p 00000000 08:00 0
4016f000-40191000 r-xp 00000000 08:02 178212
→/usr/lib/apache/mod_log_config.so
40191000-40193000 rw-p 0001000 08:02 178212
→/usr/lib/apache/mod_log_config.so
40193000-40194000 r-xp 00000000 08:02 178213
→/usr/lib/apache/mod_log_referer.so
40194000-40195000 rw-p 00000000 08:02 178213
→/usr/lib/apache/mod_log_referer.so
40195000-40197000 r-xp 00000000 08:02 178214
→/usr/lib/apache/mod_mime.so
40197000-40198000 rw-p 00000000 08:02 178214
→/usr/lib/apache/mod_mime.so
40198000-4019d000 r-xp 00000000 08:02 178217
→/usr/lib/apache/mod_negotiation.so
4019d000-4019e000 rw-p 00000000 08:02 178217
→/usr/lib/apache/mod_negotiation.so
4019e000-401a1000 r-xp 00000000 08:02 178221
→/usr/lib/apache/mod_status.so
401a1000-401a2000 rw-p 00000000 08:02 178221
→/usr/lib/apache/mod_status.so
401a2000-401a5000 r-xp 00000000 08:02 178210
→/usr/lib/apache/mod_info.so
401a5000-401a6000 rw-p 00000000 08:02 178210
→/usr/lib/apache/mod_info.so
401a6000-401ac000 r-xp 00000000 08:02 178209
→/usr/lib/apache/mod_include.so
401ac000-401ad000 rw-p 00000000 08:02 178209
→/usr/lib/apache/mod_include.so
401ad000-401b1000 r-xp 00000000 08:02 178198
→/usr/lib/apache/mod_autoindex.so
401b1000-401b3000 rw-p 00000000 08:02 178198
→/usr/lib/apache/mod_autoindex.so
401b3000-401b4000 r-xp 00000000 08:02 178203
→/usr/lib/apache/mod_dir.so
401b4000-401b5000 rw-p 00000000 08:02 178203
→/usr/lib/apache/mod_dir.so
401b5000-401b7000 r-xp 00000000 08:02 178201
→/usr/lib/apache/mod_cgi.so
401b7000-401b8000 rw-p 0001000 08:02 178201
→/usr/lib/apache/mod_cgi.so
401b8000-401b9000 r-xp 00000000 08:02 178194
→/usr/lib/apache/mod_asis.so
401b9000-401ba000 rw-p 00000000 08:02 178194
→/usr/lib/apache/mod_asis.so
401ba000-401bd000 r-xp 00000000 08:02 178208
→/usr/lib/apache/mod_imap.so
401bd000-401be000 rw-p 00002000 08:02 178208
→/usr/lib/apache/mod_imap.so
401be000-401bf000 r-xp 00000000 08:02 178192
→/usr/lib/apache/mod_actions.so
401bf000-401c0000 rw-p 00000000 08:02 178192
→/usr/lib/apache/mod_actions.so
401c0000-401c1000 r-xp 00000000 08:02 178223
→/usr/lib/apache/mod_userdir.so
401c1000-401c2000 rw-p 00000000 08:02 178223
→/usr/lib/apache/mod_userdir.so
401c2000-401d0000 r-xp 00000000 08:02 178190
→/usr/lib/apache/libproxy.so
401d0000-401d1000 rw-p 0000d000 08:02 178190
→/usr/lib/apache/libproxy.so
401d1000-401d3000 r-xp 00000000 08:02 178193
→/usr/lib/apache/mod_alias.so
401d3000-401d4000 rw-p 00001000 08:02 178193
→/usr/lib/apache/mod_alias.so
401d4000-401de000 r-xp 00000000 08:02 178218
→/usr/lib/apache/mod_rewrite.so
401de000-401df000 rw-p 00009000 08:02 178218
→/usr/lib/apache/mod_rewrite.so
401df000-401e0000 r-xp 00000000 08:02 178191
→/usr/lib/apache/mod_access.so
401e0000-401e2000 rw-p 00000000 08:02 178191
→/usr/lib/apache/mod_access.so
401e2000-401e4000 r-xp 00000000 08:02 178195
→/usr/lib/apache/mod_auth.so
401e4000-401e5000 rw-p 00001000 08:02 178195
→/usr/lib/apache/mod_auth.so
401e5000-401e6000 r-xp 00000000 08:02 178196
→/usr/lib/apache/mod_auth_anon.so
401e6000-401e7000 rw-p 00000000 08:02 178196
→/usr/lib/apache/mod_auth_anon.so
401e7000-401e8000 r-xp 00000000 08:02 178197
→/usr/lib/apache/mod_auth_db.so
401e8000-401e9000 rw-p 00000000 08:02 178197
→/usr/lib/apache/mod_auth_db.so
401e9000-401eb000 r-xp 00000000 08:02 178202
→/usr/lib/apache/mod_digest.so
401eb000-401ec000 rw-p 00001000 08:02 178202
→/usr/lib/apache/mod_digest.so
401ec000-401ed000 r-xp 00000000 08:02 178206
→/usr/lib/apache/mod_expires.so
401ed000-401ee000 rw-p 00000000 08:02 178206
→/usr/lib/apache/mod_expires.so
401ee000-401ef000 r-xp 00000000 08:02 178207
→/usr/lib/apache/mod_headers.so
401ef000-401f0000 rw-p 00000000 08:02 178207
→/usr/lib/apache/mod_headers.so
401f0000-401f1000 r-xp 00000000 08:02 178224
→/usr/lib/apache/mod_usertrack.so
401f1000-401f2000 rw-p 00000000 08:02 178224
→/usr/lib/apache/mod_usertrack.so
401f2000-401f3000 r-xp 00000000 08:02 178219
→/usr/lib/apache/mod_setenvif.so
401f3000-401f4000 rw-p 00000000 08:02 178219
→/usr/lib/apache/mod_setenvif.so
401fa000-40202000 r-xp 00000000 08:02 30760
→/lib/libnss_files-2.1.1.so
40202000-40203000 rw-p 00007000 08:02 30760
→/lib/libnss_files-2.1.1.so
40203000-40204000 rwxp 00000000 00:00 0
bfffb000-c0000000 rwxp ffff c000 00:00 0
```

正如你所见，此输出不仅显示了 apache 使用的模块和共享库，还显示了它们的位置。这些信息在调试时非常有用。`maps` 文件的完整细节可在 `proc` 手册页中找到，可通过以下命令获取：

```
```
