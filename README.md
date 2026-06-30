# Extension List
- Caffeine[https://extensions.gnome.org/extension/517/caffeine/]
- Desktop Widgets (Desktop Clock)[https://extensions.gnome.org/extension/5156/desktop-clock/]
- Hide Top Bar[https://extensions.gnome.org/extension/545/hide-top-bar/]
- No overview at start-up[https://extensions.gnome.org/extension/4099/no-overview/]
- P7 Borders[https://extensions.gnome.org/extension/9064/p7-window-borders/]
- Window Calls[https://extensions.gnome.org/extension/4724/window-calls/]
- Dash Show[https://extensions.gnome.org/extension/9055/dash-show/]

# Extension Configure
1) Desktop Widgets (Desktop Clock)
  - Digital Clock Widget -> Widget Location -> X Position: **92.0** / Y Position: **0.5**
  - Time Label -> Data/Time Format: **%H∶%M** / Font Size: **42**
  - Date Label -> Date/Time Format: **%m월 %d일 (%a)** / Font Size: **18**
2) Hide Top Bar
  - Show panel when mouse approaches edge of the screen -> **false**
  - Show panel in overview -> **false**
3) P7 Borders
  - Enable by default -> **true**
  - Rounded corners -> **true**
  - Active border color -> **#FFB6B9**
  - Inactive border color -> **#BEEBE9**

# User Script for Gnome
1) ${HOME}/.local/bin/switch_window.sh
- It works the same as Alt+Esc. I applied this simply for faster shortcut usage.
```
#!/bin/sh

TARGET_WINID=$(gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell/Extensions/Windows --method org.gnome.Shell.Extensions.Windows.List | sed 's/,/\n/g' | grep id\": | grep -v pid | awk -F ':' '{print $2}' | head -n 1)

if [[ z${TARGET_WINID} != "z" ]]
then
	gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell/Extensions/Windows --method org.gnome.Shell.Extensions.Windows.Activate ${TARGET_WINID} > /dev/null 2>&1
fi
```
- Add gnome user shortcut
  - Name : **Switch Window**
  - command : **${HOME}/.local/bin/switch_window.sh**
  - Shortcut : **Super + w**
2) ${HOME}/.local/bin/dash_show_setting.sh
- It replaces the standalone launcher program.
```
#!/bin/sh

CURRENT_STATUS=`LANG=C gnome-extensions info dash-show@BryanMaker | grep State | awk '{print $2}'`


if [[ ${CURRENT_STATUS} == "ACTIVE" ]]
then
	gnome-extensions disable dash-show@BryanMaker
else
	gnome-extensions enable dash-show@BryanMaker
fi
```
- Add gnome user shortcut
  - Name : **Change dash-to-dock Autohide Setting**
  - command : **${HOME}/.local/bin/dash_show_setting.sh**
  - Shortcut : **Super + d**

# Gnome Config
- Disable Wallpaper
```
dconf write /org/gnome/desktop/background/picture-options "'none'"
```
- backgroud color set black
```
dconf write /org/gnome/desktop/background/primary-color "'#000000'"
dconf write /org/gnome/desktop/background/secondary-color "'#000000'"
```

# My Gnome Desktop

![ScreenShot](https://raw.githubusercontent.com/kappa-k0801/My_Gnome_Configure/main/8986579575.png)
