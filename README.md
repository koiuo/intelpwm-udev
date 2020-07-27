# intelpwm-udev

`intelpwm` script sets backlight PWM frequency for some generations of i915 GPU on linux (tested on Sandy Bridge).

It expects config file to live in `/etc/intelpwm.conf` with a content like this:

```
FREQ=800
```

The script assumes Sandy Bridge and has not been tested on GPUs from other generations. To avoid unexpected behavior,
the script will refuse to work if `intel_reg` utility does not report register with mnemonic names this script exepects.

If it is known that the script should work even if the names of the registers do not match, it is possible to force
the script to work by explicitly specifying registers names or offsets. In `/etc/intelpwm.conf` add:

```
PCH_RAWCLK_FREQ_REG=0xc8254
BLC_PWM_PCH_CTL2_REG=0xc6204
```

`intelpwm` script can be invoked directly (for testing purposes) or via a supplied udev rule to set PWM frequency effectively
permanently. In the latter case, either udev rule has to specify an absolute path to `intelpwm`, or the script must live
in `/usr/lib/udev` (double check with udev man page of your distribution).

The udev rule should usually live in `/etc/udev/rules.d/` or `/usr/lib/udev/rules.d/` (double check with udev man page).

## Dependencies

The script requires `intel_reg` utility from the http://cgit.freedesktop.org/xorg/app/intel-gpu-tools/ to be in `PATH`.

