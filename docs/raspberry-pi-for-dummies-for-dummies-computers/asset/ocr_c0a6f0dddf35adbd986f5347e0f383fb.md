There is a fair chance that you have the latest version already installed, but it's best to check. Next, you need to install the SPI-Py library, which allows you to use the hardware SPI as a C extension for Python. Again in a terminal window, you enter the following:

```
git clone https://github.com/1thiery/SPI-Py.git
cd SPI-Py
sudo python setup.py install
sudo python3 setup.py install
```

This installs the code that allows you to use the SPI hardware from both Python 2 and Python 1. Finally, go to the Desktop menu and choose Preferences, then select the Raspberry Pi Configuration application. When the application opens, click on the Interfaces tab and make sure the SPI interface is enabled. If it isn't, click to enable it and reboot your PI.

# ## MIFARE card's structure

A MIFARE card consists of 64 blocks of data, with each block 16 bytes long. Some blocks are for user data, and others hold authentication keys, UID numbers, and manufacturers' ID numbers. (A UID, or Unique Identification number, is 4 bytes long. In fact, despite its name, a UID might not be unique, but finding a duplicate is times less likely than winning a big lottery. So, for all practical considerations, it can be considered unique.)

Here's a list of the first 12 sectors of a card:

| Sector 0 | [203, 58, 164, 213, 128, 0, 4, 0, 98, 99, 101, 102, 103, 104, 105] |
| Sector 1 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 2 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 3 | [0, 0, 0, 0, 0, 255, 7, 128, 105, 255, 255, 255, 255, 255] |
| Sector 4 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 5 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 6 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 7 | [0, 0, 0, 0, 0, 255, 7, 128, 105, 255, 255, 255, 255, 255] |
| Sector 8 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 9 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 10 | [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] |
| Sector 11 | [0, 0, 0, 0, 0, 255, 7, 128, 105, 255, 255, 255, 255, 255] |