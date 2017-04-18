# USB Audio for DX200
This application switches iBasso DX200 audio processor (XMOS chip) into USB DAC mode, accessible for Android applications, installed on this DX200 itself! When **USB Audio for DX200** starts the USB DAC Interface, any compatible Android music player application, that supports and is configured to use a USB DAC, will play bit perfect audio, including DSD! For DSD, it supports both Native and DoP modes, and even DoP-encoded PCM formats, e.g. in flac.

Don't like Mango, or it does not suit your needs? Just forget about it, and use USB Audio Player PRO, or Hiby Music, fully utilizing the great hardware of DX200! The startup screen of **USB Audio for DX200** has listed compatible applications, along with the required settings.

**Please note:** such applications are not aware that the volume control of DX200 _is the volume control_ of the USB DAC they use! It may lead to distorted, or too loud sound! Look into the particular application setting to find a way to disable using volume control at all.

**Warning:** Avoid having installed and configured for USB DAC playback more than one application at a time! They tend to autolaunch on a device attached, and you'll have a mess, that may lead to conflicting system volume settings, that may damage your ears or headphones!

## History
**1.0.23** - The problem of 1.0.22 has been solved: with wakelock acquired, it is not killed until turned off manually, or while the battery lasts, whatever is sooner.<br />
**1.0.22**:
* _Exit_ button moved to 3-dots menu. The options are in the menu as well.
* Optional _Acquire WakeLock_ to prevent interface shutdown in doze mode. **Note**: don't forget to stop interface when idle!
* Optional _Autostart_ to start the interface without the need to push _Start_ button.
The known problem of this version is that Android kills the application when it is the only application which holds wakelock for a long time.<br />
**1.0.20** - initial release.

## FAQ
**Q**: Is it safe to run DX200 in this mode?<br />
**A**: Actually, Mango on both DX80 and DX200 uses this mode to playback DSD. So, yes - it is safe!

**Q**: Do I need a special/custom firmware build, or a root access, or anything else special?<br />
**A**: No, it works with any stock firmware.

**Q**: Why XXX application is not compatible, but perfectly deals with an external USB DAC?<br />
**A**: I don't know the exact reason, but, most probably, this is due to misuse of the volume controls, which leads to damaged bit stream output to this USB DAC.

**Q**: PCM formats sound OK, but with DSD I hear only a noise! What's wrong?<br />
**A**: Check software volume control in your player application and be sure it is set to 100%.
