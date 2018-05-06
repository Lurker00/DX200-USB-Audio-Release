# USB Audio for DX200 and DX150
1. [Introduction](#introduction)
1. [Menu items](#menu-items)
1. [Settings](#settings)
1. [Indicator color](#indicator-color)
1. [FAQ](#faq)
1. [Known problems](#known-problems)
1. [History of public releases](#history-of-public-releases)

## Introduction
### For everybody
Starting from version **1.2.59**, this application became a system wide control center, meaning, useful for anybody:
* [***System settings***](#system-settings) menu allows to stop Google/Android unwanted background activity, and to provide write access to SD-card for any application.
* The application reliably detects music playback, and [***Smart release of WakeLock***](#settings) works for any music player.

I could make a separate application for this purpose, but it would be waste of time that I can devote for this work.

### For hi-res and DSD listeners
This application switches iBasso DX200 audio processor (XMOS chip) into USB DAC mode, accessible for Android applications, installed on this DX200 itself! When **USB Audio** starts the USB DAC Interface, any compatible Android music player application, that supports and is configured to use a USB DAC, will play bit perfect audio, including DSD! For DSD, it supports both Native and DoP modes, and even DoP-encoded PCM formats, e.g. in flac.

Don't like Mango, or it does not suit your needs? Just forget about it, and use other applications, fully utilizing the great hardware of DX200! The startup screen of **USB Audio** has listed compatible applications, along with the required settings.

Currently, there are 3 applications, fully compatible with USB Audio:
* free [HibyMusic](https://play.google.com/store/apps/details?id=com.hiby.music) (a special build is embedded into firmware 2.2.110 Rev.2 and later),
* [USB Audio Player PRO](https://play.google.com/store/apps/details?id=com.extreamsd.usbaudioplayerpro),
* [Neutron Music](https://play.google.com/store/apps/details?id=com.neutroncode.mp).

They cover almost, if not all, file formats and sound sources around, and have rich functionality.

**Please note:** When Mango plays DSD tracks, it switches XMOS chip into USB DAC mode. Avoid playing DSD in Mango in Android, if you have configured UAPP/Hiby/Neutron to auto-start when USB DAC is attached! They will fight for the access to USB DAC with Mango.

**Warning:** Avoid having installed and configured for USB DAC playback more than one application at a time! They tend to autolaunch on a device attached, and you'll have a mess! If you want more than one USB Audio compatible music player, use ***Active player*** feature to avoid problems.

## Menu items
* ***Settings*** - see [below for details](#settings).
* ***System settings*** - system wide settings and actions. See [below for details](#system-settings).
* ***USB DAC*** - turns DX200 into USB DAC mode. The Android interface is disabled while USB DAC mode is active.
* ***Clear the log*** - clears the log screen.
* ***Show ALSA state*** - displays information about currently played music format. This is the format that ALSA (Linux level sound driver) accepts and then sends to the DAC.
* ***Exit*** - exits the application and removes its icon and bar from the notifications area.

## Settings
* ***Acquire WakeLock*** - prevents the device to go to sleep mode, while the interface is active. Without ***Smart release of WakeLock***, you have to stop the interface manually to let the device sleep.
* ***Smart release of WakeLock*** - checks for music playback in a supported application, and releases the wakelock after ***Idle Timeout*** period of detected inactivity.
* ***Idle Timeout*** - number of seconds of inactivity of a supported application, after which the wakelock is released.
* ***Active player*** - choose the music player application that you currently use most of time, even if you have only one USB Audio compatible player. On USB device attached event, it grants access to the USB device without questions and launches the player chosen. This eliminates possible conflicts and simplifies the use. If you want to control access rights manually, select *I'll control it myself!* and tap OK.
* ***Beep on USB Audio detached*** beeps if the USB interface has been detached, and the screen is turned off. It is useful to know that ***Idle timeout*** has been expired, and you need to turn screen on for a moment to continue listening.
* ***Autostart*** - turn on to start the interface on application launch, without the need to push _Start_ button.
* ***Current theme*** allows you to choose from 6 Android standard themes for the application.

***Active player*** lists the currently installed supported applications. If you have an application you want to be supported, please let me know!

## System settings
For the best experience, it is recommended to turn these settings all green.
* ***Enforce deep sleep*** - sets [Android's DeviceIdleController](https://android.googlesource.com/platform/frameworks/base/+/marshmallow-release/services/core/java/com/android/server/DeviceIdleController.java) parameters to values, optimized for average DAP usage, to minimize battery drain when DAP is not used.
* ***Disable Google services*** disables both Google services and Play Market, and eliminates their background activity. It backs up your Google account information, and restores it when this option is turned off.
* ***Disable media scanner*** stops the media scanner, which scans all your files time to time. Turning this option off forces media re-scan, which is useful when you have added or deleted some files, and want to access them via MTP.
* ***Battery saver*** - turns on Android Battery Saver mode system wide. It does not actually save much battery, because the main consumers are DAC and amp. But it does reduce background activity of Android and Google stuff, and other apps.
* ***Hide MangoPlayer*** just hides MangoPlayer away from the desktop, like it is not installed. Recommended if you don't actually use it.
* ***Disable system logs*** - turn this option off only if you need to collect system logs for investigation, or if disabling them creates problems, like for user interface of SuperSU. Disabled by default for 32-bit apps, because it eliminates a lot of background work.
* ***DSD/384kHz support for Neutron*** - turn it off only if this support creates conflicts with other applications (very unlikely).

### Actions
* ***Collect system logs*** - push this button to collect system logs, e.g. to send to me for investigation. It creates files on the internal storage with names `syslogs0.tgz`, `syslogs1.tgz` etc. up to 5 in total, and `syslogs0.tgz` is always the most recent collection.
* ***Grant SD card write access to all apps*** - Android in DX200 has broken the standard way to let the user grant write access to apps. This button grants it to all at once. If you have updated an app that needs write access, you have to push this button again.

## Indicator color
The circle in the bottom right corner of the application icon in the notification bar reflects the current state:
* Gray - idle state.
* Green - the interface is active and ready to use.
* Yellow - the interface is being restarted after a disconnect.
* Red - the interface was disconnected and is about to be restarted.
* Blue - idle state with music playback detected. The smart wakelock is active.

## FAQ
**Q**: Is it safe to run DX200 in this mode?<br />
**A**: Actually, Mango on both DX80 and DX200 uses this mode to playback DSD. So, yes - it is safe!

**Q**: Do I need a special/custom firmware build, or a root access, or anything else special?<br />
**A**: The basic functionality works with any stock firmware. Advanced features added in 1.0.24+ versions require it to be a part of the custom firmware.

**Q**: Why XXX application is not compatible, but perfectly deals with an external USB DAC?<br />
**A**: I don't know the exact reason, but, most probably, this is due to misuse of the volume controls, which leads to damaged bit stream output to this USB DAC.

**Q**: PCM formats sound OK, but with DSD I hear only a noise! What's wrong?<br />
**A**: Check software volume control in your player application and be sure it is set to 100%.

**Q**: Where is my internal storage in USB Mass Storage mode? The second disk is not inserted!<br />
**A**: USB Mass Storage provides direct access to a real disk. The user visible internal storage is actually a folder of the internal disk (flash partition formatted with ext4). Though it is possible to export this whole partition, and ext4-aware OS (Linux) recognizes it, it has a little sense, because access rights keep the iternal storage directory out of reach anyway. Changing (accidentally or intentionally) these access rights will ruin DX200.

**Q**: USB Audio looks like hung on starting the interface. Why?<br />
**A**: Most probably an application plays music via Android, and keeps the interface from switching this way. Push Pause button to let USB Audio go.

**Q**: PowerAmp Alpha has claimed to support USB DACs, but it does not produce any sound with USB Audio. Why?<br />
**A**: Actually, PowerAmp build 703/704 does not support USB DACs directly. It relies on Android to route the sound to the DAC correctly. But in DX200, Android does not correctly route sound to USB Audio.

## Known problems
During playback of tracks with 44.1KHz sampling rate, short cracking noise may appear time to time, with several seconds, or even minutes, in between. The reason is still unknown, and there is no a way to avoid it. It happens with all the players tested, and does not happen with any other sample rate, including DSD. A workaround for 16/44.1 recordings is to use any player with playback via Android: it does not affect the quality ([the proof](https://github.com/Lurker00/DX200-firmware/blob/master/tools/README.md#tracks-to-test-bit-perfect-playback)). The best solution is to use [Neutron Music](https://play.google.com/store/apps/details?id=com.neutroncode.mp) with its Generic Driver (not with USB Audio!), because it is able to play bit perfect audio up to 24/192, including 24/44.1.

## History of public releases
**1.2.69** - only available in [custom firmware builds](https://github.com/Lurker00/DX150-firmware) starting from 2.9.250L0:
* Support for iBasso DX150.

**1.2.68** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.8.198L1:
* It does not hide USB-capable music players, if an **Active player** was selected.

**1.2.65** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.8.198L0:
* Disabling Google Services also disables/enables YouTube amd Google Music applications, if they are installed. They won't work without GMS anyway, but wake up the device and drain battery.

**1.2.63** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.7.188L1:
* Bug fix: USB DAC mode was affected by ***Smart release of WakeLock*** timeout.
* Better support for devices with XMOS firmware version 1.20 (shipped after August, 2017).

**1.2.59** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.7.188L0:
* Menu ***System settings*** accomodates system wide settings to minimize Android/Google background activity, leading to improved battery life in sleep mode and sound performance.
* Menu ***Show ALSA state*** to display information about currently playing format.
* Application look can be changed by choosing from 6 available themes.

**1.1.48** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.5.141L1:
* With ***Smart release of WakeLock*** turned on, when in idle state, USB Audio detects music playback in any application, and acquires its own wakelock to prevent Android from immediate sleep mode when the music is put on pause. The wakelock timeout is controlled by the same ***Idle Timeout*** value.
* ***Filter media buttons*** option has been removed.

**1.1.45** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.3.125L2:
* All CPU cores control has been removed, including ***CPU Turbo Mode***: CPU cores are controled by custom Android Power HAL module.

**1.1.44** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.3.125L1:
* Start/Stop button in the notification bar, to control from the lock screen.
* Support for Onkyo HF Player. Warning: don't touch volume control, when Onkyo HF Player plays via USB Audio, as it may damage your hearing and/or headphones!
* Now USB Audio detects Internet connection, and disables ***Battery saver*** mode on connect, and restores on disconnect.

**1.1.43** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.3.125:
* Most of the settings are moved into the ***Settings*** menu. This new user interface item is the reason to increase the minor version number ;)
* ***Filter media buttons***, ***Beep on USB Audio detached***, ***Hide MangoPlayer*** settings added.
* If music is being played via Android, USB Audio can't start the interface. The new version detects such situations, informs the user via a toast, and does prevents manual start of the interface in such a situation.
* A new method to turn the USB interface on and keep it active, which does not consume a CPU cycle anymore.

**1.0.39** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.2.110 Rev.2:
* ***USB DAC*** menu item - turns DX200 into USB DAC mode.
* USB Audio saves at reboot or power off, and restores ant boot up, the DX200-specific sound settings: digital filter, gain, auto-mute. Now MangoPlayer has no a feature that requires to use it.
* Attempt to switch XMOS chip modes (start/stop interface, start/stop USB DAC) is not allowed when an S/PDIF cable is attached, and a warning message is displayed. This is due to a discovered problem, that the audio driver does not correctly switches modes with S/PDIF cable attached, down to device hang.
* Minor bug fixes, notification display improved.

**1.0.35** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.2.110 Rev.1:
* ***Active player*** added, ***Battery saver*** is improved: it stops 4 out of 8 CPU kernels, and stops Media Scanner.
* The notification bar now contains information about current application state, displays number of detected wakelocks (right bottom corner, including its own wakelock), and idle time chronometer.
* If the interface was detached due to doze mode, it is not restarted immediatelly once the screen is turned on: it waits for around 5 seconds before initiates restart. This allows to only take a look to the lock screen, or keeps the interface from unneeded restart in case a background service turns the display on for a moment.
* Many other fixes and improvements.

**1.0.30** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.2.110:
* ***Smart release of WakeLock*** menu setting added, with corresponding ***Idle Timeout*** value.
* ***Battery saver*** menu option added.
* ***CPU Turbo Mode*** menu option added. Turn it on, if music can't be played when the display is turned off. For instance, playback of SACD ISO images encoded with DST requires a lot of CPU power. When display turns off, Android on DX200 stops 7 from 8 CPU cores. Turbo Mode keeps 3 additional cores (to 4 total) from stopping. If _Acquire WakeLock_ and _Smart Release_ are enabled, the cores are made available for stopping during smart release period. Turbo Mode is activated on application start, even if the interface is not started. This allows to use MangoPlayer in Turbo mode as well, but be careful: smart  release does not work when the interface is not started!

These features require either SuperSU installed, or permissions available only for pre-installed applications. This restriction makes no sense to make new versions for the stock firmware anymore.

**1.0.23** - The problem of 1.0.22 has been solved: with wakelock acquired, it is not killed, and stays until turned off manually, or while the battery lasts, whatever is sooner. _This is the last release as a standalone application. All further versions are integrated into firmware mods._

**1.0.22**:
* ***Exit*** button moved to 3-dots menu. The options are in the menu as well.
* Optional ***Acquire WakeLock*** to prevent interface shutdown in doze mode. **Note**: don't forget to stop interface when idle!
* Optional ***Autostart*** to start the interface without the need to push _Start_ button.
The known problem of this version is that Android kills the application when it is the only application which holds wakelock for a long time.

**1.0.20** - initial release.
