# 204 CHAPTER 5 Embedded Heterogeneous Programming with OpenCL

```
char *program_source,*log;
size_t file_size, program_size;
const char options[50] = "-cl-fast-relaxed-math\0";nsize_t log_length = 0, return_size;
    work_item_sizes[3], max_wg_size[3];
```

Example Code:

```
myFile = fopen("horner.cl", "r+");

if (!myFile) {
    perror("Cannot open kernel source file");
    exit(0);
}

fseek(myFile,0,SEEK_END);
file_size = ftell(myFile);
fseek(myFile,0,SEEK_SET);
program_source=(unsigned char*)malloc(file_size+1);
fread(void*)program_source,1,file_size,myFile);
program = clCreateProgramWithSource(context,1,
    &program_source,0,&ret);

CHECK_STATUS(ret);
ret = clBuildProgram(program, 0, 0, options, 0, 0);
fclose(myFile);
program_source[program_size]=0;
if(ret==CL_BUILD_PROGRAM_FAILURE) {
    ret=clGetProgramBuildinfo(program,
        device,CL_PROGRAM_BUILD_LOG,
        0,0,&log_length);
}

CHECK_STATUS(ret);
log=(char*)malloc(log_length));
```