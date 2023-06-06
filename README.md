## Solid FVWM configuration
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/333333.png)

**GREETINGS**  
You've navigated to page, where advanced, original and great FVWM configuration may be downloaded.  
Why is it great?  
1. It is modern and ready to use, so even gnome/kde users won't be missing something. It's containing functionality from modern window managers (including its focus policy) and some unique features. Moreover, it's superior by its usability, stability and speed.  
2. It is lightweight and simple by design, so easily customizable. The whole configuration includes one "icons" directory and three files: "autostart" (sh script with startup applications), "config" (FVWM configuration file) and "exit" (FvwmScript exit dialog). Also, with its relevant and advanced functions, it'll be a great start for new FVWM users as well.  
3. It is great by its appearance, light, integrated look and is theme independent. Initially it was intended to use with Vertex GTK theme (as it was posted on couple of forums couple of years ago, e.g fvwmforums.org), but now it's compatible with every bright or dark Qt/GTK theme you want (I'm using it with numix-gtk-theme now, which is available in most of repositories). Also, no additional images are used in menus or window decorations, straight solid FVWM native decor.  

**Compatible with everything, where FVWM2 may be installed.**
Personally, I recommend to use Devuan (devuan.org) and OpenBSD (openbsd.org), depending on your hardware and use case. Should work with all not too old FVWM2 versions (tested with 2.6+), and also with current FVWM3 version as well (which is still under active development, so should be used more by enthusiasts). I'm using it with FVWM 2.7.0, which was released in the end of 2022 year.  

---

### INSTALLATION  
  
**1.** Install `fvwm` package, then navigate to your home dir and fetch the configuration
```
$ git clone https://github.com/111LUX/FVWM.git
```
**2.** Remove any old FVWM configuration if exists and rename fetched directory
```
$ mv ~/FVWM ~/.fvwm
```
**3.** Install the following packages
```
# apt install xcompmgr stalonetray suckless-tools dzen2
```
* dzen2 is an optional dependency, but with this package installed, you'll get nice notifications with current Desk number, when switching it with Super+F1/F2/F3/F4 (to move window to certain Desk use Super+1/2/3/4) or Super+PgUp/PgDown. Also, it may be used to display sound volume notifications, when changing it with your keyboard/laptop multimedia hotkeys (continue reading to know how).  
* dmenu launcher from "suckless-tools" package will be required, in certain repositories it's packaged simply as "dmenu". For a command history support, additionally download [dmenu_run_history](https://tools.suckless.org/dmenu/scripts/dmenu_run_with_command_history/) script and save it to your _$PATH_ as executable (e.g `# cp dmenu_run_history /usr/local/bin/` and `# chmod +x /usr/local/bin/dmenu_run_history`), then configuration file will use it instead of a regular dmenu as a launcher (Alt+F2).  
* stalonetray is used as a tray application. (Alternatively, it is possible to install `wmsystemtray` package instead, then uncomment two "wmsystemtray" lines at top of ~/.fvwm/config .)
* xcompmgr composition manager configured pretty well via its command line options in configuration file, also it's using server-side shadows — -s flag, which is not commonly used. It fits nicely with overall design, look and feel.  

Few useful additional applications with short description (like fbxkb - tray keyboard layout indicator) are commented in ~/.fvwm/autostart file, install it and uncomment if required. "Files" root menu entry will open your home dir with your default file manager (via xdg-open), I prefer caja or pcmanfm (and engrampa as archive manager), but for file operations I'm using drop down terminal mostly.

**4.** Launch or restart FVWM.  

---

### Embedded drop down applications  
* **Drop down terminal** is available, toggle its visibility with Ctrl+F1 hotkey. No additional actions required, it's working with every screen resolution "out of the box", urxvt terminal emulator will be used if installed, or otherwise xterm. It "remembers" its maximized state even when is hidden (maximize/unmaximize it with Super+W hotkey, or using tiling functionality - Super+Up/Down/Left/Right arrows).  
* **Drop down telegram client** is added too, press Alt+F1 and it will be displayed on left side of screen. "telegram-desktop" executable will be used in your _$PATH_, so make sure it exists, in most cases an installation of `telegram-desktop` package should be enough.  

---

### Xft configuration  
To make Xft fonts similar in size among all applications, to enable its hinting (in modern DEs this part is automatically handled by "settings-daemons"), xft configuration should be added to ~/.Xresources file. [Download my .Xresources](https://raw.githubusercontent.com/111LUX/777/main/.Xresources) and save it to your _$HOME_, while it will be enough to add "Xft" lines, my urxvt and xterm settings are pretty usable too. To apply it, `$ xrdb -merge ~/.Xresources` should be executed, no need to add this command to ~/.fvwm/autostart file, as it is already there.

---

### Keybindings
To iconify (minimize) all applications/restore — ShowDesktop function should be used, it is available via Ctrl+Alt+D, or when pressing dock tray borders (screen bottom left corner click). Icon middle click will close iconified application, window title middle click will maximize/unmaximize window, close title button middle click will kill application. Some other common keybindings: Super+Q - close, Super+A - iconify, Super+C - deiconify previous, Super+W - maximize, Super+D - lower/raise window. Alt+Tab is working as expected, Super+Tab/Super+Shift+Tab - raise and focus next/prev window. All keybindings may be found under "Keybindings" section of ~/.fvwm/config .  

To enable dzen2 sound volume notifications, when using sound media keys, [download vol.sh script](https://raw.githubusercontent.com/111LUX/777/main/vol.sh), save "vol.sh" to your _$PATH_ as executable and restart FVWM.  No further configuration required, as these lines are already present in ~/.fvwm/config :
```
Test (X vol.sh) Key XF86AudioRaiseVolume A A Exec exec vol.sh up
Test (X vol.sh) Key XF86AudioLowerVolume A A Exec exec vol.sh down
```  
  
### Time and date  
![](https://raw.githubusercontent.com/111LUX/SCREENSHOTS/main/0707time.png)  
To view current time and date in bottom right corner of root window, install `conky`, [download .conkyrc.clock file](https://raw.githubusercontent.com/111LUX/777/main/.conkyrc.clock) and save it as ~/.conkyrc.clock . Uncomment `conky -q -c ~/.conkyrc.clock &` line in ~/.fvwm/autostart and it will be automatically started on startup.
