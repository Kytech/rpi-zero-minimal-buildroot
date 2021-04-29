# rpi-zero-minimal-buildroot

A Minimal Buildroot config for the Raspberry Pi Zero, inspired by [Minimal Raspberry Pi 3](https://github.com/romainreignier/minimal_raspberrypi_buildroot), but with most features usable out of the box. This build should serve as a good starting point for any headless pi zero embedded projects.

Kernel boot time measures approximately 2 seconds when the `quiet` parameter is added to the pi kernel's `cmdline.txt` arguments. Without changing the `start.elf` bootloader to the cutdown version, the total boot time from initial power on is about 5-6 seconds. Overclocking the SD card, if you have a class 10 or UHS 1 card, should yeild a bit of a boost. Shaved off about 0.5-1 second on my board. Additional gains can come by trimming unused kernel features as well. An initramfs and/or embedded device tree may also improve overall boot times.

See below section for limitations.

## Repo Notes

This repository uses git submodules to manage the buildroot version used by this project. As such, you will want to clone this repository using `git clone --recursive` or manually initialize the buildroot submodule yourself. This submodule is configured to be the `buildroot` directory in this repository.

## Usage

After cloning the repository (and initializing the buildroot submodule if cloning without `--recursive`), navigate to the `build_workdir` directory and run `./configure`. This sets up the buildroot external tree. From there, run any buildroot commands from the `build_workdir` directory to keep a clean external tree setup.

## Known Limitations

If you plan to use the camera port, you will need to modify the buildroot config to produce the `start_x.elf` bootloader/firmware file.

Networking is disabled in the kernel config. Since standard pi zeros do not have wireless, this just added extra time to the boot. If you are using an external network card, you will need to re-enable networking in the kernel.

The current busybox setup still leaves in place a network service startup script that will fail quickly due to networking being removed from the kernel. I'm sure I'll get around to cleaning that up sometime soon. If it's an issue, just delete the script from the `/etc/init.d` folder in the generated image.

This configuration uses the musl c library. It was chosen due to its very diminuitive size and its growing use (ex. standard clib in Alpine linux). If you have a program that relies on glibc quirks or want to use uclibc, change the clib in the buildroot config.
