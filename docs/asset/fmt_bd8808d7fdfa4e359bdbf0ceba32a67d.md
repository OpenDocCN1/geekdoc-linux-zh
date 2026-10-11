
# 第 9 章 进程模型

```c
while (prevJob->next != job) prevJob = prevJob->next;

prevJob->next = job->next;
}

freeJob(job);
}

/* 检查是否有后台进程已退出——它们

确定退出原因并查看作业是否完成 */
void checkJobs(struct jobSet * joblist) {
    struct job * job;
    pid_t childpid;
    int status;
    int progNum;
    while ((childpid = waitpid(-1, &status, WNOHANG)) > 0) {
        for (job = jobList->head; job; job = job->next)
            progNum = 0;
            while (progNum < job->numProgs &&
                   job->progs[progNum].pid != childpid)
                progNum++;
            if (progNum < job->numProgs)
                break;
            job->runningProgs--;
            job->progs[progNum].pid = 0;
            if (!job->runningProgs) {
                printf(JOB_STATUS_FORMAT, jobId, "Done", job->text);
                removeJob(jobList, job);
            }
    }
    if (childpid == -1 && errno != ECHLD) {
        perror("waitpid");
    }
}
```

```c
int main(int argc, char **argv[]) {
    char command[MAX_COMMAND_LEN + 1];
    char * nextCommand = NULL;
    struct jobSet jobList = {NULL, NULL };
    struct jobNext;
    FILE * input = stdin;
    int i;
    int status;
    int inbg;
    if (argc < 2) {
        fprintf(stderr, "unexpected arguments; usage: lavish <commands>\n");
        exit(1);
    } else if (argc == 2) {
        input = fopen(argv[1], "r");
        if (!input) {
            perror("fopen");
            exit(1);
```

```c
    /* 不要忽略这个信号；它只会引起混乱，
    并且实际上就不是为 shell 设计的 */
    signal(SIGTOU, SIG_IGN);
    while (1) {
        if (!jobList.fg) {
            /* 没有作业在前台运行 */
            /* 检查是否有后台进程已退出 */
            checkJobs(&jobList);
            if (!nextCommand) {
                if (getCommand(input, command)) break;
                nextCommand = command;
                if (!parseCommand(&nextCommand, &newJob, &inBg) &&
                    newJob.numProgs)
                    runCommand(newJob, &jobList, inBg);
            } else {
                /* 有作业在前台运行；等待它完成 */
                int i = 0;
                while (jobList.fg->progs[i].pid) {
                    waitpid(jobList.fg->progs[i].pid, &status, 0);
                    jobList.fg->runningProgs--;
                    jobList.fg->progs[i].pid = 0;
                    if (!jobList.fg->runningProgs) {
                        /* 子进程退出 */
                        removeJob(&jobList, jobList.fg);
                        jobList.fg = NULL;
                        /* 将 shell 切回前台 */
                        if (tcsetpgrp(0, getpid()))
                            perror("tcsetpgrp");
                    }
                    i++;
                }
            }
        }
    }
    return 0;
}
```
