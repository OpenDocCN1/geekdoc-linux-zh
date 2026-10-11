# BUILD A COMPLEX LED MATRIX

![](bbox=[0.115, 0.125, 0.445, 0.44])

Above This is the full schematic of the LED matrix that we're working with here (you can also view it at its full size on FileSilio).

# Full code listing

```
```
{
    _where->writePinLow(PIND7);
}
```

```cpp
int main(void)
{
    rtmpGpio_rpiGpio;
    // Set outputs
    rtmpGpio_setPinDir(PINA0, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PINA1, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PINA2, rtmpGpio::OUTPUT);
    // Data out RS491
    rtmpGpio_setPinDir(PINCS0, rtmpGpio::OUTPUT);
    rtmpGpio_writePinHigh(PINCS0);
    // Data out RS491
    rtmpGpio_setPinDir(PINCS1, rtmpGpio::OUTPUT);
    rtmpGpio_writePinHigh(PINCS1);
    rtmpGpio_setPinDir(PIND0, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND1, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND2, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND3, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND4, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND5, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND6, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND7, rtmpGpio::OUTPUT);
```

```cpp
unsigned char dataStore[2][16];
```

```cpp
for(int j=0; j<2; j++)
{
    for(int k=0; k<16; k++)
    {
        dataStore[j][k] = 64;
    }
}
```

```cpp
int blockCounter = 0;
int rowCounter = 0;
while(1)
{
    blockCounter++;
    if (blockCounter == 16)
    {
        if (rowCounter == 0)
        {
            blockCounter = 0;
            rowCounter = 1;
        }
        else
        {
            blockCounter = 0;
            rowCounter = 0;
        }
    }
```

```cpp
safelySetRow(rowCounter, &rpiGpio);
setAddress(blockCounter, &rpiGpio);
setData(dataStore[rowCounter][blockCounter], &rpiGpio);
usleep(50);
}
return 0;
```

```

# 11  Energy control

LEDs light up if current flows through them. SetData pulls the pins of the 74HC244 low to ensure that the energy supplied from the 74HC238 can flow through the diode.

# 12  Avoid GPIO trouble

The Raspberry Pi Foundation has a tendency to change the layout of the expansion header regularly, a habit which professional manufacturers of process computers abhor. It's recommended to handle the mapping between pins and functions via a set of defines. Our code is optimised for a Rev2 Raspberry Pi with a 'short' header - 40-pin variants will require readjustments making sure the physical pin numbers correspond to the logical GPIO numbers.

# 13  Add example data

Test the code by setting the datastore to a value of your choice. Setting 64 to all fields will disable one row in each part of the display.

# 14  Kick it off

Check all connections between the planar and the single-board computer, and proceed to starting the compiled app. Don't forget to use the sudo command - direct memory access is restricted to root in order to prevent apps from causing havoc in the physical memory. Users are accustomed to this, so requiring them to put a sudo in front of the command doesn't cause concern.

# 15  Notice a flicker

Sharp-eyed readers will notice an occasional flicker where one line appears brighter than the others. This is caused by the stalling of the program - if the kernel does other work, the switching routine can't run. We could solve this problem by using a real-time Linux kernel.