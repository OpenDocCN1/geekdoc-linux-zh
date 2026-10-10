# ## CONFIGURATION

You can specify extra mail header lines to be added to each message, defaults for the subject prefix and file suffix, number patches when outputting more than one patch, add "To" or "Cc:" headers, configure attachments, and sign off patches with configuration variables.

```
[format] headers = "Organization: git-foo\n" subjectPrefix = CHANGE suffix = .txt numbered = auto to = <email> cc = <email> attach [ = mime-boundary-string ] signOff = true coverletter = auto
```