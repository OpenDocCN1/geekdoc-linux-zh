
# 列出以获取文件。
private_get      = yes

# private_index    [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能获取文件索引。
private_index    = yes

# private_info      [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能使用 info <list> 命令。
private_info     = no
# private_which     [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能获取该列表的 which 信息。
private_which    = no

# private_who       [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能使用 who 命令。
private_who      = yes

# purge_received    [bool] (no) <resend>
# 在转发消息之前删除所有已接收行。
purge_received   = no

# reply_to          [word] () <resend,digest>
# 将带有值 <value> 的 reply-to 头部放入
# 外发消息中。如果使用令牌 $SENDER，则
# 发送者的地址将用作 reply-to 头部的值
# 这是 reply-to 头部的值，用于
# 摘要列表。
reply_to         =

# resend_host       [word] (undef) <resend>
# 附加到所有地址字符串的主机名
# 指定用于 resend。
resend_host      =

如果要限制发帖，文件列表应为主要列表和摘要列表的成员列表。在这种情况下，使用的值为 /usr/local/majordomo/lists/listname:/usr/local/majordomo/lists/listname-digest。

# restrict_post   [restrict_post] (undef) <resend>
# 如果定义，则只有在其中一个文件中列出的地址（以冒号
# 或空格分隔）才能向邮件列表发帖。这
# 看起来似乎很有用，但实际上用处不大，因为没有
# 办法在没有访问权限的情况下创建这些文件
# 运行 resend 的机器。此机制将
# 在 majordomo/resend 的未来版本中被替换。
restrict_post   =

# sender          [word] (owner-digestonly-sample) <majordomo,resend>
# 转发邮件的信封和发件人地址。此
# 字符串附加了 "%e" 和 resend_host 的值
# 以构成完整地址。对于 majordomo，它提供
# 订阅命令生成欢迎邮件消息的发件人地址
# 作为订阅命令的一部分。
sender          = owner-digestonly-sample

# strip           [bool] (yes) <majordomo>
# 将地址添加到列表时，剥离所有注释
# 等，并仅将原始地址放入列表文件。在
# 除了关键字之外，如果文件 <listname>.strip
# 存在，则与指定 yes 值相同。该
# yes 值会被此关键字的取值覆盖。
strip           = yes

# subject_prefix  [word] (undef) <resend>
# 如果主题中尚未存在，此词将被加前缀到主题行
# 。文本在使用前会进行扩展
# 。定义了以下扩展令牌：
# $LIST - 当前列表的名称，$SENDER -
# 从 from 行获取的发件人，$VERSION，版本
# 为 majordomo。
subject_prefix  =

# subscribe_policy [enum] (open) <majordomo>
# /open;closed;auto/
# 三个可能值之一：open、closed、auto。Open
# 允许人们自行订阅列表。Auto
# 允许任何人无需维护者批准即可订阅任何人到列表
# 。文件
# <listname>.auto 的存在与指定值 auto 相同。
# Closed 需要维护者批准所有订阅
# 请求到列表。此外，除了关键字之外，如果
# 文件 <listname>.closed 存在，则与
# 指定值 closed 相同。此关键字的取值
# 会覆盖任何存在文件提供的取值。
subscribe_policy = open

最后，以下是摘要的配置文件。这是一个封闭列表；实际上，从不允许任何人订阅它。这将是一项毫无意义的练习，因为其成员列表永远不会被使用。

仅显示与主列表的更改。大多数配置是相同的。

# description    [string] (undef) <majordomo>
# 用于在回复时对邮件列表的描述
# lists 命令。没有引用机制，并且
# 只有大约 50 个字符的空间。
description  = 'Sample digest-only list (digest)'

# digest_archive  [absolute_dir] (undef) <digest>
# 摘要归档保存的目录。此项
# 目前不起作用。留空。
digest_archive  =

摘要问题将由 mkdigest 自动更新。摘要卷必须手动更新。

# digest_issue    [integer] (1) <digest>
# 下一期的期号
digest_issue    = 23

# digest_name     [string] (digestonly-sample-digest)
# <digest> 摘要的主题行。此字符串
# 附加了卷号和期号。
digest_name  = Sample Digest

# digest_volume   [integer] (1) <digest>
# 当前卷号
digest_volume   = 1

# digest_work_dir  [absolute_dir] (undef) <digest>
# 用于摘要的临时空间目录。不要
# 在你知道自己在做什么之前更改此设置
digest_work_dir  =

# message_footer  [string_array] (undef) <resend,digest>
# 将附加到发布到所有消息末尾的文本
# 列表。
message_footer  << END

END

# message_fronter  [string_array] (undef) <resend,digest>
# 将前置到所有消息开头的文本
# 发布到列表。文本在使用前会进行扩展。
# 定义了以下扩展令牌：$LIST -
# 当前列表的名称，$SENDER - 发件人作为
# 从 from 行获取，$VERSION，版本
# 为 majordomo。如果在摘要中使用，则只有扩展令牌
# $_SUBJECTS 可用，它会扩展为
# 摘要中消息主题的列表
message_fronter  << END

END

# message_headers  [string_array] (undef) <resend,digest>
# 这些头部将被附加到
# 发布消息的头部。文本在使用前会进行扩展。
# 定义了以下扩展令牌：$LIST -
# 当前列表的名称，$SENDER 发件人作为
# 从 from 行获取，$VERSION，majordomo 的版本。
message_headers  << END

END

由于从不应该有人向摘要列表发帖，我们将其设置为 moderated，并在配置中 moderate=yes。

# moderate        [bool] (no) <resend>
# 如果为 yes，则列表的所有帖子必须由
# 版主批准。
moderate         =  yes

# private_get  [bool] (yes) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能获取文件。
private_get  = yes

# private_index  [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能获取文件索引。
private_index  = yes

# private_info  [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能使用 info <list> 命令。
private_info  = no

# private_which  [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能获取该列表的 which 信息。
private_which  = no

# private_who  [bool] (no) <majordomo>
# 如果设置为 yes，则请求者必须在邮件
# 列表中才能使用 who 命令。
private_who  = yes

# purge_received  [bool] (no) <resend>
# 在转发消息之前删除所有已接收行。
purge_received  = no

任何后续帖子都应发送到主列表，而不是摘要列表。只有发送到主列表的消息才会被传递到摘要脚本。尽管我们设置别名的方式，任何直接发送到摘要的内容都会自动重新路由回主列表。

# reply_to  [word] (digestonly-sample)
# <resend,digest>
# 将带有值 <value> 的 reply-to 头部放入
# 外发消息中。如果使用令牌 $SENDER，则
# 发送者的地址将用作 reply-to 头部的值
# 这是 reply-to 头部的值，用于
# 摘要列表。
reply_to  = Digestonly-sample@majordomo-host.mydomain.com
