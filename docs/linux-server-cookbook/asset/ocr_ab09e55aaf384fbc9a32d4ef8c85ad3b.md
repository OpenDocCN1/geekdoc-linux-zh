```
```
"lRepoDigestsInuxservercb/ubuntupache@sha256:58557aced96f8d937178
29e2ba6e418e15ea0992e4c83c8659f6f21cead26381"
],
(omitted)
"Config" : {
(omitted)
"Cmd" : [
"/bin/sh",
"-c",
"/usr/sbin/apache2ctl -D FOREGROUND"
],
"Image":
"sha256:14efd05a5ac026c330095be5c09f8bcfd0b6c82da8dc2853c7aaeaf4e
9c1e19",
},
"Architecture" : "amd64",
"OS" : "linux",
"Size" : 225124187,
"VirtualSize": 225124187,
(omitted)
},
"RootFS" : {
"Type": "layers",
"Layers": [
"sha256:7ea4455e747ead87d6cc1c4efaf3a79530a931a0856a9f9ce9ac2d8
d45bd3c28",
"sha256: bcebbf94eb56506a9f1f6bc38f5a6bbf1fc74d03af0cb44eb137ad6
e107279fa",
"sha256:0ff7c267b89e80ad4571a737758fa48f57a80cbddc52351bbab565c
70b875c77",
"sha256:ddf9698d2d70c418c2abe60746ff92b58dffdd16fa68d3fd4cdca
9366c5a85"
]
},
(omitted)
}
]```

```

There is the possibility to run a private **Image Registry**, to not publish globally the images generated. This is usually required for enterprises with custom applications