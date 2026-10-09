# View Files and Directories in a Tree Format

```
$ tree
$ tree -d
$ tree -L number
```

The **tree** command displays files and directories in a tree like format. If you only want to see the directory structure, use the -d option. To limit the depth of the tree, use the -L option followed by a number.

```
$ tree Music/
Music/
└── jazz
    ├── giant-steps.mp3
    │
    ├── jazz-album-1.mp3
    │
    └── john-coletrene.mp3

1 directory, 3 files

$ tree -d Music/
Music/
└── jazz

1 directory

$ tree -d /var | head
/var
├── account
├── cache
│
└── fontconfig
    |
    └── gdm
        |
        ├── adminuser
        |
        └── jason
```