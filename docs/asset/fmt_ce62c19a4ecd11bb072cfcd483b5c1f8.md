
```
# tail /var/log/dpkg.log status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:04:07 status startup packages remove
2016-12-22 09:20:07 status installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 remove kali-linux-gpu:amd64 2016.3.2 <none>
2016-12-22 09:20:07 status half-configured kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status half-installed kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status config-files kali-linux-gpu:amd64 2016.3.2
2016-12-22 09:20:07 status not-installed kali-linux-gpu:amd64 <none>
```

## 使用 --reinstall 重新安装软件包

当你误移除或修改某些文件而不小心损坏系统时，恢复它们最简单的方法是重新安装该软件包。遗憾的是，软件包系统发现该软件包已安装，并礼貌地拒绝重新安装。为了避免这种情况，你会使用 `apt` 和 `apt-get` 命令的 `--reinstall` 选项。以下命令会在 `postfix` 已存在时重新安装它：

```
# apt --reinstall install postfix
```

`aptitude` 命令行略有不同，但通过 `aptitude` 可以实现相同的结果。`dpkg` 命令不会阻止安装，且很少被直接调用。

## 不要使用 --reinstall 从攻击中恢复

使用 `apt --reinstall` 来恢复在攻击期间被修改的软件包无疑无法将系统恢复到原来的状态。在攻击之后，你不能依赖它：`apt` 可能已经被恶意程序替换，攻击者可能已经更改或创建了 `dpkg` 控制之外的文件。记住，你也可以用 `apt` 指定特定的发行版本，这意味着你可以回滚到软件包的旧版本（例如，你知道该版本可以工作），只要该版本在 `sources.list` 中引用的某个源中仍然可用：

## 利用 --force-* 修复损坏的依赖

如果你不小心，使用 `--force-*` 选项或其他故障可能会导致 APT 系列命令无法工作。实际上，由于这些选项中的某些允许在依赖未满足或存在冲突时安装软件包。结果是从观点角度看系统是不一致的，APT 命令将拒绝执行任何除将系统恢复到一致状态以外的操作。这通常会导致类似下面的信息，是在安装新版本的 `libc6` 后得到的：

```
You might want to run 'apt-get -f install' to correct these.
The following packages have unmet dependencies:
desktop: Depends: libc6 (>= 2.5) but 2.3.6 is installed
Try 'apt-get -f install' to fix the broken dependencies.
```

### 8.2. graphical interfaces: aptitude and synaptic

> We will take a look at two of these interfaces: aptitude and synaptic

### Aptitude
