# USB Audio for DX200
This application switches iBasso DX200 audio processor (XMOS chip) into USB DAC mode, accessible for Android applications, installed on this DX200 itself! When **USB Audio for DX200** starts the USB DAC Interface, any compatible Android music player application, that supports and is configured to use a USB DAC, will play bit perfect audio, including DSD! For DSD, it supports both Native and DoP modes, and even DoP-encoded PCM formats, e.g. in flac.

Don't like Mango, or it does not suit your needs? Just forget about it, and use USB Audio Player PRO, or Hiby Music, fully utilizing the great hardware of DX200! The startup screen of **USB Audio for DX200** has listed compatible applications, along with the required settings.

**Please note:** When Mango plays DSD tracks, it switches XMOS chip into USB DAC mode. Avoid playing DSD in Mango in Android, if you have configured UAPP/Hiby/Neutron to auto-start when USB DAC is attached! They will fight for the access to USB DAC with Mango.

**Warning:** Avoid having installed and configured for USB DAC playback more than one application at a time! They tend to autolaunch on a device attached, and you'll have a mess, that may lead to conflicting system volume settings, that may damage your ears or headphones!

**Known problem:** During playback of tracks with 44.1KHz sampling rate, short cracking noise may appear time to time, with several seconds, or even minutes, in between. The reason is still unknown, and there is no a way to avoid it. It happens with all the players tested, and does not happen on any other sample rate, including DSD.

## History of public releases
**1.0.35** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.2.110 Rev.1:
* ***Active player*** - choose the music player application that you currently use most of time, even if you have only one USB Audio compatible player. If there are more than one recognized players, the application hides other players (they are still visible in Android Settings-Apps menu), and, on USB device attached event, grants access to the USB device without questions and launches the player chosen. This eliminates possible conflicts and simplifies the use. If you want all your players back, select *I'll control it myself!* and tap OK.
* ***Battery saver*** is improved: it stops 4 out of 8 CPU kernels, and stops Media Scanner.
* The notification bar now contains information about current application state, displays number of detected wakelocks (right bottom corner, including its own wakelock), and idle time chronometer.
* If the interface was detached due to doze mode, it is not restarted immediatelly once the screen is turned on: it waits for around 5 seconds before initiates restart. This allows to only take a look to the lock screen, or keeps the interface from unneeded restart in case a background service turns the display on for a moment.
* Many other fixes and improvements.

**1.0.30** - only available in [custom firmware builds](https://github.com/Lurker00/DX200-firmware) starting from 2.2.110:
* ***Smart release of WakeLock*** menu setting added, with corresponding ***Idle Timeout*** value.
With this (and _Acquire WakeLock_) setting turned on, the application tries to detect that no a known music player actually use the USB DAC, by checking wakelocks from other processes. If no a know wakelock found for the timeout period, the application releases its own wakelock, letting Android to enter doze mode.
* ***Battery saver*** menu option added, which turns on Android Battery Saver mode when the interface is active. It does not actually save much battery, because the main consumers are DAC and amp. But it does reduce background activity of Android and Google stuff.
* ***CPU Turbo Mode*** menu option added. Turn it on, if music can't be played when the display is turned off. For instance, playback of SACD ISO images encoded with DST requires a lot of CPU power. When display turns off, Android on DX200 stops 7 from 8 CPU cores. Turbo Mode keeps 3 additional cores (to 4 total) from stopping. If _Acquire WakeLock_ and _Smart Release_ are enabled, the cores are made available for stopping during smart release period. Turbo Mode is activated on application start, even if the interface is not started. This allows to use MangoPlayer in Turbo mode as well, but be careful: smart  release does not work when the interface is not started!

These features require either SuperSU installed, or permissions available only for pre-installed applications. This restriction makes no sense to make new versions for the stock firmware anymore.

**1.0.23** - The problem of 1.0.22 has been solved: with wakelock acquired, it is not killed, and stays until turned off manually, or while the battery lasts, whatever is sooner.

**1.0.22**:
* ***Exit*** button moved to 3-dots menu. The options are in the menu as well.
* Optional ***Acquire WakeLock*** to prevent interface shutdown in doze mode. **Note**: don't forget to stop interface when idle!
* Optional ***Autostart*** to start the interface without the need to push _Start_ button.
The known problem of this version is that Android kills the application when it is the only application which holds wakelock for a long time.

**1.0.20** - initial release.

## FAQ
**Q**: Is it safe to run DX200 in this mode?<br />
**A**: Actually, Mango on both DX80 and DX200 uses this mode to playback DSD. So, yes - it is safe!

**Q**: Do I need a special/custom firmware build, or a root access, or anything else special?<br />
**A**: The basic functionality works with any stock firmware. Advanced features added in 1.0.24+ versions require it to be a part of the custom firmware.

**Q**: Why XXX application is not compatible, but perfectly deals with an external USB DAC?<br />
**A**: I don't know the exact reason, but, most probably, this is due to misuse of the volume controls, which leads to damaged bit stream output to this USB DAC.

**Q**: PCM formats sound OK, but with DSD I hear only a noise! What's wrong?<br />
**A**: Check software volume control in your player application and be sure it is set to 100%.

**Q**: Where is my internal storage in USB Mass Storage mode? The second disk is not inserted!
**A**: USB Mass Storage provides direct access to a real disk. The user visible internal storage is actually a folder of the internal disk (flash partition formatted with ext4). Though it is possible to export this whole partition, and ext4-aware OS (Linux) recognizes it, it has a little sense, because access rights keep the iternal storage directory out of reach anyway. Changing (accidentally or intentionally) these access rights will ruin DX200.
