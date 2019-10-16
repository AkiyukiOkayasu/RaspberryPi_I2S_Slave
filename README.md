# RaspberryPi_I2S_Slave
General I2S slave I/O device tree overlay for Raspberry pi.  
Tested with Raspberry pi Compute Module 3+ and Asahi Kasei AK4556.  

- I2S slave: Raspberry pi
- I2S master: Audio codec(ex. AK4556)

[I2S Master version](https://github.com/AkiyukiOkayasu/RaspberryPi_I2S_Master)

## How to use  
Compile on Raspberry Pi  
```bash
dtc -@ -H epapr -O dtb -o genericstereoaudiocodec.dtbo -Wno-unit_address_vs_reg genericstereoaudiocodec.dts
```

Copy i2smaster.dtbo to /boot/overlays  
```bash
sudo cp genericstereoaudiocodec.dtbo /boot/overlays
```

Edit /boot/config.txt  
Enable I2S and add i2smaster device tree overlay  
```/boot/config.txt    # Uncomment some or all of these to enable the optional hardware interface
#dtparam=i2c_arm=on
dtparam=i2s=on
#dtparam=spi=on
dtoverlay=genericstereoaudiocodec
```

If you don't need HDMI audio output and Raspberry Pi's headphone output, comment out "dtparam=audio=on" by hash.  
like this.  
```/boot/config.txt
#dtparam=audio=on
```
