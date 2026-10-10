
当在 `man.viewer` 配置变量中指定 `konqueror` 时，我们将启动 `kfmc1ient` 以尝试在新的标签页中打开已在 `konqueror` 中打开的 man 手册页（如果可能）。

为了保持一致性，如果 `man.konqueror.path` 设置为类似 `A_PATH_TO/konqueror` 的值，我们也会尝试这种技巧。这意味着我们将尝试启动 `A_PATH_TO/kfmc1ient`。如果您确实想使用 `konqueror`，可以使用如下示例：

```
[man]  viewer = konqueror
[man "konq"]  cmd = A_PATH_TO/konqueror
```

### 关于 git config —global 的注意事项

请注意，所有这些配置变量可能都应当使用 `--global` 标志进行设置，例如像这样：

```
$ git config --global help.format web
$ git config --global web.browser firefox
```

因为它们可能更偏向于用户级别而非仓库级别。有关此配置的更多信息，请参阅 `git-config(1)`。

## GIT-HTTP-BACKEND

### NAME

`git-http-backend` - Git 通过 HTTP 协议的服务器端实现

### SYNOPSIS

```
git http-backend
```

### DESCRIPTION

一个简单的 CGI 程序，用于向通过 `http://` 和 `https://` 协议访问仓库的 Git 客户端提供 Git 仓库的内容。该程序支持使用智能 HTTP 协议和向后兼容的哑 HTTP 协议进行拉取操作的客户端，以及使用智能 HTTP 协议进行推送操作的客户端。

它会验证目录中是否存在 "`git-daemon-export-ok`" 魔术文件，除非设置了环境变量 `GIT_HTTP_EXPORT_ALL`，否则它将拒绝导出任何未通过此方式明确标记为可导出的 Git 目录。

默认情况下，仅启用 `upload-pack` 服务，该服务于 `git fetch-pack` 和 `git ls-remote` 客户端，这些客户端由 `git fetch`、`git pull` 和 `git clone` 调用。如果客户端已通过身份验证，则启用 `receive-pack` 服务，该服务于 `git send-pack` 客户端，由 `git push` 调用。

### SERVICES

这些服务可以使用每仓库的配置文件进行启用/禁用：

- `http.getanyfile`

  此功能服务于版本早于 1.6.6 且无法使用 `upload pack` 服务的 Git 客户端。启用后，客户端可以读取仓库内的任何文件，包括那些不再从分支可达但仍然存在对象。默认启用，但仓库可以通过将此配置项设置为 `false` 来禁用它。

- `http.uploadpack`

  此功能服务于 `git fetch-pack` 和 `git ls-remote` 客户端。默认启用，但仓库可以通过将此配置项设置为 `false` 来禁用它。

- `http.receivepack`

  此功能服务于 `git send-pack` 客户端，允许推送。对于匿名用户，默认禁用；对于通过 Web 服务器认证的用户，默认启用。可以通过将此项设置为 `false` 来禁用，或设置为 `true` 以启用所有用户（包括匿名用户）。

### URL TRANSLATION

为了确定磁盘上仓库的位置，`git http-backend` 会连接环境变量 `PATH_INFO`（由 Web 服务器自动设置）和 `GIT_PROJECT_ROOT`（必须在 Web 服务器配置中手动设置）。如果 `GIT_PROJECT_ROOT` 未设置，`git http-backend` 将读取 `PATH_TRANSLATED`，这也是由 Web 服务器自动设置的。

### EXAMPLES

以下所有示例都映射到 `/var/www/git/foo/bar.git`。

#### Apache 2.x

确保 `mod_cgi`、`mod_alias` 和 `mod_env` 已启用，适当设置 `GIT_PROJECT_ROOT`（或 `DocumentRoot`），并创建一个指向 CGI 的 `ScriptAlias`：

```
SetEnv GIT_PROJECT_ROOT /var/www/git
SetEnv GIT_HTTP_EXPORT_ALL
ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/
```

若要启用匿名读取权限但启用经过身份验证的写入权限，需要对初始引用通告（我们通过查询字符串中的服务参数检测为推送）以及 `receive-pack` 调用本身都要求授权：

```
RewriteCond %{QUERY_STRING} service=git-receive-pack [OR]
RewriteCond %{REQUEST_URI} /git-receive-pack
RewriteCond /git/ - [E=AUTHREQUIRED:yes]

<LocationMatch "^/git/" >
    Order Deny,Allow
    Deny from env=AUTHREQUIRED
    AuthType Basic
    AuthName "Git Access"
    Require group committers
    Satisfy Any
</LocationMatch>
```

如果您没有 `mod_rewrite` 可用于匹配查询字符串，那么仅仅保护 `git-receive-pack` 本身就足够了，例如：

```
<LocationMatch "^/git/.*/git-receive-pack$" >
    AuthType Basic
    AuthName "Git Access"
    Require group committers
</LocationMatch>
```

在此模式下，直到客户端实际开始推送的对象协商阶段，服务器才会请求身份验证，而不是在初始接触时。因此，您必须在任何应接受推送的仓库中启用 `http.receivepack` 配置选项。如果未设置 `http.receivepack`，默认行为是拒绝未验证用户的任何推送；因此，初始请求将向客户端报告 403 Forbidden，甚至没有提供身份验证的机会。

若要要求读取和写入都进行身份验证，请使用 `Location` 指令围绕仓库或其父目录之一：

```
<Location /git/private>
    AuthType Basic
    AuthName "Private Git Access"
    Require group committers
</Location>
```

要在相同的 URL 下提供 `gitweb`，请使用 `ScriptAliasMatch` 将仅 `git-http-backend` 能够处理的 URL 指向 `git-http-backend`，并将其余部分转发给 `gitweb`：

```
ScriptAliasMatch \
    "(?x)^/git/(.*/HEAD | \
             info/refs | \
             objects/(info/[^/]+ | \
             [0-9a-f]{2}/[0-9a-f]{38} | \
             pack/pack-[0-9a-f]{40}\.(pack|idx)) | \
             git-(upload|receive)-pack)$" \
    /usr/libexec/git-core/git-http-backend/$1
ScriptAlias /git/ /var/www/cgi-bin/gitweb.cgi/
```

要从单个仓库中服务来自不同 (7) 的多个仓库：

```
SetEnvIf Request_URI "^/git/([^/])" GIT_NAMESPACE=$1
ScriptAliasMatch ^/git/[^/]*(.*) /usr/libexec/git-core/git-http-backend/storage.git$1
```

#### 加速的静态 Apache 2.x

与上述配置类似，但 Apache 可用于返回存储在磁盘上的静态文件。在许多系统上，这可能效率更高，因为 Apache 可以让内核直接将文件内容从文件系统复制到网络：
