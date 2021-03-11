# raspberry-qemu

## Get Raspberry Pi Os image and qemu-ready kernels
```shell
cd ${HOME}
wget https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2021-01-12/2021-01-11-raspios-buster-armhf-lite.zip
unzip 2021-01-11-raspios-buster-armhf-lite.zip
git clone --depth 1 https://github.com/dhruvvyas90/qemu-rpi-kernel
```

## Get and compile Qemu
```shell
wget https://download.qemu.org/qemu-5.2.0.tar.xz
tar xvJf qemu-5.2.0.tar.xz
cd qemu-5.2.0
./configure --target-list=aarch64-softmmu,arm-softmmu
make
cd build/
```
## Run Raspberry Pi (Hint: default user 'pi' with password 'raspberry')
```
./qemu-system-arm -dtb "${HOME}/qemu-rpi-kernel/versatile-pb-buster.dtb" -kernel "${HOME}/qemu-rpi-kernel/kernel-qemu-4.19.50-buster" -append 'root=/dev/sda2 panic=1' -cpu arm1176 -m 256 -M versatilepb -serial stdio -hda "${HOME}/2021-01-11-raspios-buster-armhf-lite.img" -no-reboot
```
## Connect to Pi
vncviewer localhost:5900
