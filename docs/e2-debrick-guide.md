## Intro

Built in firmware update function writes app (SYSTEM.VSB[0x100:]) to flash.

SYSTEM.VSB has 0x100 byte header, remaining 0x200000 is the application.

Secondary Bootloader (SBL) loaded to on-chip RAM at 0x80000000.

App loaded to external RAM at 0xc0000000.

<br/>

## RPi and OpenOCD

### Install and Setup

Install OpenOCD and connect RPi GPIO to e2 CPU JTAG  Header (J9).
		
**RPi / OpenOCD:**

* https://iosoft.blog/2019/01/28/raspberry-pi-openocd
* https://learn.adafruit.com/programming-microcontrollers-using-openocd-on-raspberry-pi/overview
		
**e2 J9:**
* https://4.bp.blogspot.com/-kc4eZ1IID-k/VcfOYaU08aI/AAAAAAAAAqk/2kCErwdJcXc/s1600/IMG_9288.JPG
		
**Config files:**
* https://github.com/bangcorrupt/hacktribe/tree/master/openocd

<br/>

### Prepare SD Card

Prepare SD card with SYSTEM.VSB at correct path for device.

_(Ensure SYSTEM.VSB is correct firmware for device as it was from the factory)._
	
**Factory Synth (e2, grey or blue):**

`KORG/electribe/System/SYSTEM.VSB`
		

**Factory Sampler (e2s, black or red):**

`KORG/'electribe sampler'/System/SYSTEM.VSB`
		
<br/>

### Halt Processor

Halt processor in bootloader (0x80nnnnnn), before hand off to app (0xc0000000).

I haven't figured out resetting the CPU via JTAG.  Halt in the bootloader before handing off to the app by pressing the power button at the same time as (or very slightly after) executing the openocd command.  Processor will halt when openocd connects.
		
Output from openocd command will show the address halted at.  

* If it begins with 0x8 we're in on-chip RAM in the bootloader (good).

* If it begins with 0xc we're in external RAM in the app (try again).

<br/>

### Connect to server

Connect to the telnet server provided by OpenOCD.

Set a breakpoint at 0xc0000000 and continue.
	
At breakpoint, load bytes from SYSTEM.VSB[0x100:] to 0xc0000000, then continue.

<br/>

### Write Firmware	

Once booted, use built in firmware update function to write firmware to flash.

<br/>

## RPi and FlashROM

Couldn't get clean write using cheap connectors.

Test again using Pomona 5250.
