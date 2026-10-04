```
};
while (i<sz);
};
void decrypt(BYTE *buf, int sz, char *pw) {
    char *p=strdup (pw);
    strrev (p);
    int i=0;
    do {
        memcpy(cube, buf+i, 8*8);
        rotate_all (p, 3);
    memcpy(buf+i, cube, 8*8);
        i+=64;
    } while (i<sz);
    free (p);
};
```

```
void crypt_file(char *fin, char* fout, char *pw) {
    FILE *f;
    int flen, flen_aligned;
    BYTE *buf;
    f=fopen(fin, "rb");
    if (f==NULL) {
        printf("Cannot open input file!\n");
        return;
    }
    fseek(f, 0, SEEK_END);
    flen=ftell(f);
    fseek(f, 0, SEEK_SET);
    flen_aligned=(flen&0xFFFFFFFC)+0x40;
    buf=(BYTE*)malloc(flen_aligned);
    memset(buf, 0, flen_aligned);
    fread (buf, flen, 1, f);
    fclose (f);
```