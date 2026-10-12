
```
[root@localhost vagrant#] dnf remove nodejs
Last metadata expiration check: 0:07:49 ago on Fri 16 Jun 2022 09:29:29 UTC.
Dependencies resolved.
=================================================================================
Package             Arch    Version                                     Repository Size
=================================================================================
Removing:
nodejs              x86_64  14.20.1-2.module+el8.6+20874+38992dc @appstream             37 M
nodejs-dev           x86_64  14.20.1-2.module+el8.6+20874+38992dce @appstream             967 k
nodejs-packaging    noarch   23-3.0.module+el8.3.78+cd3085                   41 k
srpm                x86_64  16.4-17.1.2.module+el8.6+20874+38992dc @ol8_appstream 15 M
Removing unused dependencies:
minobin            x86_64  10.8-3.0.el8                               @appstream             968 k
rotl-devel       x86_64  0-3.10.el8                               @appstream             53 k
dwz                x86_64  0.12-10.el8                               @appstream             225 k
efi-rpm-macros     noarch   3-3.0.el8                               @appstream             38 k
gnc-rpm-macros     noarch   1.4-2.7                                     appstream             414 k
gd                 noarch   3-2                                        appstream             33 k
keyutils-libs      x86_64  11.5-9.10                            @appstream_basest_latest 33 k
krb5-devel          x86_64  11.80-14.1.el8                            @appstream_basest_latest 1 M
libcrypt-devel       x86_64  1.45-14.10                           @appstream_basest_latest 1 M
libblkid           x86_64  11.16-24.1.el8                            @appstream             219 k
libselux-devel     x86_64  2.9-5.el8                               @appstream             127 k
libepsol-devel      x86_64  6.4-3.el8                               @appstream             127 k
libreadline-macros  noarch   3-3.5.el8                               @appstream             35 k
nocaml-rpm-macros    noarch   5-4.el8                               @appstream             37 k
openblas-rpm-macros noarch   2-2.el8                               @appstream             104 k
openssl-devel       x86_64  1.1.1k-6.el8_5                            @appstream             3.4 M
pcre2-devel          x86_64  10.32-2                            @appstream_latest 1.8
pcre2-utf1         x86_64  10.32-2                            @appstream_latest 570
pcre2-utf2          noarch   3-2.el8                               @appstream_latest 780
perl-rpm-macros     noarch   3-4.el8                               @appstream             4.2
python-rpm-macros   noarch   3-4.el8                               @appstream             5.1
python3-rpm-macros  noarch   5.15.3.el8                            @appstream             3.6
qt5-rpm-macros      noarch   0                                      @appstream_basest_latest 429 k
redhat-rpm-macros   noarch   129-1.0.el8                           @appstream_basest_latest 149
rust-rpm-macros     noarch   5-2.el8                               @appstream             1.1
zip                  x86_64  6.0-46.1.el8                            @appstream_basest_latest 422 k
```

## 有...

那么，既然我们已经涵盖了 `AppStream` 的用法，你可能会问自己：“我们以前不是已经通过 `Software Collections` 有类似的功能了吗？”答案是肯定的，但 `Software Collections` 和 `AppStream` 之间存在巨大的差异。

`Software Collections` 提供了并行可用（`Parallel Availability`）和并行安装（`Parallel Installability`），而 `AppStream` 只提供并行可用。

根据 Fedora 文档，*并行可用意味着热门软件项目有多个主版本供安装。*而*并行安装意味着可以在同一个用户空间中安装一个软件项目的多个主版本。*

现在你可能会问：“等等，所以你是在告诉我 `AppStream` 并不像我们之前的工具那样好？”嗯，确实如此。事实证明，并行安装并没有想象中那么好。虽然从表面上看在同一个系统上安装多个版本的软件似乎很不错，但它充满了复杂性，需要用户知道要做一些额外的操作才能使用已安装的软件或备用版本。例如，如果你想安装多个版本的 `Node.js`，你首先需要启用相应的 `Software Collection`，然后你还需要知道该去哪里查找并激活你想使用的特定版本。换句话说，你无法以普通方式直接使用备用版本，因为软件包将安装在非标准位置。

# 狮子、老虎与容器——噢我的天！Podman 及其朋友们
