![](../images/sonoma.png)


::: warning
macOS Sonoma is supported by OpenCore Legacy Patcher **1.0.0 and later,** currently in early stages.  
Use the latest available version for the most stability.
:::

## Dropped Hardware

In addition to all unsupported Macs, the following models will now require OpenCore Legacy Patcher to run macOS Ventura:

| Model Name | Model Identifier |
| — | — |
| iMac (21.5-inch, 2017) | `iMac18,1` | 
| iMac (Retina 4K, 21.5-inch, 2017) | `iMac18,2` | 
| iMac (Retina 5K, 27-inch, 2017) | `iMac18,3` |
| MacBook (Retina, 12-inch, 2017) | `MacBook10,1` | 
| MacBook Pro (13-inch, 2017, 2 Thunderbolt 3 ports) | `MacBookPro13,1` | 
| MacBook Pro (13-inch, 2017, 4 Thunderbolt 3 ports) | `MacBookPro13,2` | 
| MacBook Pro (15-inch, 2017) | `MacBookPro13,3` | 

## Updates to OCLP versioning

With 1.0.0, we'll be switching to a proper major, minor and bug fix system ([Semantic Versioning](https://semver.org/)). This means the coming release will be version 1.0.0, and future releases plan to follow this scheme:

- First digit: Major changes, including new OS support, API changes, and significant patch set changes, etc
- Second digit: Minor changes, including incoming OS update fixes, minor patch set changes, etc
- Third digit: Bug fixes, primarily hot fixes either due to a regression in prior release or resolving issues in already released OS updates

## Current Issues

* [Bluetooth](#bluetooth)
* [T1 Security chip](#t1-security-chip)
* [USB 1.1 (OHCI/UHCI) Support](#usb-11-ohciuhci-support)
* [Graphics support and issues](#graphics-support-and-issues)


### Bluetooth

Sometimes Bluetooth may not work after boot on pre-2012 models. Running NVRAM reset can alleviate it.

Dual boots may also bring the issue back even after the reset.

### T1 Security chip

::: details Support for the T1 Security chip (Resolved in 1.1.0 and newer)

Sonoma has removed support for T1 chips found in the 2016 and 2017 MacBook Pros with Touch Bar. Therefore on these systems, the following will not function:

* Enable or disable FileVault
* Open the Password Settings window
* Add fingerprints (if upgrading, existing fingerprints will be deleted)
* Add cards to Apple Pay

[More information here](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/1103)

:::

::: warning
**Do not** erase the EFI partition on the internal drive of these machines when upgrading to macOS Sonoma. If a clean install is desired, this can be done by erasing the APFS container.

Erasing the EFI partition of these Macs results in the T1 Security chip firmware being removed, killing all functionality related to it: Touch ID, Touch Bar, Apple Pay, etc.

Since the firmware cannot currently be reinstalled from macOS Sonoma, reinstalling macOS Ventura or earlier, as well as having a connection to the internet, is required to restore the firmware.
:::

::: warning
Updating macOS may result in enrolled fingerprints and Apple Pay cards being removed from the system, as well as FileVault automatically being disabled.
:::

### USB 1.1 (OHCI/UHCI) Support

For Penryn systems, pre-2013 Mac Pros and Xserve, USB 1.1 support was outright removed in macOS Ventura and naturally this continues in Sonoma.
While USB 1.1 may seem unimportant, it handles many important devices on your system. These include:

* Keyboard and Trackpad for laptops
* IR Receivers
* Bluetooth

With OpenCore Legacy Patcher v0.6.0+, basic support has been implemented via Root Volume patching. However due to this, users will need to use a USB hub for installation and post-OS updates when patches are cleaned:

![](../images/usb11-chart.png)

::: warning The following systems rely on USB 1.1

* iMac10,x and older
* Macmini4,1 and older
* MacBook7,1 and older
* MacBookAir3,1 and older
* MacPro5,1 and older
* Xserve 3,1 and older
:::

[More information here](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/1021)

### Graphics support and issues
This build includes both Legacy Metal and non-Metal patches for macOS Sonoma. Refer to the following links for more information about Legacy Metal and non-Metal support and their respective issues.

* [Legacy Metal](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/1008)
* [Non-Metal](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/108)

