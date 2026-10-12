
其他别名可能永远不会被使用。它们是为了完整性和作为安全网而包含的。

要使用摘要，必须创建额外的目录：

/usr/local/majordomo/digests/listname-digest/

在我们的例子中，该目录名为 digestonly-sample-digest/。此外，还必须在 /usr/local/majordomo/digests/ 中创建一些可选文件，在我们的例子中将分别命名为 digestonly-sample-digest.header 和 digestonly-sample-digest.trailer。这些文件包含在生成摘要时要添加到每个摘要前后的文本。所有文件和目录都应由用户 majordomo 拥有并可写入。

> **注意**
> 
> 邮件列表的密码可以明文写在配置文件中，也可以存储在单独的文件中。文档对于应该放在哪里并没有说得很清楚。

以下是主列表的配置文件。这是一个开放的、未经审核的列表。其成员列表不会直接使用，而是由子摘要列表获取。文件相当长，大多是样板内容。你可能只想更改密码以及其他安全和隐私相关项目。

```
# The configuration file for a majordomo mailing list.
# Comments start with the first # on a line, and continue to the
# end of the line. There is no way to escape the # character.
# The file uses either a key = value for simple (i.e. a single)
# values, or uses a here document
# key << END
# value 1
# value 2
# [ more values 1 per line]
# END
# for installing multiple values in array types. Note that the
# here document delimiter (END in the example above) must be the
# same at the end of the list of entries as it is after the <<
# characters.
# Within a here document, the # sign is NOT a comment character.
# A blank line is allowed only as the last line in the here
# document.
#
# The values can have multiple forms:
#
# absolute_dir -- A root anchored (i.e. begins with a /)
# directory
# absolute_file -- A root anchored (i.e. begins with a /) file
# bool -- choose from: yes, no, y, n
# enum -- One of a list of possible values
# integer -- an integer (string made up of the digits 0-9,
# no decimal point)
# float -- a floating point number with decimal point.
# regexp -- A perl style regular expression with
# leading and trailing '/s.
# restrict_post -- a series of space or : separated file
# names in which to look up the sender's address
# (restrict-post should go away to be replaced by
# an array of files)
# string -- any text up until a \n stripped of
# leading and trailing whitespace
# word -- any text with no embedded whitespace
#
# A blank value is also accepted, and will undefine the
# corresponding keyword.
# The character Control-A may not be used in the file.
#
# A trailing _array on any of the above types means that that
# keyword will allow more than one value.
#
# Within a here document for a string_array, the '..' sign takes
# on a special significance.
#
# To embed a blank line in the here document, put a '..' as
# the first and ONLY character on the line.
#
# To preserve whitespace at the beginning of a line, put a .
# on the line before the whitespace to be preserved
#
# To put a literal '..' at the beginning of a line, double
# it.
#
# The default if the keyword is not supplied is given in ()'s
# while the type of value is given in [], the subsystem the
# keyword is used in is listed in <>'s. (undef) as default value
# means that the keyword is not defined or used.

# admin_passwd    [word] (digestonly-sample.admin)
# <majordomo>
# (Default is specified in the file <listname>.passwd) The
# password for handling administrative tasks on the list.
admin_passwd    = mypassword

# administrivia   [bool] (yes) <resend>
# Look for administrative requests (e.g.
# subscribe/unsubscribe) and
# forward them to the list maintainer instead of the list.
administrivia   = yes

# advertise       [regexp_array] (undef) <majordomo>
# If the requestor email address matches one of these
# regexps, then the list will be listed in the output of a
# lists command. Failure to match any regexp excludes the
# list from the output. The regexps
# under noadvertise override these regexps.
advertise       << END

END

# approve_passwd  [word] (digestonly-sample.pass)
# <resend>
# Password to be used in the approved header to allow
# posting to moderated list, or to bypass resend checks.
approve_passwd  = digestonly-sample.passwd

# archive_dir     [absolute_dir] (undef) <majordomo>
# The directory where the mailing list archive is kept.
# This item does not currently work. Leave it blank.
archive_dir     =

# comments        [string_array] (undef) <config>
# Comment string that will be retained across config file
# rewrites.
comments        << END

END

# date_info        [bool] (yes) <majordomo>
# Put the last updated date for the info file at the top of
# the info file rather than having it appended with an info
# command. This is useful if the file is being looked at by
# some means other than majordomo (e.g. finger).
date_info     =  yes

# debug        [bool] (no) <resend>
# Don't actually forward message, just go through the
# motions.
debug     =  no

# description    [string] (undef) <majordomo>
# Used as description for mailing list when replying to the
# lists command. There is no quoting mechanism, and there
# is only room for 50 or so characters.
description   ="Sample digest-only list"

# digest_archive [absolute_dir] (undef) <digest>
# The directory where the digest archive is kept. This item
# does not currently work. Leave it blank.
digest_archive =

# digest_issue   [integer] (1) <digest>
# The issue number of the next issue
digest_issue   = 1

# digest_name    [string] (digestonly-sample) <digest>
# The subject line for the digest. This string has the
# volume and issue appended to it.
digest_name   =  digestonly-sample

# digest_rm_footer [word] (undef) <digest>
# The value is the name of the list that applies the header
# and footers to the messages that are received by digest.
# This allows the list supplied headers and footers to be
# stripped before the messages are included in the digest.
# This keyword is currently non operative.
digest_rm_footer =

# digest_rm_fronter [word] (undef) <digest>
# Works just like digest_rm_footer, except it removes the
# front material. Just like digest_rm_footer, it is also
# non-operative.
digest_rm_fronter =

# digest_volume    [integer] (1) <digest>
# The current volume number
digest_volume  = 1

# digest_work_dir  [absolute_dir] (undef) <digest>
# The directory used as scratch space for digest. Don't
# change this unless you know what you are doing
digest_work_dir =

# maxlength        [integer] (40000) <resend,digest>
# The maximum size of an unapproved message in characters.
# When used with digest, a new digest will be automatically
# generated if the size of the digest exceeds this number
# of characters.
maxlength       = 40000

# message_footer   [string_array] (undef) <resend,digest>
# Text to be appended at the end of all messages posted to
# the list. The text is expanded before being used. The
# following expansion tokens are defined: $LIST - the name
# of the current list, $SENDER the sender as taken from
# the from line, $VERSION, the version of majordomo. If
# used in a digest, no expansion tokens are provided
message_footer  << END

END

# message_fronter  [string_array] (undef) <resend,digest>
# Text to be prepended to the beginning of all messages
# posted to the list. The text is expanded before being
# used. The following expansion tokens are defined: $LIST -
# the name of the current list, $SENDER - the sender as
# taken from the from line, $VERSION, the version of
# majordomo. If used in a digest, only the expansion token
# $SUBJECTS is available, and it expands to the list of
# message subjects in the digest
message_fronter << END

END

# message_headers   [string_array] (undef) <resend,digest>
# These headers will be appended to the headers of the
# posted message. The text is expanded before being used.
# The following expansion tokens are defined: $LIST the
# name of the current list, $SENDER - the sender as taken
# from the from line, $VERSION, the version of majordomo.
message_headers  << END

END

# moderate          [bool] (no) <resend>
# If yes, all postings to the list  must be approved by the
# moderator.
moderate          =  no

# mungedomain       [bool] (no) <majordomo>
# If set to yes, a different method is used to determine a
# matching address. When set to yes, addresses of the form
# user@domain.ain.com are considered equivalent to addresses
# of the form user@ain.com. This allows a user to subscribe
# to a list using the domain address rather than the
# address assigned to a particular machine in the
# domain. This keyword affects the interpretation of
# addresses for subscribe, unsubscribe, and all private
# options.
mungedomain       =  no

# noadvertise       [regex_array] (undef) <majordomo>
# If the requestor name matches one of these regexps, then
# the list will not be listed in the output of a lists
# command. Noadvertise overrides advertise.
noadvertise       << END

END

# precedence        [word] (bulk) <resend,digest>
# Put a precedence header with value <value> into the
# outgoing message.
precedence        =  bulk

# private_get       [bool] (yes) <majordomo>
# If set to yes, then the requestor must be on the mailing
```
