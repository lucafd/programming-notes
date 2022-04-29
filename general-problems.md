# Common problems and their solutions

Just my experiences in different fields and applications and with different softwares.

[TOC]

## OBS Studio

Ok, the usual problem with microphone and desktop audio track. To separate in two different tracks, hover in "**Edit**" in the context menu above, just under the titlebar.
There, click "**Advanced audio Settings**" or properties or whatever. There, for each audio track, tick only the track in which you want to save the audio. Like, Desktop audio ticked on track 1, microphone ticked on track audio 2.
To listed separately, open in VLC and on "**Audio**"-> "**audio track**" select the track you want to listen.

## Download view-only shared Google Drive video

Last week, I got a Google Drive recording video and it was shared with me with View-Only access. The video was further shared with my team but they are getting access denied on the link. Here are the steps on how to download the video:

1. In Chrome, open developer tools and select the “**Network**” tab.
2. Reload the page that plays the video and filter by type “**videoplayback**”.
3. Right-click on this link and select “**open in new tab**”.
4. Right-click on the video and select “**save video as**”.

That is. No external plugin required. And you can upload your video to the shared drive for your teams, or upload it to youtube depending on your use case.

## Imagemagic error and solution

To install it, `sudo apt install ghostscript imagemagick`.

Today a friend of mine asked to merge a few images into a single PDF document. 
 How hard can it be? **`imagemagick` to a rescue**! 
 Having a clean operating system, I installed it from scratch, via the package manager. 
 However, when I tried to execte `convert` I got a strange and new (to me) error:

```
% convert 'mt 1.jpg'  'mt 2.jpg'  'mt 3.jpg' mt.pdf
convert-im6.q16: attempt to perform an operation not allowed by the security policy `PDF' @ error/constitute.c/IsCoderAuthorized/408.
```

What the hell? 
 It turned out that ImageMagick now has a policy file located at `/etc/imagemagick-6/policy.xml` (or a different path), and that file includes a line for every type of conversion. For example, for PDF there is:

```
  <policy domain="coder" rights="none" pattern="PDF" />
```

that needs to be changed into something that allows the reading and/or writing privileges to the PDF *coder*:

```
  <policy domain="coder" rights="reader | write" pattern="PDF" />
```

## Wacom scripts for linux

```bash
# First, find out the command for your Wacom:
xsetwacom --list devices
```

![img](https://miro.medium.com/max/60/1*Nn4HUxHMdLvgZgHKQrdWDw.png?q=20)

![img](https://miro.medium.com/max/1509/1*Nn4HUxHMdLvgZgHKQrdWDw.png)

In this case, the touch is called ***“Wacom Cintiq 24HD touch Finger touch”\***

```bash
# Then, make Scripts folder to Home:
mkdir -p ~/Scripts/Wacom

# Make the script:
nano ~/Scripts/Wacom/wacom_disable_touch.sh

# Write or copy-paste (Ctrl+C, Ctrl+Shift+V) the following text in there, but replace the "Wacom Cintiq 24HD touch Finger touch" part with what you have:

#!/bin/sh
xsetwacom --set "Wacom Cintiq 24HD touch Finger touch" touch off

# Save and close (Ctrl+X, Y, Enter)# Then, give execute permission for it:
chmod +x ~/Scripts/Wacom/wacom_disable_touch.sh

# You can test the command with:
sh ~/Scripts/Wacom/wacom_disable_touch.sh
```

### Create a ‘W**acom Set Screen’** shell script:

```bash
# Make Scripts folder to Home, if you haven't already:
mkdir -p ~/Scripts/Wacom

# Make the script:
nano ~/Scripts/Wacom/wacom_set_screen1.sh

# Write or copy-paste (Ctrl+C, Ctrl+Shift+V) the following text in there, but replace the "Wacom Intuos4 6x9 Pen stylus" part with what you have:

#!/bin/sh
xsetwacom set "Wacom Intuos4 6x9 Pen stylus" MapToOutput HEAD-0

# Save and close (Ctrl+X, Y, Enter)

# Then, give execute permission for it:
chmod +x ~/Scripts/Wacom/wacom_set_screen1.sh
# HEAD-0 is the monitor 1, HEAD-1 is the monitor 2, and so on. You can make more of these scripts depending on how many monitors you have, if you want to be able to switch between them (to use Wacom on monitor 1 or monitor 2).
```

![img](https://miro.medium.com/max/60/1*waK8WqpanJmiTWdJIT3M0Q.png?q=20)

![img](https://miro.medium.com/max/1664/1*waK8WqpanJmiTWdJIT3M0Q.png)

Using the command line text editor [***Nano\***](https://en.wikipedia.org/wiki/GNU_nano) to make a small Wacom shell script

You can make these scripts to be run automatically when you login to your  distro. For example in Xfce desktop environment (like what Xubuntu uses) search for ‘Startup’ to open the ‘Session and Startup’ application in  order to add your scripts into it:

![img](https://miro.medium.com/max/60/1*wSmT_YPqavgYO3UXpZo1aw.png?q=20)

![img](https://miro.medium.com/max/1467/1*wSmT_YPqavgYO3UXpZo1aw.png)

Adding a Wacom script for autostart in the Session and Startup application

You can also use a shortcut, like **Ctrl+Shift+F1** to run the script to map Wacom to monitor 1 (HEAD-0) and **Ctrl+Shift+F2** for an other script to map it to monitor 2 (HEAD-1):

![img](https://miro.medium.com/max/2184/1*62Tu15vvUA5WuToQqtUwNg.jpeg)

## How to Install the Tor Browser

Note that the Tor Project advises [against installing pre-packaged versions](https://2019.www.torproject.org/docs/debian.html.en) of the Tor browser from the Ubuntu repositories, saying they “have not  reliably been updated” by the Ubuntu community in the past. Only install it from the official Tor Project website. The Tor Project also offers [official repositories](https://2019.www.torproject.org/docs/debian.html.en) for Ubuntu and Debian, but the following manual instructions will work on any Linux distribution.

![Tor browser download page](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_1.png?trim=1,1&bg-color=000&pad=1,1)

If your browser offers to open or save the file, choose the save file option.

Let’s assume the file is saved to the Downloads directory.

When future versions of the Tor browser are released the version  numbers in the filename will change. Also, part of the filename  indicates the language. In this example, “en-US” means English, US.

If you’ve downloaded a different language version, or you’re  following these instructions at a point in the future where the browser  version has changed, substitute the file names and directory names that  you are actually working with for the file names and directory names  used in these instructions.

![Downloaded file in the downloads directory](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_4.png?trim=1,1&bg-color=000&pad=1,1)

The downloaded file is a .tar.xz file. We need to uncompress and untar it so that we can use its contents.

**RELATED:** [***How to Extract Files From a .tar.gz or .tar.bz2 File on Linux\***](https://www.howtogeek.com/409742/how-to-extract-files-from-a-.tar.gz-or-.tar.bz2-file-on-linux/)

There are several ways to do this. If you right-click on the file, a  context menu will appear. Select “Extract Here” from the menu.

![Right click context menu](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_5.png?trim=1,1&bg-color=000&pad=1,1)

Advertisement

If your context menu does not have an “Extract Here” option, close it and double-click the downloaded file. Your file manager might extract  the file contents for you.

If that doesn’t work, open a terminal window in your Downloads directory and use the following command. Note that the “J” in `xvJf` is in uppercase.

```
tar -xvJf tor-browser-linux64-8.5.1_en-US.tar.xz
```

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_20.png?trim=1,1&bg-color=000&pad=1,1)

So, one way or another, the file will be uncompressed and untarred  for you. A new directory will be created in the Downloads folder.

![New folder in the downloads directory](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_6.png?trim=1,1&bg-color=000&pad=1,1)

Double-click the new directory so that the file manager changes into  that directory. Like Russian dolls, there’s another directory inside the first one.

![Inner directory in the Downloads directory](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_7.png?trim=1,1&bg-color=000&pad=1,1)

### Run From the Directory or Do a System Install?

You have a choice here.

Now that you have downloaded and extracted the Tor browser, you can  go ahead and use it, with no further installation steps. Or you can  perform a tighter level of integration with a system level installation.

The operation of the Tor browser is identical in both cases, and  security updates and bug fix patches will find and update the browser  either way.

Advertisement

You may prefer the Tor browser to have as light a touch on your  computer as possible. If you feel happier without embedding the Tor  browser into your system that’s perfectly fine. You will be every bit as anonymous and protected when you use it directly from this directory as you are when you use it after a system level installation. If this is  your preferred approach, follow the instructions in the section titled  Using the Tor Browser From the Tor Directory.

If you’d like the Tor browser to be recognized as an installed  application by your desktop environment and have it appear in the  application menus and application searches, follow the instructions in  the section titled System Level Integration.

### Using the Tor Browser From the Tor Directory

To start the Tor browser directly from the directory, open a terminal window at this location and issue the following command:

```
./tor-browser_en-US/Browser/start-tor-browser &
```

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_x3.png?trim=1,1&bg-color=000&pad=1,1)

You can now skip ahead in this article to the section titled How to Configure the Tor Browser.

### System Level Integration

Open a terminal window at this location. To install the Tor browser into a system folder, you’ll need to move this directory, `tor-browser_en-US`, into the `/opt` directory. This is the usual location for user installed programs in  Linux. We can do this with the following command. Note that you need to  use `sudo` and you’ll be prompted for your password.

```
sudo mv tor-browser_en-US /opt
```

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_8.png?trim=1,1&bg-color=000&pad=1,1)

The folder will move to the new location and will vanish from the  file manager window. In the terminal window change directory so that  you are in the `/opt/tor-browser_en-US` directory.

```
cd /opt/tor-browser_en-US
```

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_26.png?trim=1,1&bg-color=000&pad=1,1)

Using `ls` to list the contents of this directory we see  another directory and a file with a “.desktop” extension. We need to run the “.desktop” file to register the application with your desktop  environment.

```
ls
./start-tor-browser.desktop --register-app
```

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_13.png?trim=1,1&bg-color=000&pad=1,1)

### How to Launch the Tor Browser

The installation sequence described above was tested on the current  Ubuntu, Fedora, and Manjaro Linux distributions. Pressing the Super key  (the one between the left hand Ctrl and Alt keys) and typing “tor”  brought up the Tor Browser icon in all cases.

![img](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_22.png?trim=1,1&bg-color=000&pad=1,1)

Clicking the icon launches the Tor browser.

### How to Configure the Tor Browser

The first time the Tor browser is launched a dialog window appears.

If you access the internet through a proxy, or if you are located in a country that tries to censor the use of tools like Tor, you should  click the “Configure” button.

If neither of those applies to you, click the “Connect” button.

![Configuration dialog window](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_14.png?trim=1,1&bg-color=000&pad=1,1)

Clicking the “Configure” button allows you to set a proxy or to  configure a “bridge” to let you use Tor in countries where its use is  restricted.

![Censorship and proxy check boxes](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_007a-1.png?trim=1,1&bg-color=000&pad=1,1)

We’ll look at the censorship options first.

Advertisement

Select the “Tor is Censored in My Country” checkbox. A set of three options will appear.

These options give you different ways to configure a “bridge.” Bridges are [alternative entry-points](https://2019.www.torproject.org/docs/bridges.html.en) into the Tor network. They are not listed publicly. Using a bridge  makes it much more difficult for your internet service provider to  detect that you are using Tor.

The first option allows you to select a built-in bridge. Click on the “Select a Built-in Bridge” radio button, and choose one of the bridges  from the “Select a Bridge” dropdown menu.

![bridge configuration options](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_003.png?trim=1,1&bg-color=000&pad=1,1)

The second option is to request an alternative bridge.

Click on the “Request a Bridge From Torproject.com” radio button, and click the “Request a New Bridge” button.

![request a new bridge](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_005.png?trim=1,1&bg-color=000&pad=1,1)

When you click the “Request a New Bridge” button, you will be asked to complete a [Captcha](http://www.captcha.net/) to prove you’re a human.

![captcha dialog box](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_004.png?trim=1,1&bg-color=000&pad=1,1)

The third option is for when you already have the details of a bridge that you trust and have used before, and you wish to use that bridge  again.

Advertisement

Click the “Provide a Bridge I Know” radio button and enter the details of the bridge you wish to use.

![provide a bridge I know option](https://www.howtogeek.com/wp-content/uploads/2019/06/new_tor_003.png?trim=1,1&bg-color=000&pad=1,1)

When you have configured your bridge using one of these options, click the “Connect” button to launch the Tor browser.

![connect button to launch Tor browser](https://www.howtogeek.com/wp-content/uploads/2019/06/new_tor_004a-1.png?trim=1,1&bg-color=000&pad=1,1)

### Configuring a Proxy

If you connect to the internet through a proxy, you need to provide the proxy details to the Tor browser.

Click on the “I Use a Proxy to Connect to the Internet” radio button. A new set of options will appear.

![proxy options](https://www.howtogeek.com/wp-content/uploads/2019/06/proxy1.png?trim=1,1&bg-color=000&pad=1,1)

If you have set up your own proxy, you will know the connection  details for it. If you are on a corporate network or someone else set up the proxy, you will need to get the connection details from them.

You will need to provide the IP address or the network name of the  device acting as the proxy, and which port to use. If the proxy requires authentication, you must also provide a username and password.

Advertisement

Click on the “Select a Proxy Type” button to select the proxy type from the dropdown menu, then complete the other fields.

![proxy type dropdown menu](https://www.howtogeek.com/wp-content/uploads/2019/06/proxy2.png?trim=1,1&bg-color=000&pad=1,1)

When you have configured your proxy, click the “Connect” button to launch the Tor browser.

![connect button to launch Tor browser](https://www.howtogeek.com/wp-content/uploads/2019/06/new_tor_004a-1.png?trim=1,1&bg-color=000&pad=1,1)

### How to Use the Tor Browser

You will see a progress bar as the connection to the Tor network is established.

![Tor browser connection progress bar](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_15.png?trim=1,1&bg-color=000&pad=1,1)

Soon you will see the Tor browser main window.

![Tor browser main window](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_16.png?trim=1,1&bg-color=000&pad=1,1)

If it looks a lot like Firefox, that’s because it is Firefox, tweaked and configured to work on the Tor network.

But be careful. Just because you are familiar with Firefox don’t  adjust any of the configuration settings. And don’t install any add-ons. Doing either of these will affect the ability of the Tor browser to  mask your identity. And if you do that there’s hardly any point to using the Tor browser in the first place.

You can put any web site address in the address bar, and the Tor  browser will happily browse to that web site. But using the Tor browser  to do general web browsing will give you an inferior user experience  compared to a standard browser.

Because your connection is bounced around the network of Tor relays  your connection will be slower. And to maintain your anonymity, certain  parts of websites might not work correctly. Flash and other  technologies—even some fonts—will be prevented from operating or  displaying as usual.

The Tor browser is best reserved for those occasions when you value  anonymity above the user experience, and for when you need to visit a  “.onion” web site.

### How to Access an Onion Site on Linux

Some websites have a presence on the clear web and a presence on the  Tor network. The search engine Duck Duck Go does this, for example. The  Tor browser has a quick way for you to connect to the Duck Duck Go  “.onion” site.

Click on the “New to Tor Browser?” link in the top left corner of the browser window.

![New to Tor browser? link](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_16a.png?trim=1,1&bg-color=000&pad=1,1)

Now click on the “Onion Services” link, then click the “Visit an Onion” button.

![visit an onion link](https://www.howtogeek.com/wp-content/uploads/2019/06/visit_onion.png?trim=1,1&bg-color=000&pad=1,1)

You will be taken to the Duck Duck Go “.onion” site.

![Duck duck go .onion site](https://www.howtogeek.com/wp-content/uploads/2019/06/tor_19.png?trim=1,1&bg-color=000&pad=1,1)

Click on the green onion logo in the site information field, and  you’ll see the route your connection has taken to the “.onion” site  you’re currently viewing.

 

![green onion logo in the Tor browser address bar](https://www.howtogeek.com/wp-content/uploads/2019/06/duckduck_onion-1.png?trim=1,1&bg-color=000&pad=1,1)

The route your connection has taken is called its “circuit.” In this  example, the route starts in the UK, and goes via France to the US, and  then through another set of unnamed relays before finally arriving at  the Duck Duck Go “.onion” site.

![relay circuit for .onion routing](https://www.howtogeek.com/wp-content/uploads/2019/06/circuit-1.png?trim=1,1&bg-color=000&pad=1,1)

Click on the shield icon in the top right of the browser toolbar to see your current security level.

![security level for the current connection](https://www.howtogeek.com/wp-content/uploads/2019/06/security_level-1.png?trim=1,1&bg-color=000&pad=1,1)

If you want to change your security level, click on the “Advanced Security Settings” button.

You can set the security level to be Standard, Safer, or Safest. Each increase in security further reduces the number of website features  that will continue to operate correctly.

![Tor browser security settings](https://www.howtogeek.com/wp-content/uploads/2019/06/security.png?trim=1,1&bg-color=000&pad=1,1)

You can browse the internet and find lists of other “.onion” sites,  but this is a dangerous practice. Many of these will host material which is considered illegal, will leave you wanting to bleach your eyes, or  both.

A better approach is to discover whether sites you already use and  trust have a “. onion” presence on the Tor network. You can then use  those sites with anonymity.

Honest and legal sites that value privacy and security and make it a  mainstay of their customer offering are likely to provide a “.onion”  site so that they can be reached using the Tor browser.

ProtonMail, for example, claims to have been built from the ground up with security and privacy in mind. They have [a “.onion” site](https://protonirockerxow.onion/login) to allow their users to connect to them with added privacy. Of course, that link won’t work in a regular browser window.

### And Yet More Anonymity

If even the Tor browser doesn’t provide enough anonymity and privacy  for you, another project that uses Tor at its heart might be what you  need.

Tails is a [live operating system](https://tails.boum.org/) that you can run from a USB flash drive, SD card, or even a DVD. You  can carry it with you, and use it from (almost) any computer. You don’t  need to install anything, and you’ll leave no digital footprints.

### Be Careful Out There

Be cautious, be careful, be wary, and be safe.
When you veer off the clear web and into the shadows, you must always think before you click.
