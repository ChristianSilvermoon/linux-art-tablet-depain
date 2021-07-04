# Monoprice 10x6.5in (10954)

A relatively cheap tablet
[Amazon Link](https://www.amazon.com/Monoprice-6-25-inch-Graphic-Drawing-Tablet/dp/B00H4LAF9O/ref=sr_1_1?dchild=1&keywords=monoprice+10594&qid=1625428444&sr=8-1)
The drivers for Windows appear to be simplistic and possibly outdated or unmaintained. But you're probably here for Linux info

## Distros Tested

| Distro          | Status                   |
| ---             | ---                      |
| Linux Mint 20.x | Functioning, minor quirk |


### Caveats
For some unknown reason, the pen button which triggers the radial UI in [Krita](https://krita.org/en/) (Upper Pen Button / Right Click) will behave strangely, when pressing the button, the menu will spawn, but when releasing it will despawn, rendering the menu unable to be used.

To work around this, pressing the button and quickly releasing it by sliding the thumb off seems not to trigger this odd effect.

## How To Get It Working

### Part 1: Drivers
It was necessary to rely on the [DIGIMend](https://digimend.github.io/) Driver to get the tablet working. It was necessary to **compile it from source** due to what appeared to be a bug with Ubuntu 20.04 / Linux Mint 20, which was worked around using [a solution suggested in digimend-kernel-drivers Issue #387](https://github.com/DIGImend/digimend-kernel-drivers/issues/387#issuecomment-683452351)

### Part 2: X11 Configuration
With the driver installed, the next step was to get the tablet working with `xsetwacom`, which was done using [information from digimend-kernel-drivers Issue #42](https://github.com/DIGImend/digimend-kernel-drivers/issues/42#issuecomment-353995855)
which involved creating a configuration file for X11, which can be found in this tablet's `xorg.conf.d` directory

### Part 3: Input Mapping

With the above taken care of, the tablet at this point should be operational in a way that allows clicking and pressure sensitivty from the pen, however, the buttons may be non-functional and, should you have multiple monitors, the tablet may cover ALL monitors, as opposed to the one you want.

To deal with this, a Mapping Script (located in Scripts) was created. It is recommended to set this up to start automatically on login.

The script will detect whether or not the tablet is connected, and automatically map to the display "HDMI-0" along with setting up the buttons to do what would be expected for [Krita](https://krita.org/en/). After mapping, the script will send a desktop notificaiton using `notify-send` to alert you. If the tablet should become disconnected, it will also notify you.

This script will loop infinitely in the background and ensure that when connected, the tablet is mapped correctly, and should consume only a negligable amount of resources.

You may wish to **modify your local copy of the script** to fit your preferences and personal computer configuration better.
