# TBS-Satellite-Tuner-Patches-For-DontLookUp
This repo contains AI vibe-coded patches to enable raw data handling on TBS satellite tuners. Use at your own risk! 


Follow my DontLookUp tutorial for more information (timestamp 5 minutes and 10 seconds onwards):

https://youtu.be/jdTF1PFWJJo

# Patching Instructions For TBS5930 USB DVB-S2X Tuner

Tested and working in DragonOS FocalX R37 And DragonOS Noble R7:
```
sudo apt-get update

sudo apt-get install patchutils gcc-12 libproc-processtable-perl -y

cd ~/

git clone https://github.com/tbsdtv/media_build.git

git clone --depth=1 https://github.com/tbsdtv/linux_media.git -b latest ./media

wget https://raw.githubusercontent.com/RobVK8FOES/TBS-Satellite-Tuner-Patches-For-DontLookUp/refs/heads/main/5930_raw_payload.patch

cd ~/media/drivers/media/usb/dvb-usb/

git apply ~/5930_raw_payload.patch

cd ~/media_build

make dir DIR=../media

make allyesconfig

sed -i -r 's/(^CONFIG.*_RC.*=)./\1n/g' v4l/.config

sed -i -r 's/(^CONFIG.*_IR.*=)./\1n/g' v4l/.config

make -j$(nproc)

sudo make install

cd ~/

wget http://www.tbsdtv.com/download/document/linux/tbs-tuner-firmwares_v1.0.tar.bz2

sudo tar jxvf tbs-tuner-firmwares_v1.0.tar.bz2 -C /lib/firmware/
```

Reboot PC to load patched drivers.

It is safe to delete the 'media' and 'media_build' folders, '5930_raw_payload.patch' file, and the 'tbs-tuner-firmwares_v1.0.tar.bz2' archive from your /home/ directory
