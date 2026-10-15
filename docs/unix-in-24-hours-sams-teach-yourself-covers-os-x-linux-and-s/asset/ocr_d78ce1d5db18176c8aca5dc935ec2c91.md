```
{ sum += $4 }
END { mb = sum / 1024
    gb = mb / 1024
    printf "%.0f MB (%.2fGB) of available disk space\n", mb, gb
}
```