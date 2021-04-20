# rpi-zero-minimal-buildroot

A Minimal Buildroot config for the Raspberry Pi Zero, inspired by [Minimal Raspberry Pi 3](https://github.com/romainreignier/minimal_raspberrypi_buildroot).

**This project is currently a work in progress!** The current main branch may not be usable at the moment!

## Notes

This repository uses git submodules to manage the buildroot version used by this project. As such, you will want to clone this repository using `git clone --recursive` or manually initialize the buildroot submodule yourself. This submodule is configured to be the `buildroot` directory in this repository.

## Usage

After cloning the repository (and initializing the buildroot submodule if cloning without `--recursive`), navigate to the `build_workdir` directory and run `./configure`. This sets up the buildroot external tree. From there, run any buildroot commands from the `build_workdir` directory to keep a clean external tree setup.
