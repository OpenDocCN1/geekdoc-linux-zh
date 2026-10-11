
```c
120:       if (!*src) {
121:         printf(stderr, "character expected after \n");
122:         freeJob(job);
123:         return 1;
124:       }
125:     }
126:   } /* 在 shell 中,' 产生 */
127:   if (*src != quote) buf++ = '\';
128: }
129:   *buf++ = *src;
130: else if (isspace(*src)) {
131:     if (prog->argv]) {
132:       buf++, argc++;
133:       /* 为结束 argv 的 NULL 留位置 */
134:       if ((argc + 1) == argvAllocated) {
135:           argvAllocated += 5;
136:           prog->argv = realloc(prog->argv, argvAllocated);
137:       }
138:       prog->argv[argc] = buf;
139:     }
140:   else switch (*src) {
141:     case '\'': 
142:     case '\'': 
143:       quote = *src;
144:       break;
145:     case '#': /* 注释 */
146:       done = 1;
147:       break;
148:     case '&'; /* 后台 */
149:       *isBg = 1;
150:     case ':': /* 多命令 */
151:       done = 1;
152:       returnCommand = *commandPtr + (src - *commandPtr) + 1;
153:       break;
154:     case '\'': 
155:       src = *src;
156:       if (!*src) {
157:         freeJob(job);
158:         fprintf(stderr, "character expected after \n");
159:         return 1;
160:       } /* 透穿 */
161:       default:
162:         *buf++ = *src;
163:   }
164:   src++;
165:   )
166:   if (*prog->argv[argc]) {
167:     argc++;
168:   if (!argc) {
169:     freeJob(job);
170:     return 0;
171:   }
172:   prog->argv[argc] = NULL;
173: 
174:   if (!returnCommand) {
175:     job->text = malloc(strlen(commandPtr) + 1);
176:     strcpy(job->text, commandPtr);
177:   } else {
178:     /* 这留下了末尾空格，有点粗略 */
179:     count = returnCommand - commandPtr;
180:     job->text = malloc(count + 1);
181:     strcpy(job->text, commandPtr, count);
182:     job->text[count] = '\0';
183:   }
184: 
185:   *commandPtr = returnCommand;
186: 
187:   return 0;
188:   )
189:  int runCommand(struct job newJob, struct jobSet * jobList, int inbg) {
190:    struct job *job;
191: 
192:    /* 在这里处理内置命令——我们不 fork(0)，所以不能在早期
193:       后台运行 */
194:    if (strcmp(newJob.progs[0], "exit")) {
195:      /* 这应该返回真正的退出码 */
196:      exit(0);
197:    } else if (strcmp(newJob.progs[0], "jobs")) {
198:      for (job = jobList->head; job; job = job->next)
199:        printf(JOB_STATUS_FORMAT, job->jobid, "Running");
200:    }
201:   job->text);
202:   return 0;
203:   /* 我们现在每个子进程有一个程序，所以这很简单 */
204:   if (!(newJob.progs[0].pid = fork())) {
205:     execvp(newJob.progs[0].argv, newJob.progs[0].argv);
206:     fprintf(stderr, "exec of %s failed: %s\n", newJob.progs[0].argv[0], strerror(errno));
207:   }
208:   /* 将我们的子进程放入自己的进程组 */
209:   setpgid(Job.progs[0].pid, newJob.progs[0].pid);
210:   newJob.pgrp = newJob.progs[0].pid;
211:   /* 查找作业使用的 ID */
212:   newJob.jobid = 1;
213:   for (job = jobList->head; job; job = job->next) {
214:     if (job->jobid >= newJob.jobid) {
215:         newJob.jobid = job->jobid + 1;
216:     }
217:   } /* 将作业添加到运行列表 */
218:   if (jobList->head) {
219:     job = jobList->head = malloc(sizeof(*job));
220:   } else {
221:     for (job = jobList->head; job->next; job = job->next) {
222:         job->next = malloc(sizeof(*job));
223:         job = job->next;
224:     }
225:   *job = newJob;
226:   job->next = NULL;
227:   job->runningProgs = job->numProgs;
228: 
229:   if (inBg) {
230:      /* 我们不等待后台作业返回——将其添加到
231:         后台作业列表并置不管它 */
232:   }
233:   }
234: }
235: }
```

## 132 第 9 章 进程模型

```c
252:
253:\    printf("%d %d\n", job->jobid,
254:\        newJob.progs[newJob.numProgs - 1].pid);
255:
} else {
256:
    JobList->fg = job;
    /* 将新的进程组移前台 */
    if (tcsetpgrp(0, newJob.pgid))
        perror("tcsetpgrp");
}
    return 0;
```
```c
void removeJob(struct jobSet * jobList, struct job * job) {
    struct job *prevJob;
    freeJob(job);
    if (job == jobList->head) {
        jobList->head = job->next;
    } else {
        prevJob = jobList->head;
```
