
### 附录 B：监控软件的 C 语言编程

```c
    DevCount=0; // 设置在第一行写入描述

    DateCamp = tblock->tm_mday;

}
```

```c

**********************************************

//retstrcp(DateCamp,dir);

// 尝试在第一行写入数据描述

if(DateCamp != tblock->tm_mday)

{

    DevCount++;

    DateCamp = tblock->tm_mday; // 仅用于下次比较

    fopen(dir,"a"); // 在此处向文件写入数据描述

    out_file = fopen(out_file,"NULL");

    if (out_file == NULL)

    {

        printf("打开文件失败 \n"); // 测试

    }

    else

        fprintf(out_file,"%s", "");

    for(i=0;i<ChanCount;i++){

        GetChannelName(ChanHandle[i],ChanName, 200);

        fprintf(out_file,"%20s", ChanName); // 存储数据的描述

    }

    fprintf(out_file,"\n");

}

```

```c

fclose(out_file);

}

i=0;

while(isalpha(TimeDate[i])!=0 || (TimeDate[i]== 0x20)) {

    // 只需要日期和月份

    {

        i++;

        TimeDate[i]='0';

        /********* 写入数据的读取时间 *********/

        sprintf(DataTime,"%s%%02d/%s%%02d,%s%%02d,%s%%02d", TimeDate, tblock->tm_mday, tblock->tm_mon+1, tblock->tm_year+1900, tblock->tm_hour, tblock->tm_min, tblock->tm_sec);

    }

/**/

i=0;

while(TimeDate[i]!='\n') // 去除计时器中的 '\n'

    i++;

TimeDate[i]='0';

/******* // 尝试将数据写入文件

out_file = fopen(dir,"w");

out_file2 = fopen("status/sunny_status.txt","w");

out_file3 = fopen("status/monitor_body.txt","w");

if (out_file == NULL || (out_file2==NULL)) {

    printf("打开文件失败 \n"); // 测试

} else {

    fprintf(out_file,"%s", DataTime); // 存储时间

    for(i=0;i<ChanCount;i++) {

        GetChannelName(ChanHandle[i],ChanName, 200);

        if(SunnySleep<=100)

            /***** 夜间读取数据无响应结果为零 *****/

            /* 获取通道值... */

            res = GetChannelValue(ChanHandle[i], DevHandle,&Value, 30, MaxValue);

            if(res==0) {

                /* 状态文本？*/

                if(strlen(Value)==0)

                    printf("%f", Value);

            } else {

                if(ChanMask & CH_PARA) {

                    if (out_file2 != NULL)

                        fprintf(out_file2,"读取通道失败\n...代码=%d\n",res);

                }

                printf("读取通道失败\n...代码=%d\n",res);

                break;

            }

            strcpy(Value,"<unknown>");

            strcpy(Value,"0.00000"); // 这里不行，数据为零

            SunnySleep=100;

            fprintf(out_file2,"* Sunny 休眠\n");

        }

}

```

```c

if (SunnySleep==100)

    strcpy(TextValue,"0.00000"); // 如果不行，数据为零

printf("%d |%16s |%s\n", ChanHandle[i], ChanName, TextValue);

fprintf(out_file,"%20s", TextValue);// 放入文件

/* 想要在网页首页显示的值 */

if((strcmp(ChanName,"Up")) || !strcmp(ChanName,"Iac")) || !strcmp(ChanName,"Uac")) || !strcmp(ChanName,"Pac")) || !strcmp(ChanName,"Pac")) || !strcmp(ChanName,"Fehler)))

{

    fprintf(out_file,"%15s", TextValue);// 用于网页首页监控

    if((strcmp(ChanName,"Ubat")) || !strcmp(ChanName,"Ibat)))

    if (Check==1)

    {

        out_file=4;

        fopen("status/monitor.txt","w"); // 打开文件

        Check = 1;

    }

    fprintf(out_file,"%15s", TextValue);// 用于网页首页监控

}

/* 想要在网页首页显示的值 */

if (ChanHandle[i]==54 || ChanHandle[i]==59 || ChanHandle[i]==60 || ChanHandle[i]==56 || ChanHandle[i]==69 || ChanHandle[i]==74 || ChanHandle[i]==80)

    fprintf(out_file,"%15s", TextValue);// 用于监控

}

fprintf(out_file,"\n");

fprintf(out_file3,"\n");

if (Check==1)

{

    fprintf(out_file4,"\n");

    fclose(out_file4);

}

if (SunnySleep !=100)

    fprintf(out_file2,"Sunny 良好\n");

fclose(out_file);

fclose(out_file2);

fclose(out_file3);

}

else // 这里是 SMA 的操作

if (ChMask==0x04f)

/* // 将参数也存储到文件

{

    fprintf(dir,"%s%%%s", "show_parameter", DevHandle, ".txt");

    out_file=fopen(dir,"w");

    if(out_file==NULL)

    {

        printf("打开文件失败 \n"); // 测试

    }

    for(i=0;i<ChNameCount;i++)

{

    GetChannelName(ChanHandle[i],ChanName, 200);

    if(SunnySleep !=100)

    /* 获取通道值... */

        res = GetChannelValue(ChanHandle[i], DevHandle, &Value, 30, MaxValue);

    }

}

```

```c

if(res==0)

{

    /* 状态文本？*/

    if(strlen(TextValue)==0)

        printf(TextValue,"%f", Value);

}

else

{

    if (ChanMask & CH_PARA)

    {

        /* if (ChanMask==0x04f)

            if (out_file != NULL)

                fprintf(out_file,"读取通道值失败...代码=%d\n",res);

        */

        printf("读取通道值失败...代码=%d\n",res);

        break;

    }

    strcpy(TextValue,"<unknown>");

    SunnySleep=100;

    /*if(ChMask==0x04f)

    {

        if (out_file != NULL)

    }

    fprintf(out_file,"读取失败。Sunny 未响应\n");

    */}

/* if (SunnySleep==100)

{

    strcpy(TextValue,"<unknown>");

*/

if ((ChanMask==0x04f) && (out_file != NULL) && (SunnySleep !=100)

    fprintf(out_file,"%15s", TextValue);

else

    printf("%d |%16s |%s\n", ChanHandle[i], ChanName, TextValue);

}

fclose(out_file);

}

```

```c

************************************************

描述：打印设备列表

************************************************

void PrintDevList()

{

    int i;

    DWORD DevHandles[10];

    char NameBuffer[200];

    DWORD DevCount=0;

    printf("--------------------------------------\n");

    printf("设备句柄 | 设备名称 \n");

    printf("--------------------------------------\n");

    for(i=0;i<DevCount;i++)

    {

        GetDeviceName(DevHandles[i], NameBuffer, 200);

        printf("%ld | %s\n", DevHandles[i], NameBuffer);

    }

}

```

```c

************************************************

描述：打印通道的所有状态文本

************************************************

void printStatTexts (DWORD ChanHandle)

{

    int i;

    int TxtCnt = GetChannelStatCnt (ChanHandle);

    if (TxtCnt)

    {

        printf("该通道的所有状态文本：\n");

        for (i=0;i<TxtCnt;i++)

        {

            char StatText[30];

            GetChannelStat(ChanHandle, StatText, sizeof(StatText)-1);

            printf("%2d: %s\n", i, StatText);

        }

    }

}

```

```c

************************************************

描述：设置通道值

************************************************

void SetParamValue(void)

{

    char Device[5],value[50]={};

    DWORD ChanHandle,DevHandle;

    double ChanValue;

    int iResult,dev,check=0;

    FILE *in_file,*out_file_res;

    printf("写入参数：n\n");

    printf("设备句柄： "); scanf("%ld", &DevHandle);

    in_file=fopen("status/device.txt","r"); // 从文件读取设备

    fgets(Device,5,in_file);

    fclose(in_file);

    sscanf(Device,"i=%ld", &DevHandle);//拷贝数据并转换为整数

    DevHandle=i; // 手动设置

    printf("通道句柄： "); scanf("%ld", &ChanHandle);

    in_file=fopen("status/parameters.txt","r"); // 读取参数

    if(in_file == NULL)

    {

        printf("打开文件失败 \n");

    }

    else

    {

        out_file_res = fopen("status/result_set.txt","w"); // 将结果写入文件

        if (out_file_res == NULL)

            printf("打开文件失败 \n"); // 测试

    }

}

```

```c

else

{

    while (fgets(value, 4, in_file) != NULL && (check(100))) // 从文件获取 chan

        printf("%s ", read_data);//// 测试

        {

            sscanf(value, "%ld", &ChanHandle);

            printf("File:%ld", ChanHandle); // 测试

            printStatStats(ChanHandle); // 如果有错误则打印状态！

            printf("New channel: %s"); scanf("%s", value);

            sscanf(value, "%lf", &ChanValue); // 转换为浮点

            fgets(value, 20, in_file); // 我们也检查文件末尾

            sscanf(value, "%lf", &ChanValue);

            i=0;

            while (value[i] != 0x20) // 去除 value 中的空格

            {

                i++;

            }

            dev=1;

            while (value[i] != '0') // 复制

                value[i-dev]=value[i];

                i++;

        }

        /* 用户输入的是文本还是数值？ ?*/

        if (value[0] > '9' || value[0] < '0')

        {

            // 插入文本，查找该值的状态文本索引

            int TCnt = GetChannelStatCnt( ChanHandle);

            int i;

            ChanValue = -1;

            for(i=0;i<TxtCnt;i++)

            {

                char StatText[30];

                strcpy(StatText, GetChannelStatText(ChanHandle, i));

                GetChannelStatText(ChanHandle, StatText, sizeof(StatText)-1);

                Trim(StatText, strlen(StatText));
```
