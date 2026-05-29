
# Atlas Copco Elektronikon Mk5 Touchscreen Protocol Emulation

Modern devices today are so reliant on touchscreens. We even have cars where almost all of their crucial function buttons are in the touchscreen infotainment system. Industrial machines are not an exception either; the Atlas Copco Elektronikon Mk5 is a control panel for a screw compressor. In my particular case, to power on the system, it must be touched via the touchscreen interface, and since this machine I'm working on has a defective digitizer, it completely rendered the whole machine useless.

## Atlas  Copco MK5 Graphic Touch

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/911553218d49df2b1167b16147127c8ec9aace63/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/Screenshot%202026-05-28%20001814.png)



# Alternative Solution

Now, my solution was to first look for a replacement and an alternative way to turn on the machine. It is supposed to have a remote option where you can connect external switches to run the machine, and there is also a LAN option to control the machine through LAN, but both of these are not available in the system probably not in my firmware.

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/main/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/Screenshot%202026-05-28%20002920.png)

But both local and remote control did not work thus ive devised a cheap solution to emulate the touch controller.

# Solution

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/6bed3685882c2aaf5162b41c2db4eb5e063006b5/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/2.png)

And upon inspection, the system utilizes a Goodix GT911 touch controller, which uses an I2C bus to communicate directly with the main control panel.


![App Screenshot](https://github.com/Username0240/Repair-Log/blob/8f461c3828caa9d16eabd00ee661c155e14da2eb/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/20260528_152959.jpg)


There are two compressors in the company with the same Atlas Mk5 control panel. One of the compressor control panels is fully working. Since it has the exact same control panel and touch controller, we could use a logic analyzer to capture the specific data that the touch controller sends to the control panel to power on the system. The turn-off signal needs to be recorded as well.


![App Screenshot](https://github.com/Username0240/Repair-Log/blob/a0473a50e2884c2aaec802c67c9e2f38fec88c0e/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/20260528_154403.jpg)

## Setup Initial signal

At boot-up the touch controller needs to be setup first it needs for the gt911 to read data from the control panel according to the gt911 goodix datasheet 
 
![App Screenshot](https://github.com/Username0240/Repair-Log/blob/30759eea77ff726719066b860626835dfd8a9bfd/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/Screenshot%202026-05-29%20152603.png)

## Turn ON signal

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/3c0b294068d13365490489d421b6ac2b366ab0bb/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/asdf.png)

## Turn Off signal

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/06cbbd388cfac55627589c0a4f3babedc6002c55/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/asdf2.png)

## Circuit
After getting the turn-on and turn-off data packets, a microcontroller just needs to be programmed to send the signal to the control panel.

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/55689c9eb8813488f9479e758553e77fe2294ad5/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/ezgif-7279ec69e0b72955.gif)

## Software
For the software, I utilized the Arduino IDE and the native `Wire.h` library. As shown in the image, the exact 6-byte data packets required to trigger the system are stored in memory arrays, ready to be executed and transmitted to the control panel to emulate the compressor's turn-on and turn-off actions.

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/9fc2cd82efe88b97a9adce9a6357aef0f4d0d741/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/c57a975b-e26b-45f3-b962-f2369b1b6878.jfif)

## Actual Testing
To test the control panel in the bench i also capture another touch coordinates that designates to the Menu and Home, this allow me to execute this command to verify that the touch is working without the actual compressor plugged in.

<video src="https://github.com/Username0240/Repair-Log/blob/86c0e1ada72ee2d5c4d695f497d0b07047726298/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/atlas%20test%20(1).mp4" controls width="100%">
  Your browser does not support the video tag.
</video>
