## Package install of ver 9.0 piaware, dump1090-fa, piaware-web, and dump978-fa on:
### (1) Ubuntu-22.04 (jammy) amd64/x86_64 (PC / Laptop) 
### (2) Ubuntu-22.04 (jammy) arm64/aarch64 (RPi 3 & 4) 
### (3) Ubuntu-22.04 (jammy) armhf/armv7l (RPi 3 & 4) </br></br>

### STEP-1: Add this repository to list of apt sources by following 3 commands:
**First two commands are long. Please scroll right to see and copy them in FULL.** 
```
sudo wget -O /etc/apt/sources.list.d/abcd567a.list https://abcd567a.github.io/ubuntu22/abcd567a.list  
```
```
sudo wget -O /etc/apt/trusted.gpg.d/abcd567a-key.gpg https://abcd567a.github.io/ubuntu22/KEY2.gpg  
```
```
sudo apt update  
```

</br>

### STEP-2: Install packages
```
sudo apt install piaware  
```
```
sudo apt install dump1090-fa  
```
```
sudo apt install piaware-web  
```
```
sudo piaware-config feeder-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
```
sudo reboot 
```

&nbsp;

### STEP-3: (for USA only) Additional steps to install & configure dump978-fa

```
sudo apt install dump978-fa  
```
```
sudo apt install skyaware978  
```
```
sudo piaware-config uat-receiver-type sdr  
```

**Configure dump1090-fa and dump978-fa to use their respective dongles.**
If you want to receive both ES1090 and UAT978, then two dongles are required, one for 1090 MHz and other for 978 MHz. In this case you will have to serialize dongles so that correct dongle+antenna sets are used by dump1090-fa and dump978-fa.
Serialize dongles with following serial numbers </br>

**For 1090 Mhz dongle: use 8-digit serial # 00001090** </br>
**For 978 Mhz dongle : use 8-digit serial # 00000978** </br>

After Serializing dongles with serial numbers as above, issue following commands to configure dump1090-fa and dump978-fa to use their respective dongles:

```
sudo sed -i 's/^RECEIVER_SERIAL=.*/RECEIVER_SERIAL=00001090/' /etc/default/dump1090-fa  
```
```
sudo sed -i 's/driver=rtlsdr[^ ]* /driver=rtlsdr,serial=00000978 /' /etc/default/dump978-fa  
```  
```
sudo reboot 
```

## How to Serialize Dongles:
(1) Issue following command to install serialization software: </br>
`sudo apt install rtl-sdr ` </br>

(2) Unplug ALL DVB-T dongles from Computer

(3) Plugin only that DVB-T dongle which you want to use for dump1090-fa. All other dongles should be unplugged.

(4) Issue following command. </br>
`rtl_eeprom -s 00001090 ` </br>
Say yes when asked for confirmation to change serial number.


(5) Unplug 1090 dongle

(6) Plugin only that DVB-T dongle which you want to use for dump978-fa. All other dongles should be unplugged.

(7) Issue following command. </br>
`rtl_eeprom -s 00000978 ` </br>
Say yes when asked for confirmation to change serial number.


(8) Unplug 978 dongle

IMPORTANT: After completing above commands, unplug and then replug both dongles.



&nbsp;

### How to remove this repository from your Computer:

Deleting this repository from your Pi’s apt sources list is simple. Just issue following 2 command and it is done:

```
sudo rm /etc/apt/sources.list.d/abcd567a.list 
```
```
sudo apt update 
```

&nbsp;
