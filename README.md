# ELoad

## Introduction

This is ELoad, a fast loader library for various Commodore 64/128 drives.

## Website, Repository and Issue Tracker

EasyFlash website: https://skoe.de/easyflash/

Official repository and issue tracker:
https://gitlab.com/easyflash/eload/

Other EasyFlash related repositories:
https://gitlab.com/easyflash/

Source repository mirror:
https://github.com/easyflash-mirror/eload/

## License

(C) Thomas 'skoe' Giesel

Refer to [LICENSE.md](./LICENSE.md).

## Memory Maps

Memory map for 1541:

| Address         | Usage |
|-----------------|-------|
| $0000           | ZP    |
| $0100           | Stack |
| $0300 <br>$0400 | drive_code_1541 (init and xfer) <br> drive_code_1541 (common code) |
| $0500 <br>$0600 | drive_code_1541_read or write <br>&nbsp; |
| $0700           | buffer |

## Drive Code Overlays

`drive_code_init_size_1541` bytes at `drive_code_1541` are uploaded using the
KERNAL transfer functions to `$0300`. This is 256 bytes or less. When this
code runs, it loads 512 bytes using the fast protocol to `$0300`. Note that
the init code is overwritten with the same code again in this phase.
Next it loads 512 bytes overlay code to $0500 and calls it with `JSR`.
Each time the overlay code returns with `RTS`, motor and LED are switched
off and the transfer and start of the 2 blocks of overlay code is repeated.
Note that the motor deactivation is delayed with a timer, this is implemented
in DOS.

The overlay code waits for eload job codes. Job code 0 leaves the overlay
code (RTS).

## Job Codes

TODO
