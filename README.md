# DECEASED: raspberrypi-FFmpegNDI

*NDI support in FFmpeg was removed in the FFMPEG source on the 20th of March 2019.

https://github.com/FFmpeg/FFmpeg/commit/4b32f8b3ebfa011fcc5991bcaa97c3f5b61b49ad

This is from a license dispute with Newtek ( https://trac.ffmpeg.org/ticket/7589 ) and NDI support has now been removed from FFmpeg.

I will take these projects offline.

Apologies for the inconvenience.

Regards,

Johan Els *

Use Raspberry Pi as a NewTek NDI® monitor. Please ensure you register on the NewTek NDI® Software Developer Kit site using https://www.newtek.com/ndi/sdk/ before continuing.

You will have to run this locally or over ssh on the Raspberry Pi to be able to accept the NewTek NDI® SDK license agreement.

## Raspbian Micro SD Image on Mac OS
```bash
wget https://downloads.raspberrypi.org/raspbian_lite_latest
unzip
diskutil list
diskutil eraseDisk FAT32 RASBIAN /dev/disk(n)
sudo dd bs=1m if=[RASBIAN image file].img /of=/dev/(r)disk(n) conv=sync
```

## Raspberry Pi SSH server
```bash
sudo raspi-config
```

## Graphics
Click the Raspberry Menu | Preferences | Raspberry Pi Configuration | Performance Tab
Change "GPU Memory" to 128
Click OK | Click Yes to reboot


## Additional notes:
```bash
# Raspberry Pi WiFi
sudo iwlist wlan0 scan | grep ESSID
sudo bash -c 'cat << EOF >> /etc/wpa_supplicant/wpa_supplicant.conf
network={
    ssid="SSID"
    psk="PASS"
}
EOF'

# FFmpeg
ffmpeg -f libndi_newtek -extra_ips "10.10.10.100" -find_sources 1 -i dummy
ffmpeg -re -i /temp/input.mp4 -f libndi_newtek -pix_fmt uyvy422 Sample
ffplay -f libndi_newtek -i "Sample"
```
