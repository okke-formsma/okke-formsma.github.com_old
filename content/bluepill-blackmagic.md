Title: Blackmagic on a bluepill
Date: 2020-06-30
Categories: 

To flash [nrfmicro](https://github.com/joric/nrfmicro/wiki) chips, you can use a bluepill with blackmagic installed.

The bluepill has some issues with wrong resistors (I had to change R3 on the bluepill from 100k to 10k ohm). 
The blackpill with stm32f103 processor does not have this problem, and is recommended. (Black Magic is not supported on blackpill 1.2 (stm32f401) or blackpill 2.0 (stm32f411) at this time.

There's an excellent article on [flashing blackmagic firmware onto a bluepill](https://github.com/joric/nrfmicro/wiki/Software) by joric. 
Here are some the steps I went through to make it work on ubuntu.

- Connect the usb-to-uart converter to the bluemicro and set the bluemicro boot0 jumper to 1. 

- Find the usb port that the converter is attached to
``` 
> dmesg | grep tty
[157210.247340] cp210x ttyUSB0: cp210x converter now disconnected from ttyUSB0
[157221.140041] usb 1-2: cp210x converter now attached to ttyUSB0
```

- Install the dfu. Run stm32loader.py on python2 with the pySerial package installed:
```
python2 stm32loader.py -p /dev/ttyUSB0 -ewv blackmagic_dfu.bin
```

- Install the blackmagic firmware:
```
stm32flash -w blackmagic.bin /dev/ttyUSB0 -S 0x08002000
```

- Set the jumper back to 0, disconnect the uart adapter, connect the bluepill to usb.
- Check if the blackmagic probe is recognized with `lsusb`.