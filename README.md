# Acer Nitro - Enabling Smart Charging via Powershell

After realizing that Nitrosense was eating up almost half a gigabyte of memory while running in the background, I figured I could do better.

So I uninstalled it, consulted [the tomes of wisdom](https://github.com/frederik-h/acer-wmi-battery) and wrote this Powershell script.

It enables the smart charging feature, which limits the charging to 80% on Acer Nitro laptops.

```ps
$bat = get-wmiobject -Namespace "root\wmi" -Class "BatteryControl"
# Battery 1, HEALTH, Enabled, dummy bytes
$bat.SetBatteryHealthControl(1, 1, 1, [byte[]](0, 0, 0, 0, 0))
```

## Side Quest

The RGB keyboard can be controlled via OpenRGB version 0.7.
Also no need for chubby Nitrosense.

Also there are interesting settings in `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OEM\AcerAgentService\LightSetting`

For the keyboard to do this fancy wave animation where it cycles through RGB colors
- KeyBoardArea set to 0x4
- KeyBoardColor set to 0x2
