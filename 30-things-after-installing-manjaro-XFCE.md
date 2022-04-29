# 30 things to do After Installing Manjaro XFCE (2021)

**Manjaro paired with XFCE strikes a great  combination of Arch user experience and lightweight but powerful XFCE  desktop environment. In this post, we’ll be taking a look at 30 things  you can do after installing Manjaro XFCE.**

## Content

1. [Backup](https://averagelinuxuser.com/manjaro-xfce-after-install/#1-backup)
2. [Install Drivers](https://averagelinuxuser.com/manjaro-xfce-after-install/#2-install-drivers)
3. [Switch to local mirror](https://averagelinuxuser.com/manjaro-xfce-after-install/#3-switch-to-local-mirror)
4. [Enable AUR](https://averagelinuxuser.com/manjaro-xfce-after-install/#4-enable-aur)
5. [Install popular apps](https://averagelinuxuser.com/manjaro-xfce-after-install/#5-install-popular-apps)
6. [Automatic Date and Time](https://averagelinuxuser.com/manjaro-xfce-after-install/#6-automatic-date-and-time)
7. [Reduce swappiness](https://averagelinuxuser.com/manjaro-xfce-after-install/#7-reduce-swappiness)
8. [Enable Firewall](https://averagelinuxuser.com/manjaro-xfce-after-install/#8-enable-firewall)
9. [Install Microsoft Fonts](https://averagelinuxuser.com/manjaro-xfce-after-install/#9-install-microsoft-fonts)
10. [Enable TRIM for SSD](https://averagelinuxuser.com/manjaro-xfce-after-install/#10-enable-trim-for-ssd)
11. [Install Redshift](https://averagelinuxuser.com/manjaro-xfce-after-install/#11-install-redshift)
12. [Consider LTS kernel](https://averagelinuxuser.com/manjaro-xfce-after-install/#12-consider-lts-kernel)
13. [Terminal Settings](https://averagelinuxuser.com/manjaro-xfce-after-install/#13-terminal-settings)
14. [Firefox Settings](https://averagelinuxuser.com/manjaro-xfce-after-install/#14-firefox-settings)
15. [Install Google Chrome](https://averagelinuxuser.com/manjaro-xfce-after-install/#15-install-google-chrome)
16. [Install Password Manager](https://averagelinuxuser.com/manjaro-xfce-after-install/#16-install-password-manager)
17. [Install Language packages](https://averagelinuxuser.com/manjaro-xfce-after-install/#17-install-language-packages)
18. [Extend spell checking](https://averagelinuxuser.com/manjaro-xfce-after-install/#18-extend-spell-checking)
19. [Add Keyboard layouts](https://averagelinuxuser.com/manjaro-xfce-after-install/#19-add-keyboard-layouts)
20. [Xkill shortcut](https://averagelinuxuser.com/manjaro-xfce-after-install/#20-xkill-shortcut)
21. [Clipboard Manager Settings](https://averagelinuxuser.com/manjaro-xfce-after-install/#21-clipboard-manager-settings)
22. [Improve menu](https://averagelinuxuser.com/manjaro-xfce-after-install/#22-improve-menu)
23. [Change desktop themes](https://averagelinuxuser.com/manjaro-xfce-after-install/#23-change-desktop-themes)
24. [User image](https://averagelinuxuser.com/manjaro-xfce-after-install/#24-user-image)
25. [Test Webcam and Microphone](https://averagelinuxuser.com/manjaro-xfce-after-install/#25-test-webcam-and-microphone)
26. [Enable Flatpak/Snap](https://averagelinuxuser.com/manjaro-xfce-after-install/#26-enable-flatpaksnap)
27. [Turn off startup apps](https://averagelinuxuser.com/manjaro-xfce-after-install/#27-turn-off-startup-apps)
28. [Remove some apps](https://averagelinuxuser.com/manjaro-xfce-after-install/#28-remove-some-apps)
29. [Check for errors](https://averagelinuxuser.com/manjaro-xfce-after-install/#29-check-for-errors)
30. [Clean system](https://averagelinuxuser.com/manjaro-xfce-after-install/#30-clean-system)

<iframe src="https://www.youtube.com/embed/jl4nyEA-F-o" allowfullscreen="" width="720" height="480">
  </iframe>

​    

## 1. Backup

The first thing that we’ll be taking a look at is configuring the backup of data. Accidents happen. Whether you are a regular user, developer or simply Linux enthusiast, your data is valuable to you and needs to be secured.

Fortunately, Manjaro XFCE has a pre-installed backup application - **Timeshift**. The app has a functionality similar to *Restore feature* in Windows and the *Time Machine* tool in macOS. Timeshift performs **incremental snapshots** of the file system  **at user-defined intervals**.

Upon opening the Timeshift, you’ll probably notice the *Wizard* button in the top right side of the app. As the name suggests, this is a user-friendly way of configuring backup.

Run *Wizard* and follow these steps:

1. Snapshot Type

   .   

   - select RSYNC

2. Snapshot Location

   .    

   - Select the disk where you would like your snapshots to be stored.

3. Snapshot Levels

   .    

   - You can choose how many snapshots Timeshift will perform/store on a monthly, weekly, daily, hourly and boot basis

4. User home directories

   .    

   - Allows you to decide which folders Timeshift will back up. You should prioritize your home directory, but depending on your space, it  won’t hurt to include */root* directory as well.

That’s it for Timeshift! In case you accidentally loss your data, open Timeshift, click *Restore*, select a snapshot which contains the files that you would like to recover and voila - your world is bright again.

![Timeshift system snapshot.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/1-timeshift.jpg)

## 2. Install Drivers

After distros and desktop environments, drivers are probably the most controversial topic in the Linux community. Luckily, Manjaro XFCE has a nifty **Hardware Configuration** section in **Manjaro Settings Manager** which will detect and recommend the drivers for your system.

The app will show you the two options:

- Auto Install Proprietary Driver
- Auto Install Open-source Driver

For a **regular user**, I would recommend **proprietary** drivers.

More often than not, they work better than their open-source counterparts. You can also install each driver individually by *Right-clicking* on it which will show a pop-up with *Install* entry.

In addition to installing drivers, *Hardware Configuration* section has a *Show all devices* option which allows you to view information about the hardware your Manjaro XFCE runs on.

![Manjaro drivers recommendation.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/2-install-drivers.jpg)

## 3. Switch to local mirror

In computer network jargon, a *mirror* is simply a fancy word for a server holding the same data (copy) as the original server. This data is your distro updates and software available to download.

By default, Manjaro uses a global mirror to perform updates and software installations. As you might guess, the global mirror is not as fast as a local mirror.

To switch to a local mirror, Open **Pamac** → ⋮ (three dots menu) → Preferences → Official Repositories → Use mirrors from: {select your country or the nearest country to yours} → Refresh Mirrors List.

![Manjaro local mirror set to Sweden.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/3-local-mirror.jpg)

## 4. Enable AUR

Even if this is the first time for you using an Arch-based distro, you have likely heard of AUR before.

**AUR (Arch User Repository)** is a community-driven repository for Arch-based Linux distro users. Community distributes new packages in AUR. If they become popular enough, they end up in the official repository.

To enable AUR, Open **Pamac** → ⋮ (three dots menu) → Preferences → AUR → Turn on *Enable AUR Support* & *Check for updates*

![Enabling AUR in Pamac.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/4-enabling-aur.jpg)

## 5. Install popular apps

After enabling AUR, the next logical step would be to install some AUR apps, right? Here are the apps/packages I installed:

- zoom
- spotify
- skypeforlinux-stable-bin

You just need to select an app you would like to install, and *Pamac* will build and install it for you.

![Installing skype via Pamac.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/5-install-popular-apps.jpg)

## 6. Automatic Date and Time

Date and time on Manjaro can behave strangely and may not be accurate as discussed in [this thread](https://www.linux.org/threads/weird-clock-time-related-problems-in-manjaro.28175/).

To make sure that the system always displays the correct date and time, we need to enable the date and time synchronization.

Open Manjaro Settings → Time and Date → Check *Set time and date automatically* → Apply.

## 7. Reduce swappiness

[Swappiness](https://averagelinuxuser.com/linux-swap/) is the kernel parameter (0 - 100) that defines how much and how often Linux should copy RAM content to the disk.

Reducing swappiness value forces the system to use as much RAM as possible instead of swap storage. The main benefit of reducing the swap usage is that it reduces the number of writes to your hard drive resulting in better system performance.

Check the current swappiness value by executing:

```
cat /proc/sys/vm/swappiness # 60 (default)
```

Reduce the swap usage to 10:

```
sudo echo "vm.swappiness=10" > /etc/sysctl.d/100-manjaro.conf
```

Now reboot your system and check the swappiness value:

```
cat /proc/sys/vm/swappiness # 10
```

## 8. Enable Firewall

Linux community loves to brag about how secure Linux is. To some extent, this is true, but that’s not to say that there are no threats to Linux users. Therefore, it is advisable to enable a firewall to protect you against network intrusions.

**Firewall** is a pre-installed app on Manjaro that allows us to configure the network firewall. Open the app and toggle *Status* checkbox to activate it.

If you wish to learn more about network firewall and some advanced configurations, check out [my article on Linux firewall](https://averagelinuxuser.com/linux-firewall/).

![Network firewall enabled on Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/8-firewall.jpg)

## 9. Install Microsoft Fonts

Microsoft offers a wide range of fonts on Windows. Some notable ones include ***Times New Roman, Comic Sans, Arial\*** which are pretty much standard in documents. To install Microsoft fonts on Linux, Open **Pamac** → Search for *ttf-ms-fonts* → Build → Apply.

## 10. Enable TRIM for SSD

TRIM is an essential service for all Linux users on SSD. TRIM optimizes the performance and ensures the longevity of your SSD by minimizing write amplification.

Manjaro does not have TRIM enabled by default like other Linux distributions (Ubuntu, Linux Mint). We need to enable it manually.

To check the status of TRIM service run:

```
sudo systemctl status fstrim.timer # disabled; inactive (default)
```

Enable TRIM by running:

```
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

## 11. Install Redshift

**Redshift** is a Linux application for protecting your eyes by reducing the amount of blue light at night.

Open **Pamac** → Search for *redshift* → Build → Apply.

![Installing Redshift in Pamac Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/11-install-redshift.jpg)

After the **Redshift** installation, it will appear in your system tray. Click on the **Redshift** icon and make sure that it is *Enabled* & runs on *Autostart*.

No further configuration required, Redshift will handle the rest automatically.

## 12. Consider LTS kernel

One of the main reasons why Arch & Arch-based distros have gotten popular is that users are always up to date and have the latest software. While  being up to date has its advantages, it can also cause instability of the system.  This statement especially applies to the kernel. You can sacrifice some new  features but minimize the risk of instability by running the LTS kernel.

To **install the LTS kernel** version, open *Manjaro Settings Manager** → Kernel → Choose the latest LTS flagged kernel → Install*.

![Installing LTS kernel on Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/12-lts-kernel.jpg)

Then you need to **enable GRUB menu** to be able to boot this new LTS kernel.

Open the GRUB settings:

```
sudo mousepad /etc/default/grub
```

Change `GRUB_TIMEOUT_STYLE=hidden` to `GRUB_TIMEOUT_STYLE=menu` and save the file.

Next, regenerate GRUB config by running:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

Reboot your system, and you should see this GRUB menu:

![Manjaro GRUB menu](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/12-grub.jpg)

Go to **Advanced options** and **select the LTS kernel** which you have just installed.

Then go to Manjaro Settings Manager → Kernel → make sure your LTS kernel has the status “Running” → **remove all non-LTS kernels**.

After you have configured your system to run the LTS kernel, you can edit the GRUB settings to **disable the GRUB delay**. You just need to set `GRUB_TIMEOUT=0` in `/etc/default/grub` and re-run `grub-mkconfig` as shown above.

## 13. Terminal Settings

Default Manjaro’s XFCE terminal style may not be everyone’s cup of tea. Reduced opacity and top menu toolbar can be distracting.

To tweak opacity, Open **Terminal** → Right-click → Preferences → Appearance → Drag opacity slider to 1.00 (solid background color).

To disable/enable toolbar, Right-click → Toggle *Menu Toolbar*.

These simple adjustments should make your terminal more appealing.

![Manjaro XFCE terminal with solid background and without top menu toolbar.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/13-terminal-settings.jpg)

## 14. Firefox Settings

How many times have you accidentally closed your browser and lost all your tabs? If you are like me, it happens ever so often. To make sure that Firefox restores your last browser session every time you launch a browser, Open **Firefox** → Options (hamburger menu) → Preferences → Enable *Restore previous session.*

Another useful feature is to enable DRM content. You may find yourself unable to play some videos (e.g. Netflix) or audio because of DRM restriction. To enable DRM content, Open **Firefox** → Options (hamburger menu) → Preferences → Enable *Play DRM-controlled content*

The last setting is related to Firefox’s search bar. Let’s say you search for a particular email address. Firefox will open your default email client, instead of performing a web search. This functionality can certainly be annoying.

To change the search bar, Open **Firefox** → Options (hamburger menu) → Preferences → Search tab → Select *Add search bar in toolbar*

You can also customize the toolbar with Right-click on toolbar → Customize.

These were small wins that should make your browsing experience a little bit better.

![Firefox settings for better browsing experience.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/14-firefox-settings.jpg)

## 15. Install Google Chrome

Firefox is a default Linux browsers on many Linux distributions. Still, many users are used to the functionality and look of Google Chrome. If you are one of them, fear not, Google Chrome is available in AUR.

To install Google Chrome, Open **Pamac** → Search for *google-chrome* → Build (google-chrome package) → Apply.

## 16. Install Password Manager

A password manager is an essential app for every computer user. Manjaro XFCE does not come with a password manager out of the box. To install one (KeePassXC in my case), Open **Pamac** → Search for *keepassxc* → Build → Apply.

You will be prompted with a window asking you to choose display server your system is using. It’s likely X server, but if you are not sure, type:

```
ps -e | grep tty # Xorg -> X server
```

After the installation, open **KeePassXC**. Click on *Create new database*, confirm default settings and enter the master password. To create a password, click on the *+* button on the top menu bar and fill in the required details.

The next time you want to use your credentials, open KeePassXC, right-click on the desired entry and copy your username and password.

![Copying credentials in KeePassXC password manager.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/16-password-manager.jpg)

## 17. Install Language packages

Manjaro doesn’t install all language packages by default. I would recommend you to install additional language packages to have a better desktop experience.

Open **Manjaro Settings Manager** → Language Packages → Install Packages.

![Installing language packs on Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/17-language-packs.jpg)

## 18. Extend spell checking

In addition to language packages, I would also suggest a spell checker. Additional pair of eyes can’t hurt. To install, use the following command:

```
sudo pacman -S aspell-en libmythes mythes-en languagetool
```

From now on, Manjaro system will warn you of potential spelling errors.

Check out our [article on Language Tool](https://averagelinuxuser.com/languagetool-grammar-checker/) to learn more about this open-source writing assistant.

## 19. Add Keyboard layouts

If you are multi-lingual person, you need to use several keyboard layouts.

Open **Manjaro Settings Manager** → Keyboard → Layout → *+ Add* to install additional keyboard layouts. Configure the shortcut for switching between them with *Change layout option*. (Alt + Shift in my case)

The only missing functionality here would be an easy way of checking the current keyboard layout. Manjaro XFCE has a convenient solution to this.

Right-click on the bottom panel → Panel → Panel Preferences → Items → Select *Notification Area* → *+* → Search for *keyboard* → Select *Keyboard Layouts* → Add

Once you have added it, Select *Keyboard Layouts* → Settings (hamburger menu) → Show layout as *system* & layout name *country*.

![US Keyboard layout in Manjaro XFCE system tray.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/19-keyboard-layout.jpg)

Optionally, you could adjust its position in the system tray by shifting it with up and down arrows.

## 20. Xkill shortcut

`xkill` is a Linux command that allows you to *kill* an app by clicking on it.

I used the term *kill* to indicate that we use xkill to force-quit unresponsive apps. Manjaro has a default CTRL + Alt + X_ shortcut for this command, but I prefer CTRL + Alt + Esc.

Open **Manjaro Settings Manager** → Keyboard → Application Shortcuts → Find xkill → Click on it & type your desired shortcut.

![Configured xkill keyboard shortcut.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/20-xkill-shortcut.jpg)

## 21. Clipboard Manager Settings

Manjaro XFCE’s system tray includes a clipboard manager - **Clipman**. Clipboard manager allows you to retrieve data that you have previously copied. For some users, Clipman’s short history may be a problem.

Right-click on Clipman’s icon in the system tray 🔗 → Clipman Settings → Set *Maximum items* to a number that fits your needs (for me it’s 100).

## 22. Improve menu

Manjaro XFCE’s default menu is not very ergonomic. App categories are on the right-hand side, while the apps are on the left-hand side. I prefer to swap their places. To do this, Right-click on Manjaro menu → Properties → Enable *Position categories next to panel button*.

Another handy feature is *Switch categories by hovering* which you can enable on *Behaviour* tab.

![Manjaro XFCE start menu with categories on the left-hand side and apps on the right-hand side.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/22-improved-menu.jpg)

## 23. Change desktop themes

One of the most popular Linux desktop features is the ability to tweak the look and feel of your desktop. You can [install many additional XFCE themes](https://averagelinuxuser.com/xfce-look-modern-and-beautiful/) in Manjaro and the change them.

Open **Manjaro Settings Manager** → Appearance → Choose your *style/theme* and icons.

To make the window manager match your *style*, go to settings and select *Window Manager.*

You can go even further and [install DockBarX panel](https://averagelinuxuser.com/dockbarx-xfce/).

## 24. User image

The final touch to our desktop appearance is the user’s image.

Open **Manjaro Settings Manager** → User Accounts → Select user account → Select your preferred image.

![User image in Manjaro XFCE start menu.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/24-user-image.jpg)

## 25. Test Webcam and Microphone

If you use Manjaro XFCE on the laptop, it’s good to test whether your webcam and microphone work correctly.

Open **Pulse Audio Volume Control** → Input Devices → Select the microphone to test.

Try speaking to see if the bottom progress bar picks up your voice.

To test the webcam, we need to install an additional app.

Open **Pamac** → Search for *guvc* → Build (Simple UVC Viewer guvcview package) → Apply.

Open the app to see if your webcam is working.

![Testing microphone and webcam with Pulse Audio Volume Control and Guvcview on Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/25-test-webcam-mic.jpg)

## 26. Enable Flatpak/Snap

Having official Arch repository + AUR may seem that Flatpak and Snaps are unnecessary overhead. As with everything, it’s not all black and white. Flatpak/Snaps allow us to encapsulate each application’s running  environment, have different versions of the same app at the same time. If you are  little advanced user and you need this feature, enable Flatpak/Snaps:

Open **Pamac** → ⋮ (three dots menu) → Preferences → Enable *Snap* & *Flatpak* in their corresponding tabs.

![Enabling Flatpak in Pamac Manjaro XFCE.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/26-enabling-flatpak.jpg)

## 27. Turn off startup apps

As ironic as it is, Manjaro XFCE starts many services at system startup. I don’t use all of them. (e.g. Bluetooth and Snap service).

To control startup apps, Open **Session and Startup** → Application Autostart → Turn off services you don’t need.

![Controlling startup apps behaviour.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/27-startup-apps.jpg)

## 28. Remove some apps

Manjaro XFCE comes with a bunch of pre-installed apps. Reason for this is to welcome users coming from Windows/macOS.

To remove apps you don’t use, Open **Pamac** → Installed → Mark apps for removal → Apply.

![Marking apps for removal in Pamac.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/28-remove-apps.jpg)

## 29. Check for errors

From time to time, it is good to check for any errors occurring on your system.

To list any failed services, run:

```
sudo systemctl --failed
```

To check for any process errors, run:

```
sudo journalctl -p 3 -xb
```

## 30. Clean system

If you are coming from Windows, you might be familiar with CCleaner app. CCleaner is used to clean and speed up the system. Manjaro XFCE comes with Bleachbit as an alternative.

Open **Bleachbit** → Select what you would like to clean on the left panel (e.g. browser’s files, system logs) → Clean.

As a word of warning, **be careful** with the stuff you clean. You certainly wouldn’t like to erase your bash/zsh history and stuff from *Deep scan*.

![Marking things to clean in Bleachbit.](https://averagelinuxuser.com/assets/images/posts/2020-09-11-manjaro-xfce-after-install/29-clean-system.jpg)

## Conclusion

Props to you if you have followed me to the very end. I hope you have found these tips useful. Manjaro XFCE comes well configured to make you productive from day one, which makes it one of the best distro options  out there. However, there are no limits to perfection and you can tweak it  even further with these 30 things to do after installing Manjaro.

Let me know which of these things to do after install you love the most. 👇

### Please consider supporting this project: