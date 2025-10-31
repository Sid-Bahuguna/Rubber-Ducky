# RaspberryPi Pico - Rubber Ducky

## Quick Start Guide

- [Pico-ducky](https://github.com/dbisu/pico-ducky/releases) -Download the latest releases
- Plug the device into a USB port while holding the boot button. It will show up as a removable media device named RPI-RP2.


## Install CircutlPython on the Pico or Pico W 


#### If using a Pico board: 
```
Copy the adafruit-circuitpython-raspberry_pi_pico-en_US-9.2.1.uf2 file to the root of the Pico (RPI-RP2). The device will reboot and after a second or so, it will reconnect as CIRCUITPY.
```

#### If using a Pico W board: 
```
Copy the adafruit-circuitpython-raspberry_pi_pico_w-en_US-9.2.1.uf2 file to the root of the Pico (RPI-RP2). The device will reboot and after a second or so, it will reconnect as CIRCUITPY.

```

#### If using a Pico 2 board: 
```
Copy the adafruit-circuitpython-raspberry_pi_pico2-en_US-9.2.1.uf2 file to the root of the Pico (RPI-RP2). The device will reboot and after a second or so, it will reconnect as CIRCUITPY.

```

#### If using a Pico 2W board:
```
Copy the adafruit-circuitpython-raspberry_pi_pico2_w-en_US-9.2.1.uf2 file to the root of the Pico (RPI-RP2). The device will reboot and after a second or so, it will reconnect as CIRCUITPY.

4. Copy the lib folder to the root of the CIRCUITPY
    
5. Copy *.py to the root of the CIRCUITPY
    
6. Follow the instructions in README.md to enter setup mode
    
7. Copy your payload as payload.dd to the root of the CIRCUITPY
    
8. Unplug the device from the USB port and remove the setup jumper.
```


### Setup mode

To edit the payload, enter setup mode by connecting the pin 1 (`GP0`) to pin 3 (`GND`), this will stop the pico-ducky from injecting the payload in your own machine. The easiest way to do so is by using a jumper wire between those pins as seen bellow.
<img width="685" height="325" alt="image" src="https://github.com/user-attachments/assets/08f7af34-33a1-4ff1-a8b5-1984e2e65d46" />


### USB enable/disable mode

If you need the pico-ducky to not show up as a USB mass storage device for stealth, follow these instructions.

- Enter setup mode.
- Copy your payload script to the pico-ducky.
- Disconnect the pico from your host PC.
- Connect a jumper wire between pin 18 (`GND`) and pin 20 (`GPIO15`).  
    This will prevent the pico-ducky from showing up as a USB drive when plugged into the target computer.
- Remove the jumper and reconnect to your PC to reprogram.

Pico: The default mode is USB mass storage enabled.  
Pico W: The default mode is USB mass storage **disabled**

![[Pasted image 20250924235050.png]]


## **Note: Add the all (4) jumper wires in order to edit the previous payload or use a wireless AP** 


## Full Install Instructions

1. Clone the repo to get a local copy of the files. `git clone https://github.com/dbisu/pico-ducky.git`
2. Download [CircuitPython for the Raspberry Pi Pico](https://circuitpython.org/board/raspberry_pi_pico/). *Updated to 9.2.1  
    Download [CircuitPython for the Raspberry Pi Pico W](https://circuitpython.org/board/raspberry_pi_pico_w/). *Updated to 9.2.1 Download [CircuitPython for the Raspberry Pi Pico 2](https://circuitpython.org/board/raspberry_pi_pico2/). *Updated to 9.2.1  
    Download [CircuitPython for the Raspberry Pi Pico 2W](https://circuitpython.org/board/raspberry_pi_pico2_w/). *Updated to 9.2.1
3. Plug the device into a USB port while holding the boot button. It will show up as a removable media device named `RPI-RP2`.
4. Copy the downloaded `.uf2` file to the root of the Pico (`RPI-RP2`). The device will reboot and after a second or so, it will reconnect as `CIRCUITPY`.

####  **Note: If you are not able to get the drive as CIRCUITPY use the  flash_nuke.uf2 to erase all the contents from the Pico** 
[flash_nuke.uf2](https://learn.adafruit.com/getting-started-with-raspberry-pi-pico-circuitpython/circuitpython)

5. Download `adafruit-circuitpython-bundle-9.x-mpy-YYYYMMDD.zip` [adafruit-circuitpython](https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/latest) and extract it outside the device.
6. Navigate to `lib` in the recently extracted folder and copy `adafruit_hid` to the `lib` folder on your Raspberry Pi Pico.
	1. 1. Copy `adafruit_debouncer.mpy` and `adafruit_ticks.mpy` to the `lib` folder on your Raspberry Pi Pico.
	2. Copy `asyncio` to the `lib` folder on your Pico.
	3. Copy `adafruit_wsgi` to the `lib` folder on your Pico.
	4. Copy `boot.py` from your clone to the root of your Pico.
	5. 1. Copy `duckyinpython.py`, `code.py`, `webapp.py`, `wsgiserver.py` to the root folder of the Pico.
7.  _For Pico W Only_ Create the file `secrets.py` in the root of the Pico W. This contains the AP name and password to be created by the Pico W.  
    `secrets = { 'ssid' : "BadAPName", 'password' : "badpassword" }`
8. Find a script [here](https://github.com/hak5/usbrubberducky-payloads) or [create your own one using Ducky Script](https://docs.hak5.org/hak5-usb-rubber-ducky/ducky-script-basics/hello-world) and save it as `payload.dd` in the Pico. Currently, pico-ducky only supports Ducky Script 1.0, and some of 3.0.
9. 1. Be careful, if your device isn't in [setup mode](https://github.com/dbisu/pico-ducky/#setup-mode), the device will reboot and after half a second, the script will run.
10. **Please note:** by default Pico W will not show as a USB drive


### Pico W Web Service
The Pico W AP defaults to ip address `192.168.4.1`. You should be able to find the webservice at `http://192.168.4.1:80`

The following endpoints are available on the webservice:
```
/
/new
/ducky
/edit/<filename>
/write/<filename>
/run/<filename>
```

### API endpoints
```
/api/run/<filenumber>
```

### Multiple payloads
Multiple payloads can be stored on the Pico and Pico W.  
To select a payload, ground one of these pins:
```
GP4 - payload.dd
GP5 - payload2.dd
GP10 - payload3.dd
GP11 - payload4.dd
```


### Links 
[pico-ducky-github](https://github.com/dbisu/pico-ducky/)
[ducky-scripts](https://github.com/SourasishBasu/PicoW-Ducky/)
[hak5-ducky-scripts](https://github.com/hak5/usbrubberducky-payloads)



