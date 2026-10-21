# Qualcomm Atheros (ath10k) QCA9377 alternative Linux firmware
Alternative, experimental and quickly tested alternative firmware-6.bin and board-2.bin for Qualcomm Atheros QCA9377 Wifi/Bluetooth wireless PCIE device (hw1.1).

The files are sourced from last available 2019 Windows 11 driver installer for Lenovo ideapad S330-14IKB.
board-2 is derived from QCA9377 specific file from the driver's extracted files. As of writing, works even with the current linux-firmware packages on Linux Mint/cachyOS.
firmware-6 is derived from QCA9377_2.0.bin, main windows driver firmware glob that seemingly included two OTP's, main firmware and test firmware. The OTP's at least in copy left to right process do not produce a functional firmware package, as on Linux this OTP fails to initialize the hardware. Using the current linux-firmware provided firmware file as source, extracting OTP from it, and pairing it with the main firmware blob from the Lenovo driver source ends up with a usable alternative firmware file for this wifi hardware, at least on hw1.1 variant found on my personal S330-14IKB.
This ends up in hope and theory with nebulously "better", at least more hardware specific usable firmware for QCA9377 hw1.1 that my personal laptop has.

As noted in short earlier, this is not proof-tested. I am not liable for any boot failures, device crashes or circumcision that may occur.
On my hardware, the firmware files are tested to function, and not loose any basic expected functionality, while findings of any improvements is also not confirmed.
It boots, it initializes, it runs the device, everything seems to work, nothing seems to be broken is about extent of things to say about confirmed functionality.

## Installation (non-destructive, reversible)
Place the two files with your favorite manner of elevated file access into /lib/firmware/updates/ath10k/QCA9377/hw1.0/
This is reversible by simply removing these files as the main files in /lib/firmware/ath10k/ remain untouched, but your specific distro's compatibility with updates loading may vary.
ath10k_pci should report after a initramfs update and reboot or modprobes `firmware ver WLAN.TF.2.1-WINTEST-BS api 6 features wowlan,ignore-otp`

## Disclaimers
These were created using qca-swiss-army-knife and balling against a claude chat. All it boiled down to was using windows data and repackaging it to linux compatible format. Main thing was to use existing linux-firmware otp as the ones in windows 2.0 glob failed to initialize, but the firmware with existing otp results in usable.
I am no professional and not professionally rebuilding anything.
This repo exists more as a personal backup to these files than thing to spread to everyone. If you find this and it helps your device out, good.
