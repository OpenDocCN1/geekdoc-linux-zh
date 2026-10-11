```
1167 down(&dir->d_inode->i_sem);
1168 return dir;
1169 }
1170
1171 static inline struct entry \*get\_parent(struct entry \*dentry)
1172 {
1173 return dget (dentry->d\_parent);
1174 }
1175
1176 static inline void unlock\_dir(struct dentry \*dir)
1177 {
1178 up(&dir->d\_inode->i\_sem);
1179 dput(dir);
1180 }
1181
1182 \*/
1183 \* Whee.. Deadlock country. Happily there are only two VFS
1184 \* operations that does this..
1185 \*/
1186 static inline void double\_down(struct semaphore \*s1, struct semaphore \*s2)
1187 {
1188 if (s1 != s2) {
1189 if ((unsigned long) s1 < (unsigned long) s2) {
1190 struct semaphore \*tmp = s2;
1191 s2 = s1; s1 = tmp;
1192 }
1193 down(s1);
1194 }
1195 down(s2);
1196 }
1197
1198 \*/
1199 \* Ewwwwwwww.. \_triple\_lock. We are guaranteed that the 3rd argument is
1200 \* not equal to 1st and not equal to 2nd - the first case (target is parent of
1201 \* source) would be already caught, the second is plain impossible (target is
1202 \* its own parent and that case would be caught even earlier). Very messy.
1203 \* I \_think\_ that it works, but no warranties - please, look it through.
1204 \* Pox on bloody lusers who mandated overwriting rename() for directories...
1205 \*/
1206
1207 static inline void triple\_down(struct semaphore \*s1,
1208 struct semaphore \*s2,
1209 struct semaphore \*s3)
1210 {
1211 if (s1 != s2) {
1212 if ((unsigned long) s1 < (unsigned long) s2) {
1213 if ((unsigned long) s1 < (unsigned long) s3) {
1214 struct semaphore \*tmp = s3;
1215 s3 = s1; s1 = tmp;
1216 }
1217 if ((unsigned long) s1 < (unsigned long) s2) {
1218 struct semaphore \*tmp = s2;
```