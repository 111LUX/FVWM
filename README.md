![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/333.png)

**GREETINGS & CONGRATULATIONS**  
You've navigated to page, where advanced, original and great FVWM configuration may be downloaded.  
Why is it great?  
1. It is modern and ready to use, so even users of modern desktop environments won't be missing something. It's containing functionality from modern window managers (including its focus policy) and some unique features. Moreover, it's superior by its usability, stability and speed.  
2. It is lightweight and simple by design, so easily customizable. The whole configuration includes one "icons" directory and three files: "autostart" (sh script with startup applications), "config" (FVWM configuration file) and "exit" (FvwmScript exit dialog). Also, with its relevant and advanced functions, it'll be a great start for a new FVWM user as well.  
3. It is great by its appearance, light, integrated look and is theme independent. Initially it was intended to use with Vertex GTK theme (as it was posted on couple of forums couple of years ago), but now it's compatible with every bright or dark Qt/GTK theme you want (e.g numix-gtk-theme in package repositories).

**Compatible with everything, where FVWM2/3 may be installed.**
Personally, I recommend to use Devuan (devuan.org) and OpenBSD (openbsd.org), depending on your hardware and use case. Should work with all not too old FVWM2 versions (tested with 2.6+) and also with FVWM3 as well.  

### WARNING !  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/noicons.png)  
**Since new Xlib version was introduced, which is in use in Debian stable (bookworm) and newer distros, annoying bug appeared** (in such distros with new Xlib): icons of iconified applications may dissapear sometimes randomly and always on FVWM restart. And by the end of 2024 it is not fixed yet in both FVWM 2/3 versions. As a workaround solution, for FVWM 2 version: apply xthread_fix.patch — https://github.com/fvwmorg/fvwm3/issues/818#issuecomment-1710549061 and siebenmann's patch — https://github.com/fvwmorg/fvwm3/issues/818#issuecomment-1401144381 to fvwm2 source code and then build it and install. For all FVWM 3 versions prior to 1.1.0 it is possible to apply siebenmann's patch too (xthread_fix.patch is not needed). 

---

### INSTALLATION  
  
**1.** Install the `fvwm` package, then navigate to your home dir and fetch the configuration
```
$ git clone https://github.com/111LUX/FVWM.git
```
**2.** Remove any old FVWM configuration if exists and rename fetched directory  
(FVWM may create empty ~/.fvwm directory with its first launch, so remove it `$ rmdir ~/.fvwm`)
```
$ mv ~/FVWM ~/.fvwm
```
**3.** Install the following packages
```
# apt install xcompmgr stalonetray suckless-tools dzen2
```
* _dzen2_ is an optional dependency, but with this package installed, you'll get nice top screen notifications with current Desk number, when switching it with Super+F1/F2/F3/F4 (to move window to certain Desk use Super+1/2/3/4) or Super+PgUp/PgDown. Also, it may be used to display sound volume notifications too, when changing it with your keyboard/laptop multimedia hotkeys (read bellow).  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/dzen.png)  

* _dmenu_ launcher from "suckless-tools" package will be required, in certain repositories it's packaged simply as `dmenu`. For a command history support, additionally download [dmenu_run_history](https://tools.suckless.org/dmenu/scripts/dmenu_run_with_command_history/) script and save it to your _$PATH_ as executable (e.g `# cp dmenu_run_history /usr/local/bin/` and `# chmod +x /usr/local/bin/dmenu_run_history`), then configuration file will use it instead of a regular dmenu as a launcher (Alt+F2).  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/dmenu_run.png)  

* _stalonetray_ is used as a tray application. FvwmButtons module is launching it at bottom left screen corner before icons. Alternatively, it is possible to replace `stalonetray` with `wmsystemtray` package (read bellow).  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/dock.png)  

* _xcompmgr_ compositing manager configured pretty well via its command line options in configuration file, also it's using server-side shadows — -s flag, which is not commonly used. It fits nicely with overall design, look and feel. (Alternatively, use `compton` with this [~/.config/compton.conf](https://raw.githubusercontent.com/111LUX/777/main/compton.conf) and remove "xcompmgr" lines from config/autostart files.)   
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/screenshot.png)  

Few useful additional applications with short description (like fbxkb - tray keyboard layout indicator) are commented in ~/.fvwm/autostart file, install it and uncomment if required. "Files" root menu entry will open your home dir with your default file manager (via xdg-open), I prefer caja (and engrampa as archive manager), but for file operations I'm using drop down terminal mostly.  

**4.** Start or restart FVWM.  

---

### Embedded drop down applications  
* **Drop down terminal** is available, toggle its visibility with Ctrl+F1 hotkey. No additional actions required, it's working with every screen resolution "out of the box", urxvt terminal emulator will be used if installed, or otherwise xterm. It "remembers" its maximized state even when is hidden (maximize/unmaximize it with Super+W hotkey, or using tiling functionality - Super+Up/Down/Left/Right arrows).  
* **Drop down telegram client** is added too, press Alt+F1 and it will be displayed on left side of screen. "telegram-desktop" executable will be used in your _$PATH_, so make sure it exists, in most cases an installation of `telegram-desktop` package should be enough. (_This is added not because I'm a huge fan of this software or because they pay me, but as I'm using it to communicate with some regular people, and found it useful as a drop down app, it may be useful for someone else too. If you're not using it, it'll be enough to remove Alt+F1 keybinding in config:_ `Key F1 A M DropDown telegram-desktop...`)  

---

### Xft configuration  
To make Xft fonts similar in size among all applications, to enable its hinting (in modern DEs this part is automatically handled by "settings-daemons"), Xft configuration should be added to ~/.Xresources file. [Download my .Xresources](https://raw.githubusercontent.com/111LUX/777/main/.Xresources) and save it to your _$HOME_, while it will be enough to add "Xft" lines, my urxvt and xterm settings are pretty usable too. To apply it, `$ xrdb -merge ~/.Xresources` should be executed, no need to add this command to ~/.fvwm/autostart file, as it is already there.  

---

### Keybindings  
To iconify (minimize) all applications/restore — ShowDesktop function should be used,  
it is available via Ctrl+Alt+D, or when pressing dock tray borders (screen bottom left corner click).  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/showdesktop.gif)  

Icon middle click will close iconified application, window title middle click will maximize/unmaximize window, close title button middle click will kill application. Some other common keybindings: Super+Q - close, Super+A - iconify, Super+C - deiconify previous, Super+W - maximize, Super+D - lower/raise window. Alt+Tab is working as expected, Super+Tab/Super+Shift+Tab - raise and focus next/prev window. All keybindings may be found under "Keybindings" section of ~/.fvwm/config .  

To enable **dzen2 sound volume notifications**, when using laptop/keyboard sound volume media keys, [download vol.sh script](https://raw.githubusercontent.com/111LUX/777/main/vol.sh), save "vol.sh" to your _$PATH_ as executable and restart FVWM.  No further configuration required, as these lines are already present in ~/.fvwm/config :  
```
Test (X vol.sh) Key XF86AudioRaiseVolume A A Exec exec vol.sh up
Test (X vol.sh) Key XF86AudioLowerVolume A A Exec exec vol.sh down
```  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/pulsevol.png)  
Script uses ALSA backend to change volume, to use PulseAudio instead, download [download vol.sh_pulse](https://raw.githubusercontent.com/111LUX/777/main/vol.sh_pulse) and save it as "vol.sh" to your _$PATH_ as executable, it uses `pulsemixer` package to get sound volume, so it is required (on some systems it should be replaced with `pamixer`).  

---

### Local variables  
Several local FVWM variables are set at top of config file. Such variables store information about **default FVWM font**, **title font**, **tray application** and **terminal emulator** (only xterm or urxvt are supported, as it's supporting "-name" flag, required for DropDown function to work with terminal). When changing these variables, it will be changed in whole config.  
```
# Store information in local variables
InfoStoreAdd font 'Shadow=1:xft:Sans:size=10'
InfoStoreAdd titlefont 'Shadow=1:xft:Sans:size=10:bold'
InfoStoreAdd tray stalonetray
InfoStoreAdd traycommand 'stalonetray -bg "#333333" --geometry 2x2 --max-geometry 2x2 --scrollbars horizontal --scrollbars-size 3 --dockapp-mode simple --kludges force_icons_size'
Test (X urxvt) InfoStoreAdd terminal urxvt
Test (!X urxvt) InfoStoreAdd terminal xterm
```

"tray" and "traycommand" variables are setting tray application. By default stalonetray will be launched automatically with FVWM, and when any tray application will be started (like telegram-desktop), its icon will appear in bottom left corner.  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/wmsystemtray.png)  
Also, it is possible to **replace stalonetray with wmsystemtray tray application**,  
just replace "InfoStoreAdd tray" and "InfoStoreAdd traycommand" lines,  
kill stalonetray `$ pkill stalonetray` and restart FVWM.  
```
InfoStoreAdd tray wmsystemtray
InfoStoreAdd traycommand 'wmsystemtray --non-wmaker'
```
   
**To change FVWM fonts**, replace "font" and "titlefont" variables with fonts of your choice, for example:  
```
InfoStoreAdd font 'Shadow=1:xft:Liberation Sans:size=10'
InfoStoreAdd titlefont 'Shadow=1:xft:Liberation Sans:size=11:bold'
```
---

### Time and date  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/0707time.png)  
To view current time and date in bottom right corner of root window, install `conky`, [download .conkyrc.clock file](https://raw.githubusercontent.com/111LUX/777/main/.conkyrc.clock) and save it as ~/.conkyrc.clock . Uncomment `conky -q -c ~/.conkyrc.clock &` line in ~/.fvwm/autostart and it will be automatically started on FVWM startup.

---

### Title buttons  
As for example, it's possible to use 3 types of title buttons:  
1. Vector buttons, using FVWM "Vector" "ButtonStyle" (default).
2. Title buttons from [Vertex GTK theme](https://github.com/horst3180/vertex-theme).
3. Title buttons from A23D textures resource [a23d.co - glass/mirror](https://www.a23d.co/product-category/textures/glass/mirror/) (their permission to use it in this config is granted).  

To choose it, comment and uncomment appropriate "title buttons" section in the config:
```
# Vector title buttons
#ButtonStyle 1 Vector 5 25x40@1 25x60@1 75x60@0 75x40@0 25x40@1 -- Flat
#ButtonStyle 3 Vector 5 40x40@1 60x40@1 60x60@0 40x60@0 40x40@1 -- Flat
#ButtonStyle 5 Vector 5 25x25@1 25x75@1 75x75@0 75x25@0 25x25@1 -- Flat
#ButtonStyle All ActiveDown -- !Flat

# Vertex title buttons
ButtonStyle All Pixmap v_button.png -- Flat
ButtonStyle 1 ActiveDown Pixmap v_button_close.png -- Flat
ButtonStyle 3 ActiveDown Pixmap v_button_iconify.png -- Flat
ButtonStyle 5 ActiveDown Pixmap v_button_maximize.png -- Flat

# Mirror title buttons
#ButtonStyle All ActiveUp Pixmap m_button_focus.png -- Flat
#ButtonStyle All ActiveDown Pixmap m_button_press.png -- Flat
#ButtonStyle All Inactive Pixmap m_button_unfocus.png -- Flat
```
Also, it's possible to changle title bar height (in pixels):
```
TitleStyle Centered Height 30
```  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/titlebuttons1.png)  

![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/titlebuttons2.png)  

![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/titlebuttons.png)


---

### Customizing colors
Colors may be easily changed using colorsets section of ~/.fvwm/config file.
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/222.png)  
To achieve similar decorations as on screenshot above, these lines should be added/edited:
```
Style * BorderWidth 2, HandleWidth 2
TitleStyle Centered Height 28
TitleStyle Active DGradient 999 4 #111111 10 #141414 40 #822CA9 30 #FFC137 20 #FF3D29
```  
```
# Colorset <number> background, foreground, foreground shadow
Colorset 111 bg #111111, fg white, fgsh black
Colorset 333 bg #333333, fg white, fgsh black
Colorset 666 bg #666666, fg white, fgsh black
Colorset 777 bg #777777, fg #e7e7e7, fgsh black
# Set colorsets
Style * HilightColorset 111, IconBackgroundColorset 666, Colorset 777
Style * HilightBorderColorset 111, BorderColorset 777
MenuStyle * MenuColorset 333, TitleColorset 333, ActiveColorset 111
```
