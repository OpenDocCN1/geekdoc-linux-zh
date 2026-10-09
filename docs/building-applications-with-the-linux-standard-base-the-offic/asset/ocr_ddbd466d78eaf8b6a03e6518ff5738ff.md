![](bbox=[0.12, 0.12, 0.88, 0.52])

`/opt/whizbang/widgets/bin/` should be added to the end user's `PATH` environment variable.

# ### 4.5.3   Packaging Multiple Product Versions

To simultaneously support multiple versions of same products, they need to be separated into their own respective version subdirectories, such as `/opt/whizbang/widgets/v1/` and `/opt/whizbang/widgets/v2/` as illustrated in Figure 4.5. The system administrator could set up a default v1 or v2 behavior by creating a symbolic link from `/opt/whizbang/widgets/v1/bin/` back to `/opt/whizbang/widgets/bin/` or `/opt/whizbang/widgets/v2/lib/` back to `/opt/whizbang/widgets/lib/` (Example 4.7). In either case, `/opt/whizbang/widgets/bin/` should be added to the end user's `PATH` environment variable.