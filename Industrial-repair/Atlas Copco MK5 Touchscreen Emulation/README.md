
# Atlas Copco Elektronikon Mk5 Touchscreen Protocol Emulation

Modern devices today are so reliant on touchscreens. We even have cars where almost all of their crucial function buttons are in the touchscreen infotainment system. Industrial machines are not an exception either; the Atlas Copco Elektronikon Mk5 is a control panel for a screw compressor. In my particular case, to power on the system, it must be touched via the touchscreen interface, and since this machine I'm working on has a defective digitizer, it completely rendered the whole machine useless.

## Atlas  Copco MK5 Graphic Touch

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/911553218d49df2b1167b16147127c8ec9aace63/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/Screenshot%202026-05-28%20001814.png)



## Alternatives

Now, my solution was to first look for a replacement and an alternative way to turn on the machine. It is supposed to have a remote option where you can connect external switches to run the machine, and there is also a LAN option to control the machine through LAN, but both of these are not available in the system probably not in my firmware.

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/main/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/Screenshot%202026-05-28%20002920.png)

But both local and remote control did not work thus ive devised a cheap solution to emulate the touch controller.

## Solution

![App Screenshot](https://github.com/Username0240/Repair-Log/blob/6bed3685882c2aaf5162b41c2db4eb5e063006b5/Industrial-repair/Atlas%20Copco%20MK5%20Touchscreen%20Emulation/image/2.png)

And upon inspection, the system utilizes a Goodix GT911 touch controller, which uses an I2C bus to communicate directly with the main control panel.
