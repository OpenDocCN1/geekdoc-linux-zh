# Build a complex LED matrix

![](bbox=[0.06, 0.12, 0.42, 0.47])

Above This is the full schematic of the LED matrix that we're working with here; you can also view it at its full size on FileSilo

# 11 Energy control

LEDs light up if current flows through them. SetData pulls the pins of the 74HC244 low to ensure that the energy supplied from the 74HC238 can flow through the diode.

# 12 Avoid GPIO trouble

The Raspberry Pi Foundation has a tendency to change the layout of the expansion header regularly, a habit which professional manufacturers of process computers abhor. It's recommended to handle the mapping between pins and functions via a set of defines. Our code is optimised for a Rev2 Raspberry Pi with a 'short' header - 40-pin variants will require readjustments making sure the physical pin numbers correspond to the logical GPIO numbers.

# 13 Add example data

Test the code by setting the dataStore to a value of your choice. Setting 64 to all fields will disable one row in each part of the display.

# 14 Kick it off

Check all connections between the planar and the single-board computer, and proceed to starting the compiled app. Don't forget to use the sudo command - direct memory access is restricted to root in order to prevent apps from causing havoc in the physical memory. Users are accustomed to this, so requiring them to put a sudo in front of the command doesn't cause concern.

# 15 Notice a flicker

Sharp-eyed readers will notice an occasional flicker where one line appears brighter than the others. This is caused by the stalling of the program - if the kernel does other work, the switching routine can't run. We could solve this problem by using a real-time Linux kernel.

# Full code listing

```
{
            _where->writePinLow(PIND7);
        }
    }

    int main(void)
    {
        mmapGpio rpiGpio;
        //Set outputs
        rpiGpio.setPinDir(PINA0,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PINA1,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PINA2,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PINA3,mmapGpio::OUTPUT);
        //TURN OFF ASAP!
        rpiGpio.setPinDir(PINCS0,mmapGpio::OUTPUT);
        rpiGpio.writePinHigh(PINCS0);
        //TURN ON ASAP!
        rpiGpio.setPinDir(PINCS1,mmapGpio::OUTPUT);
        rpiGpio.writePinHigh(PINCS1);
        rpiGpio.setPinDir(PIND0,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND1,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND2,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND3,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND4,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND5,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND6,mmapGpio::OUTPUT);
        rpiGpio.setPinDir(PIND7,mmapGpio::OUTPUT);

        unsigned char dataStore[2][16];

        for(int j=0;j<2;j++)
        {
            for(int k=0;k<16;k++)
            {
                dataStore[j][k]=64;
            }
        }

        int blockCounter=0;
        int rowCounter=0;
        while(1)
        {
            blockCounter++;
            if(blockCounter==16)
            {
                if(rowCounter==0)
                {
                    blockCounter=0;
                    rowCounter=1;
                }
                else
                {
                    blockCounter=0;
                    rowCounter=0;
                }
            }

            safelySetRow(rowCounter, &rpiGpio);
            setAddress(blockCounter, &rpiGpio);
            setData(dataStore[rowCounter][blockCounter], &rpiGpio);
            usleep(50);

        }
        return 0;
    }
```