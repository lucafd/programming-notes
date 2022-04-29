---
title: "LINUX notes and bash"
---

[TOC]

# BASH NOTES

Remember that while you are typing a command or a *path* to a file, you can use `TAB` to have hints on what to write (autocompleting). If there are several options, pressing multiple times `TAB` all the options will be listed. If you don't know how a particular command works, use the manual as pointed out in *Other useful commands*.

## Modify file-path and directory

Commands useful to manage file-paths, files and directories.

Names and short forms for paths:

- `rwx`: permissions (read write execute) are in three groups (others, group, owner);
- `./`: look in the same directory where I am;
- `../`: look in the parent directory;
- `~/`: home directory;
- to list things, *wildcards* are: `ab*f.c` lists every file with any string where there is the star, `ab?f.c` list every file that has any character instead of the quotation mark, `ab[de]f.c` list only those with the letters `d` and `e`

To move directories of the shell and to act on them:

- `cd <dir.path>` change directory that the shell points, specifying the absolute path;
- `pwd` shows the actual absolute path;
- `ls -[alsfr]<dir>` lists all the files inside the directory pointed or by the shell or specified:
  - `-l` lists also the permissions
  - `-a` lists also the hidden files
  - `-d` lists infos only for that directory

Modify files, delete and others:

- `rm [-rif]<file>` removes the file or the directory:
  
  - `rm -r <dir>`: remove the directory in every case;
  - `rmdir`: remove the directory if empty;
  - `rm*`: remove all the file of the directory;
    - `-i` ask confirmation before deleting it;
    - `-f` don't ask for confirmation to delete it;

- `mkdir [-p] <dir>` creates a directory with the specified name, the option create the eventual intermediate directories if absent (AVOID in directory names names with `&`, `/`, `*`, `%` and ` `);

- `cp [-if] <file1> <file2>` copies *file1* in *file2*, if the latter already exists it will be overwritten;

- `cp [-if] <file1> <file2> <dir>` copy the files in the directory specified;

- `mv [-if] <file1> <file2>` moves a file in another one, if already existent it will be overwritten;

- `mv [-if] <file1> <file2> <dir>` moves the files in the directory;

- `cat file` prints in the stdout the content of a textual file;

- `cat file1 file2 > file3` concatenate two textual files in one;

- `cat file1 >> file2` concatenate with append the files specified;

- `diff file1 file2`prints the lines of *file1* that differ from the one in  *file2* and vice versa, doesn't print anything if identical;

- `head file` / `tail file` / `more file` / `less file` to print only part of the lines used, vim-like movement, `q` quit.

Commands to redirect output from _stdin_ or _stdout_  to a _file_:

- `<` input redirecting;
- `>` output redirecting with overwriting;
- `>>` output redirecting (append);
- `&>` redirecting standard error.

## Executable commands and process management

Some commands used to concatenate processes and executing short bash scripts on shell:

- `echo` prints on _stdout_;
- `echo -e` activates the _escapes_, the message should be  put between quotation marks;
- `Ctrl`+`D` it is the EOF character;
- `ps` lists the active processes and their PID of the current shell
  - option `-aux`: lists only those active
  - `-l` lists the active ones with detailed information, the `S` column gives info about the state:
    - `R`: running process or waiting for the processor
    - `S`: sleeping, waiting for an event, like a character from the keyboard
    - `T`: stopped, frozen, waiting to be reactivated
    - `N`: nice, running process with low priority
    - `Z`: zombie, dead process but waiting to communicate its error code to the parent process
- `kill`: forces termination/interruption of the process -- the `PID` is needed, or the process number from the list obtained with `ps -l` with `%N_process`; options indicates the way to kill the program, the most lethal is `-KILL`;
- `top` and `htop`: 
- `grep [arg]` checks and selects the corresponding value for the inserted 
  argument (e.g. process number) from a given _stream_;
- `sleep (num)` waits the number of seconds indicated
- `gnome-screenshot` take a screenshot
- `job` provides list of jobs triggered by the current shell
- `Ctrl`+`C`  kills processes running in the foreground
- `Ctrl`+`Z`  puts in the stopped state (`T`) a process that was running in foreground
- `bg [%N_job]` resumes execution in background
- `fg [%N_job]` resumes execution in foreground

## Consecutive commands

- in order to execute more commands together without warrying of the consequences, it is necessary to use `;` but it executes all without care of the results;
- `|` (pipe) is used to cascade commands so that the output of each is provided as input to the next;
- `||` (logic OR), executes the second command only if the first one fails
- `&&` (logic AND) executes two commands one after the other, and executes the second one only if the first one is successfully completed ;
- `<comand> &` executes the command in the background with the terminal window;

## Packages and file properties

General file management, even compressed:

- `tar xvf <file>` uncompress a tar;
- `touch` creates a text file with the name given;
- `tar cvf` create a tar inside which there is the provided files, `tvf` reads file permissions;
- `file`: reads file permissions and gives information about them;
- `od`: view binary (non-ASCII) files;
- `sort`: sort a text file;
- `gzip`: create a file `gzip`;
- `zip` create a file `zip`;
- `gunzip`, `unzip`: unzip a file;
- `grep [arg] <file>` checks a text file, each line, until it finds similarities, and prints the line where it finds them;
- `wc-l` counts how many elements are that have that name or in the name that part.

## Other useful commands

Other useful or curious commands:

- `du` disk usage, `-h` is human format, `-d number` is the depth to look for;
- `df`;
- `cal [arg][opt]` prints the date calendar format (`-m january` prints the January month of the current year);
- `whoami` tells  who is the user;
- `man <pagina> <comando>` redirects you to the manual of the command you are looking for, on page 1,2,3 which correspond to different languages;
- `history` shows command history, if I write `history 27` it shows the last 27 commands;
- `!27` repeats the commands in the 27th position in the history;
- `!!` repeats the last command, while `!so` recall and execute the command beginning with `so`.
- `cat /dev/null > ~/.bash_history && history -c && exit`: delete completely the command history and exit;
- `pdflatex <nomefile>`: compile latex documents without the need of GUI editor;
- `pandoc [-s] -f [linguaggio1] -t [linguaggio2] -o [nome-output] file_original`is a program that converts files from one language (`-f`) to another (`-t`), the `-s` option indicates whether the output _file_ is to be a _standalone_ or not.
- `which program` points the path of the executable
- `alias` to manage aliases located in `.bach_aliases`:
  - `alias name` shows what that alias does
  - `alias name='definition'` define a new alias
  - `unalias name` remove the alias
- `stty` allow to list all the meta-characters (`--all`) and to change terminal settings

## Utilities for working with files

Listed below are an entirely non-comprehensive list of utilities you  can use to do useful things with files. Many rely on a concept discussed below called a 'regular expression'. If you aren't familiar with these, I have linked some explanations of different regex flavors and  implementations.

Others are just useful for watching processes and files.

### Regexes

Regular expressions are a shorthand way of telling a scripting  language (or really any language) or utility 'look for this match'.

This can be very useful for finding a line that matches and deleting  it, finding and replacing text (your word processor's find and replace  is a much more use friendly but often less powerful version of this),  etc.

Many programming languages have their versions of the regex, all of  which tend to look similar but have different features. If you need  highly complex regexes, you're probably better moving to a scripting  language like Python, PHP, or Javascript--or even a data science tool  like R.

The two BASH tools I'll discuss that use regexes to great benefit are `grep` and `sed`.

The less than newbie friendly guide to regexes for the two programs are linked here: [`sed` regexes](https://www.gnu.org/software/sed/manual/html_node/Regular-Expressions.html) [`grep` regexes](https://www.cyberciti.biz/faq/grep-regular-expressions/) Note: This site also explain the difference in `grep -E` and `grep -F`, which are on old systems sometimes different commands.

[`grep` regex checker](https://www.online-utility.org/text/grep.jsp)

### Checking what you did - `history`

`history` is a highly, highly useful command. It prints the contents of the hidden file `.bash__history` (usually in `~`) to the console along with a list of numbers.

You can shortcut this for the previous command without typing  anything by just pressing the up arrow. Rinse and repeat the command.

But say you wanted to do this for something 50 back? You could hit up 50 times, or you cann call `history` and note the number. Then at a new terminal just type `!number` where number is the number of the command. It will be printed to the command line to be used again!

You can also pipe history output to `grep`, which I go into more detail later, but this is an easy usage:

Say I wanted to know 'When was the last time I ran a script named "manage.py"?'

`history | grep manage.py` would search my user history and return any lines that had "manage.py" in them, matched strictly.

### Looking at text - `less`, `head`, and `tail`

You might find yourself wanting a look at a file, but not wanting to fire up a text editor like `vim` (often aliased to `vi`)  or `nano`. You could `echo` or `cat` the file to the terminal, but you can't scroll or search that, which makes it somewhat worthless.

Here are some options:

### `less` isn't `more`

The history of this commandline utility is somewhre beyond confusing. It postdates `more`, which was a less flexible version of the pgining utility (i.e.  utilities that take text and paginate it for display), but it predates  the less common utility `most`. To quote the [Slackware Linux Essentials Guide](http://www.slackbook.org/html/file-commands-pagers.html): 'If `less` is more than `more`, `most` is more than `less`.

If your platform has `most` installed, it's worth looking through the `man` page and learning about it. It lets you open multiple file buffers at once, among other niceties.

`less` is the goto butter-knife here.

The syntax is simply `less <filename>`, i.e. `less myfile.html`

This will open any file, but of course a binary file (vs. HTML, XML, text documents, etc.) will just be gibberish.

`less` will take over your terminal and let you scroll up and down in the buffer. You can use `q` to quit and `:` to start command sequences. `:/word` will let you search for a word in the file you've opened.

The `man` page goes into much greater detail as to manuevering `less`. It is very handy.

### `head`

`head` show the first few lines of file. Use `man` if you want more.

### `tail`

`tail` shows the last few lines of a file. Look at `man`, but the classic use is with the `-f` flag for a log file you want to monitor. `tail -f filename` displays the file and updates when anything is appended to its end.

If you want to filter the file, you can use `grep` explained below to pipe the output.

`tail -f /var/log/messages | grep 'foo'` would only show appended lines with `foo` in them.

### `grep`

Don't worry [about the name](https://medium.com/@rualthanzauva/grep-was-a-private-command-of-mine-for-quite-a-while-before-i-made-it-public-ken-thompson-a40e24a5ef48#.utcb6warr). `grep` is amazing and it will revolutionize how you look at files.

Its usage is really beyond this basic overview, so I've included a strong tutorial below:

[Using Grep & Regular Expressions - DigitalOceans](https://www.digitalocean.com/community/tutorials/using-grep-regular-expressions-to-search-for-text-patterns-in-linux)

One thing to note is that `grep` typically includes the functionality of some old utilities called `egrep` and `fgrep`, which expand on its capacities. You'll often want to use the `-E` flag (not to be confused with `-e`).

`grep` will take a regular expression and return any line in the file that matches the expression.

A rough rundown on some regular expression tricks for grep without the extended functionality.

`grep "foo" file` would find any line that has 'foo', in it, regardless of position.

Metacharacters that flag positional info or unknown characters can help expand the functionality.

For example, `grep "^FOO" file` would find every line starting with FOO. `grep "FOO$" file` would return every line that ended with FOO.

You can also specify character ranges using `[]`, i.e. `[A-Z]` would match all the upper-case characters.

Metacharacters can also specify how often a pattern can repeat.

`grep "(.*)" file` would mean find any character `.` (`.` is a meta character that means match anything) between `()` and then do so as often as possible `*`. Thus any text between () would create a match.

(N.B. Want to make a literal `.`? `\.` "escapes" the period and treats it as literally a period.)

Grep also respects a huge number of backlash special characters and  expressions. There are sufficiently many of them that I suggest you look [here](https://www.gnu.org/software/grep/manual/grep.html#The-Backslash-Character-and-Special-Expressions). Some require invoking the `-E` flag.

Regular expressions are an art. They also often have the same  problems to solve, so googling for a regex to do a particular thing will find something.

The `-E` flag lets you do even more complex things like grouping regexes, providing alternate matches, etc.

`grep -E "(foo|bar)" file` would match "foo" OR "bar". Note that the parenthesis are special characters when `-E` is invoked.

As noted above, python, perl, PHP, etc. all have versions of the  regex, and they often include much more functionality and more online  support for checkers.

But `grep` is widely available and doesn't require extra framework in the code. MacOS has a different version of `grep` than most Unix/Linux distributions, so online guides may not work. You can use a utility like [Homebrew](https://brew.sh) to install GNU versions of it (and other utilities).

### Editing streams - `sed`

`sed` is a utility called a stream editor. It takes a stream of text, pulled from a file or `stdout` via `|`.

What makes it fantastic is that you can use basic regexes (so no  grouping, none of the special characters, unfortunately) to edit a  stream.

It is also very feature rich, so I commend Bruce Barnett's [introduction](http://www.grymoire.com/Unix/Sed.html) to you.

The basic usage is this `sed <commands and regex> filename`

This will perform the commands you request on the filename and w/o  flags specifying otherwise output the result to the terminal. So you  need to either use flags to make `sed` write the file OR use something like `>` or `|` to send the output to a file or command.

`-e` passes a script with commands to `sed` on the commandline

`sed -e s/foo/bar/g file` would output `file` with all instances of `foo` with `bar`.

`s/` invokes substitution with a regex (here the literal `foo`), and then `g` makes the replacement global throughout the line (otherwise only the first instance is replaced!).

An easier example:

`sed -e "1,11d" file` deletes the first 11 lines of a text.

If you want to edit a file inline: `sed -i.bak -e "s/foo/bar/g" file` actually writes changes to the file and backups up the original to file.bak.

Again, very powerful, not utterly user friendly.

### some remove

`rm -f` (and combinable as `rm -rf`) - These delete a file (or files/directories with `-r`) and also override any prompts for confirmation, which will still be  offered based on the files permissions. This is a bulldozer. Aim  carefully.

`rm -P` - This flag, also combinable, does a  triple-overwrite of a file after deleting it, which can render it  unrecoverable more quickly as a matter of security. You're not going to  need this often and on modern SSD drives, it is even more pointless.

## Install and uninstall with _apt_

Fast commands to install or uninstall a program from _shell_ with the _package manager_ `apt`:

- `sudo apt-get --purge remove <nomeprog>`: uninstall a program;

- `sudo apt autoremove` removes useless files and dependencies;

- `sudo apt-get update` update the repositories from which the *apt* downloads the programs and check if updates are available for installed programs;

- `sudo apt-get upgrade` download and install package updates;

- `apt -s remove package` tells you which dependencies are installed and what problems there are if you remove it;

- here is now an `apt list` command that lists available packages, and the `--installed` command will show only installed packages.  You can also search for a specific package with `apt list <package>` or to see only the matching *installed* packages: `apt list <package> --installed`. There are also the `--upgradeable` and `--all-versions` flags.

## GNOME and troubleshooting

To change from terminal the visualization in `nautilus`:

- `gsettings get org.gnome.nautilus.preferences default-folder-viewer` show the state of the variable called here;
- `gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'` fix the visualization to list, the other value is `'icon-view'`
- press `Ctrl` +`L` when you want to access the text input in nautilus file manager, so you can type it directly
- if software app tells you "failed to update metadata for lvfs: failed checksum expected...", you can solve it by typing in a terminal `fwupdmgr --force refresh`
- this problem is linked to the command `sudo fwupdmgr enable-remote lfvs` but it does not solve the problem, **I still have to understand what it does**.
- there are some packages pre-installed, they are `mlterm`, `mlterm-tiny`, `uim`, `xterm`, but the last I have chosen to keep it because it could turn useful when GNOME Terminal does not work.

## Cool tips

- remove empty directories: `find -type d -empty -exec rm {} \; # remove empty directories `

- `sudo lshw` to show all the informations about your pc. The program can be downloaded through `apt`

- List mp3 files in music directory older than a year and larger than 10MB: `find music -name '*.mp3' -mtime +365 -a -size +10M -ls `

- convert bases to other bases `echo "obase=16;ibase=10;500000" | bc`

- find the years in which 21 November is a Friday `for y in {1970..2010} ; do date -d $y-11-21 +%u-%Y ; done | grep -P "(?<=5-).*"`

- find out how many files sit in a directory `ls -l | wc -l`

- get a list of the ASCII files in the directory `file * | grep ASCII | awk -F: {'print $1'}`

- create a hexdump: `cat file | hexdump -c` 

- interesting alias to use
  
  ```bash
    alias ytmp3='youtube-dl --extract-audio --audio-quality 0 --audio-format mp3 ' # works for playlists too 
    alias update='sudo apt-get update' 
    alias upgrade='sudo apt-get upgrade' 
    alias aptinstall='sudo apt-get install -y' 
    alias ..='cd ..' 
    alias ...='cd ../../../' 
    alias :q='exit' # vim user :) 
    alias duh='du -h -d 1'
  ```

- to download things with wget from file
  
  ```bash
    wget --content-disposition --trust-server-names -i list_of_urls.txt
    cat text_file.txt | parallel --gnu "wget {}"
    wget -i text_file.txt
  ```

- to download with wget but folders, `wget -r -np https://link.com` where `-r` is for recursivity, and `-np` stands for no parent, thus you don't get up on the folder you are.

## FFMPEG

```bash
    ffmpeg -i opening.mkv -i episode.mkv -filter_complex "[0:v] [0:a] [1:v] [1:a] concat=n=2:v=1:a=1 [v] [a]" -map "[v]" -map "[a]" output.mkv
```

## SSH for dummies

In Linux to connect through SSH use the first line, if I want to copy I use line two and three (there is a difference! compare [pragmaticlinux](https://www.pragmaticlinux.com/2020/07/how-to-copy-files-via-ssh/)).
Examples:

```bash
ssh username@sshmachine
scp file-to-copy username@sshmachine:path/to/destination
rsync -e "ssh" -avz file-to-copy username@sshmachine:path/to/destination
scp remoteuser@remoteserver:/remote/folder/remotefile.txt  localfile.txt
```

Thus like from *phoenix* something like `cusu@pheonix:$ scp <file> miopc:<file>` works only if *miopc* has an SSH server turned on (and I imagine you don't have). 
Instead `cusu@miopc:$ scp phoenix:<file> <file>` copies a file from *phoenix* onto *miopc*, while `cusu@miopc:$ scp <file> phoenix:<file>` copies a file from *miopc* to *phoenix*.

## Debian and tricks of the trade

- when just installed, you have to insatll some things, like:
  
  - **git**, fundamental
  - tor browser
  - codium
  - typora
  - teams
  - brave or a cromium based browser
  - spotify 
  - xournalpp
  - flatpak
  - ibus-libpinyin (more of a gnome thing) and uninstall uim and fcitx
  - texstudio
  - nvim

- FONTS! there are plenty of fonts out there, like garamond, ibm plex, open sans and many more. Look for it in synaptic package manager:
  
  - well, I installed fonts-ebgaramond, fonts-ibm-plex, fonts-cmu, noto fonts and open sans were installed in debian already, installed the tex-fonts-extras or similar package, installed fonts-firacode.

- to see the display server in use, `ps -e | grep X`

- `echo $XDG_SESSION_TYPE` to see which display server you are using

- install `intel-microcode` to have processor updates

- to update the bios or others, there is a program, LOOK FOR IT; 

- change the swappiness: to see its value `cat /proc/sys/vm/swappiness/`, then `sudo nvim /etc/sysctl.config` and add at the end of the file `vm.swappiness = 10` or similar; after reboot everything works fine;

- to mod default settings of grub, `sudo nvim /etc/default/grub`, then `sudo update-grub`

- DON'T EVER AND NEVER install python libraries with sudo, do it in local, it doesn't cost you nothing and it doesn't mess with the system.

- to configure the editor `sudo update-alternatives --config editor` and then select what you want

- to support HiDPI screens, xfce4 after 4.14 does that, so if you want to find another solution, look away. In debian bullseye should be ok (version 4.16)

- to run an `appimage` file, you just have to download it, change its executability and run it:
  
  ```bash
  $ chmod a+x appname*.AppImage
  $ ./appname*.AppImage
  ```

- to show emoji use `ctrl-;` in gedit, other locations I don't know, there are inputs like how it works with chinese !TODO write what you did to set up chinese pinyin (install ibus-libpinyin named as intelligent pinyin in ibus center)

- to fix the printers problem in gnome settings add the package
  
  ```bash
  systemctl status cups
  sudo apt install cups
  sudo apt install system-config-printer
  sudo service cups start #or restart, just to activate it before connecting
  ```

- Python, insert the `alias python='python3'` and you have to install pip, thus `sudo apt install python3-pip`. 

- In python, packages should be installed locally per user, without `sudo`, except for `virtualenv`. In order to work, you have to install it globally.

- to install the vpn modules needed in order to use in through `sudo apt install` the modules `openvpn`, `vpnc`, `network-manager-openvpn-gnome`, `network-manager-vpnc-gnome`.

- To install jupyterlab globally, `sudo -H pip install jupyterlab` or `jupyter`.

### Open in terminal Problem in Nautilus

Since version 3.15.4 Nautilus doesn't load the `accel` file anymore [(Source)](https://gitlab.gnome.org/GNOME/nautilus/blob/master/NEWS#L422).

Fortunately there's a better approach in order to get what you want. Long explanation/useful resources can be found [here](https://help.ubuntu.com/community/NautilusScriptsHowto) and also [here](https://askubuntu.com/questions/680016/keyboard-shortcut-for-open-terminal-nautilus-3-16/696901#696901). In short:

1. Create a script called `Terminal` (yes, without a extension) inside the folder `~/.local/share/nautilus/scripts` with the following content:

```bash
 #!/bin/sh
 gnome-terminal
```

2. Make it executable, then close any Nautilus instance:

```bash
 $ chmod +x Terminal
 $ nautilus -q
```

3. Create (or edit) the `~/.config/nautilus/scripts-accels` file adding these lines:

```bash
 F12 Terminal
 ; Commented lines must have a space after the semicolon
 ; Examples of other key combinations:
 ; <Control>F12 Terminal
 ; <Alt>F12 Terminal
 ; <Shift>F12 Terminal
```

4. Test it! Open Nautilus, right click, and choose Scripts >  Terminal. Or, use the keyboard shortcut that you've just configured :)

**Note**: Tested on Ubuntu 18.04.

**Update Ubuntu 20.10**: Unfortunately, this does not anymore work in Nautilus 3.38 (Ubuntu 20.10).

### Spotify scale factor

The issue is only that Spotify doesn't auto-detect the correct scaling factor. If you pass a scaling factor on the command line it will scale just fine:

```bash
spotify --force-device-scale-factor=1.5
```

If you start Spotify using a .desktop file, you can modify it to pass the scaling factor every time like this: modify the file `/usr/share/applications/spotify.desktop`

```bash
[Desktop Entry]
Name=Spotify
GenericName=Music Player
Comment=Spotify streaming music client
Icon=spotify-client
Exec=spotify --force-device-scale-factor=1.5
TryExec=spotify
Terminal=false
Type=Application
Categories=Audio;Music;Player;AudioVideo;
MimeType=x-scheme-handler/spotify;
```

## Syncronize time between Windows and Linux on dual boot

Strangely enough, Windows and Linux use different method for saving on the motherboard the time to display. In particular, Linux saves on motherboard UTC time and then moves from there adding or subtracting the corresponding hours. On the other hand Windows save on the motherboard the local time, that is the time your wristwatch shows, even if on dst. Thus, there is every time this discrepancy between the two. How to solve? You can make linux work with local time or windows with utc.

#### Linux with local time

Simply on a terminal write:

```bash
timedatectl set-local-rtc 1 --adjust-system-clock
```

To verify everything worked properly, `timedatectl`. To reset, write the same command but with `0` instead of `1`. This mode does not support automatic updates, but if you open windows some times it should handle the change on dst without much trouble.

#### Windows with UTC

To change what it does (it works on windows 10 and 11) open `Settings` --> `Time and Language` --> `Date and Time` and there toggle off the "Set time automatically". Press `ok` to save. Then edit the Registry Editor, you can open it just searching it with Cortana or with `Win`+`R` and then `regedit`, run it. Find the following key:

```powershell
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation
```

Right click on it and click on "New" on the contextual menu, select then `DWORD (32-bit) Value`. Name the new key entry `RealTimeIsUniversal`, double click it to modify its value and enter `1` in the data column, click "ok" to save. To undo this process, just delete this new key entry and reset the "Set time automatically"  back to on.

## Manually install

Packages are **manually** installed via the **`dpkg`** command (Debian Package Management System). `dpkg` is the backend to commands like `apt-get` and `aptitude`, which in turn are the backend for GUI install apps like the Software Center and Synaptic.

Something along the lines of:

`dpkg` --> `apt-get`, `aptitude` --> Synaptic, Software Center

But of course the easiest ways to install a package would be, first,  the GUI apps (Synaptic, Software Center, etc..), followed by the  terminal commands `apt-get` and `aptitude` that  add a very nice user friendly approach to the backend dpkg, including  but not limited to packaged dependencies, control over what is  installed, needs update, not installed, broken packages, etc.. Lastly  the `dpkg` command which is the base for all of them.

Since dpkg is the base, you can use it to install packaged directly from the command line.

**To check if a package is installed**. Here `less` is a simple text reader used to scroll through the list of packages in a new buffer that opens in the existing  terminal window. The list will not be mixed with other terminal commands and output. Hit `q` to return to the terminal prompt. See `man less` for more info.

```
dpkg -l | less
```

To check whether a package is installed or not:

```
dpkg -l {package_name}
dpkg -l vlc
```

To check if the package is installed or not (for example, `vlc`). If installed, launch the package:

```
dpkg -l | grep vlc
```

Show the location where the package is installed. The `-S` (capital S) stands for "search"

```
sudo dpkg -S {package_name}
sudo dpkg -S skype
```

To use Grep to search:

```
dpkg -l | grep {keywords}
dpkg -l | grep pdf
```

To **install  a package** just type

```bash
sudo dpkg -i DEB_PACKAGE
```

For example if the package file is called `askubuntu_2.0.deb` then you should do `sudo dpkg -i askubuntu_2.0.deb`. If `dpkg` reports an error due to dependency problems, you can run `sudo apt-get install -f` to download the missing dependencies and configure everything. If that  reports an error, you'll have to sort out the dependencies yourself by  following for example [How do I resolve unmet dependencies after adding a PPA?](https://askubuntu.com/questions/140246/how-do-i-resolve-unmet-dependencies).

If you want to **remove a package**, you can use

```bash
sudo dpkg -r PACKAGE_NAME
```

For example if the package is called `askubuntu` then you should do `sudo dpkg -r askubuntu`.

To **reconfigure an existing package** instead, 

```bash
sudo dpkg-reconfigure PACKAGE_NAME
```

This is useful when you need to reconfigure something related to said package. Some useful examples it the `keyboard-configuration` when you want to enable the Ctrl+Alt+Backspace in order to reset the X server, so you would the following:

```bash
sudo dpkg-reconfigure keyboard-configuration
```

Another great one is when you need to set the Timezone for a server or your local testing computer, so you use use the `tzdata` package:

```bash
sudo dpkg-reconfigure tzdata
```

You can confirm whether a package is already installed by running dpkg command with “-l” option.

```
# sudo dpkg -l {package_name}
# sudo dpkg -l skype
```

Search for a package and do a grep to find the required package.

```
# sudo dpkg -l | grep {keywords}
# sudo dpkg -l | grep ruby
```

Here **-I** stands instead for information, to get information about a specific package.

```
# dpkg -I {package_name}
# dpkg -I skypeforlinux-64.deb
```

This command show the location where the package is installed. The “-S” (capital S) stands for “search”

```
# sudo dpkg -S {package_name}
# sudo dpkg -S ruby
```

Check whether it is installed and get more information about the package. The status “installed” is the package which correctly unpacked and  configured.

```
# sudo dpkg-query -s ruby
```

To install a downloaded `.deb` extension package from a specific location use option `-i`. Or install all packages recursively from a directory.

```
# sudo dpkg -R --install {package_location}
# sudo dpkg -i skypeforlinux-64.deb
# sudo dpkg -i -R /root/dpkg_downloads
```

To dpkg-reconfigure command will reconfigure already installed package in the system

```
# sudo dpkg-reconfigure skypeforlinux-64.deb
# sudo dpkg-reconfigure -R /root/dpkg_downloads
```

To remove any one of installed package use “-r” or we can use the capital “-P” to purge the same.

```
# sudo dpkg -r skypeforlinux-64.deb
# sudo dpkg -P skypeforlinux-64.deb
```

Print the location of installed files of a specific package.

```
# sudo dpkg -L skypeforlinux-64.deb
```

Print all the content of a .deb package using “-c”, Use -c (lowercase c) to show the content.

```
# sudo dpkg -c {package_name}
# sudo dpkg -c skypeforlinux-64.deb
```

To extract the files contained by a .deb package use -x (lowercase x).

```
# dpkg -x {package_name} {location_were_to_extract}
# dpkg -x skypeforlinux-64.deb /home/linuxsysadmins/
```

The .deb package can be extracted and display the filenames contained by a package using a -X (uppercase X).

```
# dpkg -X {package_name} {location_were_to_extract}
# dpkg -X skypeforlinux-64.deb /home/linuxsysadmins/
```

Check for any issue with installed packages by running an audit. Because In  case, if any package has an issue like dependencies or version  compatibility it will report the same.

```
# sudo dpkg --audit
```

Unpacking a package without configuring it. In your requirement to unpack a whole bunch of package under any directory use recursive option `-R`.

```
# sudo dpkg --unpack skypeforlinux-64.deb
# sudo dpkg --unpack -R /root/dpkg_downloads
```

Searches for packages selected for installation but which for some reason not yet got installed. So run the option *–yet-to-unpack* to print those packages.

```
# sudo dpkg --yet-to-unpack
```

Perform installation with `--dry-run` to show what will happen if we use `-i`.  This can be replaced with any command to see the output without making  any changes to the server. Because verifying is a good and best practice before installing with any packages.

```
# sudo dpkg --dry-run -i skypeforlinux-64.deb
```

## Manually install dependencies

**Question:** say, I have `foo-1.2.3.deb` which depends on `perl` and `python`, however, running command:

```bash
dpkg -i ./foo-1.2.3.deb
```

won't install these dependencies. So I must `apt-get install perl python` by hand.

How to make `dpkg -i` install these dependencies for me automatically?

**Answer:** after using `dpkg`, running the following command helped me to install the required dependencies:

```bash
sudo apt-get -f install
```

In all, your terminal should look like this:

```bash
$ sudo dpkg -i package_with_unsatisfied_dependencies.deb
dpkg: dependency problems prevent ... 
[additional messages]

$ sudo apt-get -f install
[apt messages]
Setting up [dependency]...
Setting up package_with_unsatisfied_dependencies...
```

**Notice** the line about `Setting up package_with_unsatisfied_dependencies`. This [fixes](http://manpages.ubuntu.com/apt-get) (and completes) the installation of `package_with_unsatisfied_dependencies.deb`.

**Remarks**: works on Ubuntu 14.04: `sudo dpkg -i package.deb; sudo apt-get -f install; sudo dpkg -i package.deb`. The first `dpkg -i` run marks dependencies, `apt-get -f install` installs required dependencies and the second `dpkg -i`successfully installs the package. Note that `apt-get install -f` is totally different command.

---

Starting with apt 1.1 (available in Xenial (16.04), stretch) `apt install` also allows local files:

```bash
sudo apt install ./foo-1.2.3.deb
```

So much simpler and cleaner.

---

## Root Passwords and similar

### 1. Why you don't have a root password

While you *can* create a password for the superuser account allowing you to log in as root with `su`, it's worth mentioning that this isn't the usual way of doing things  with Ubuntu (or increasingly, other distributions as well).  Ubuntu  chose *not* to give a root login and password by default for a reason.  Instead, a default Ubuntu install will use `sudo` to give superuser privileges.  In a default Ubuntu install the person  who installed the OS is given "sudo" permission by default.

Anybody with full "sudo" permission may perform something "as a superuser" by pre-pending `sudo` to their command.  For instance, to run `apt-get dist-upgrade` as a superuser, you could use:

```bash
sudo apt-get dist-upgrade
```

You will see this usage of sudo pretty much anywhere you read a  tutorial about Ubuntu on the web.  It's an alternative to doing this.

```bash
su
apt-get dist-upgrade
exit
```

With sudo, you choose in advance which users have sudo access. There  is no need for them to remember a root password, as they use their own  password.  If you have multiple users, you can revoke one's superuser  access just by removing their sudo permission, without needing to change the root password and notify everyone of a new password.  You can even  choose which commands a user is allowed to perform using sudo and which  commands are forbidden for that user.  And lastly, if there is a  security breach it can in some cases leave a better audit trail showing  which user account was compromised.

Sudo makes it easier to perform a single command with superuser privileges.  With `su`, you permanently drop to a superuser shell which must be exited using `exit` or `logout`.  This can lead to people staying in the superuser shell for longer than necessary just because it's more convenient than logging out and in  again later.

With sudo, you still have the option of opening a permanent (interactive) superuser shell with the command:

```bash
sudo su
```

... and this can still be done without any root password, because `sudo` gives superuser privileges to the `su` command.

*And similarly, instead of `su -` for a login shell you can use `sudo su -` or its shortcut `sudo -i`.*

However when doing so you just need to be aware that you are acting  as a superuser for every command.  It's a good security principle not to stay as a superuser for longer than necessary, just to lessen the  possibility of accidentally causing some damage to the system (without  it, you can only damage files your user owns).

Just to clarify, you *can*, if you choose, give the root user a password allowing logins as root as described in @Oli's answer, if you  specifically want to do things this way instead.  I just wanted to let  you know about the Ubuntu convention of preferring `sudo` instead and let you know that there is an alternative.

### 2. The problems with your chmod 777 -R command

Your question also has a second part to it: your issues with the command `sudo chmod 777 -R foobs`.

Firstly, the following warning indicates a potentially serious security issue on your machine:

```bash
sudo: /var/lib/sudo writable by non-owner (040777), should be mode 0700
```

This means that at some stage, you've set `/var/lib/sudo` to be world-writable.  I imagine you've done this at some stage using a command like `sudo chmod 777 -R /`.  Unfortunately, by doing this you've probably pretty much broken all  file permissions throughout your system.  It's unlikely that this will  be the only important system file whose permissions have been changed to be world-writable.  Essentially you have an easily hackable system now, and the only easy way to get it back would be to re-install.

Secondly, the command you were using:

```bash
sudo chmod 777 -R foobs
```

When manipulating files within your home directory, in this case in `~/Desktop`, you should not have to use `sudo`.  All the files you create in your home directory should be modifiable by you anyway (and if not, something funny is going on).

Also, you need to be fully aware of the consequences of changing file permissions en masse, such as doing it recursively or on a huge number  of files.  In this case, you're changing carefully set up file  permissions to be world-writable.  Any other user, or any buggy server  software on the machine, may have easy access to overwrite all of these  files and directories.

It's almost certain that `chmod 777 -R [dir]` it is *not* an appropriate solution for whatever problem you were trying to solve  (and as I mentioned above, there is evidence that you have done it to  system files in /var/lib too, and I assume to lots of other places).

A couple of basic rules of thumb:

- If you're just messing with your own files in your home directory, desktop etc, you should never need to use `sudo` or superuser rights.  If you do, it's a warning sign that you're doing something wrong.
- You should never manually modify system files owned by packages.  Exception: unless you're doing it specifically in ways documented by  those packages, such as by modifying their configuration in `/etc`.  This applies also to changing file permissions.  If a tutorial or attempt to fix the problem requires `sudo` or superuser rights, and it's not simply a change to a configuration in /etc/, it's a warning sign that you're doing something wrong.

### 3. Another Solution

By default, the superuser (`root`) account is disabled and doesn't have any password. You can create one by running:

```bash
$ sudo passwd root
```

You will then be able to login as root by running `su` using this password.

As for `chmod`, the correct command would be:

```bash
$ chmod 777 -R foobs
```

You can also use: 

```bash
$ sudo -i
```

to login as root using your password (without creating a root password as described above).

## *Makefile* how it works

The options of `make` are:

- `make -f file` compiles another file different from `makefile`
- `make -n` shows the action without doing it
- `make -i` ignore the errors
- `make -p` shows macros and default rules
- `make -s` do not show the action done

In general you write a file that has inside (other than the file that it has to use):

```bash
targets: dependencies
    actions
```

where `targets` is the list of target files of the rule, `dependencies` is the list of files from which target depends, and  `actions` are the actions to be made, the list of commands to construct the target files. For example this is a *makefile*:

```bash
prova: main.o reverse.o
    cc -o prova main.o reverse.o
main.o: main.c reverse.h
    cc -c main.c
reverse.o: reverse.c reverse.h
    cc -c reverse.c
```

Equivalently, if there are no dependencies you can write (separating with `;<TAB>`) something like `clean: ;    rm *.o core`. Too long lines are interrupted by `\` at the end and  wrap in the following line with the same tabulation.

To put different actions altogether like these

```bash
targ1:
    cc targ1
targ2:
    cc targ2
```

we can write

```bash
targ1 targ2:
    cc $*
```

where `$*` are the name of the current target.

Macro are defined as `MACRONAME=SUBSTITUTION-STRING` and to use it I have to call with  `$(NOMEMACRO)`  that substitute the required string. Some macros have a default value, like `CC=cc` or `CFLAGS= -O`  or `MAKE=make` whilst others are defined given the initial values of the environment variables: `SHELL=/bin/bash/`, `EDITOR=/usr/bin/nvim/`, `HOME=/home/username/`, `LOGNAME=username`, `PATH= current-path` o `TERM=xterm`. To pipe more actions to the same shell in the same row you have to link commands with `;` or similar, if I press `enter` doesn't work! 

There exist some predefined rules in a *makefile*, managed by default. An example is a *suffix rule*:

```bash
.c.o:
    $(CC) $(CFLAGS) -c $<
```

*Suffix rules* are rules that look like this:

```bash
DsTs:
    rule
```

Where `Ts` is the target suffix and `Ds` is the dependency suffix. In a suffix rule the predefined macro `$<` is the name of the dependency.

## Ventoy

First of all you have to download Ventoy, you can do at [the github repository](https://github.com/ventoy/Ventoy/releases) or through the [official site](https://www.ventoy.net/en/download.html). After that, extract the code in a folder, for me was `ventoy`. Now, where to install Ventoy? In an external USB, thus use `sudo fdisk -l` in order to check the name of your device as a disk. Mine was `/dev/sdb/`.  Now move to the Ventoy folder and install on the USB drive giving this command:

```bash
sudo sh Ventoy2Disk.sh -I /dev/sdb/
```

**Attention! the USB will be formatted.** option for install are several, and there is an option also for the *secure boot*:

```
Ventoy2Disk.sh CMD [ OPTION ] /dev/sdX
  CMD:
    -i   install ventoy to sdX (fail if disk already installed with ventoy)
    -I   force install ventoy to sdX (no matter installed or not)
    -u   update ventoy in sdX
    -l   list Ventoy information in sdX

  OPTION: (optional)
   -r SIZE_MB  preserve some space at the bottom of the disk (only for install)
   -s          enable secure boot support (default is disabled)
   -g          use GPT partition style, default is MBR style (only for install)
   -L          Label of the 1st exfat partition (default is ventoy)
```

Now, you can do these things in GUI, and to do so you have to run `sudo sh VentoyWeb.sh` and then open the browser and visit `http://127.0.0.1:24680`. This link is printed in the terminal, you can copy it from there. To close, close the browser and press `^c` to close the process in the terminal. Seems straight forward, you can add options from the top bar `Option`. OK, everything fine, I tried with secure-boot. After reboot I'll write what happened. 

I copied several images, like *kali, debian, manjaro, tails.* Not windows I think... we'll see. Works out of the box, well if secure boot, select `enroll key` and then `vtoyefi` and then the longest name of the file that is `ENROLL_THIS_KEY_IN_MOKMANAGER.cer` and should work without issues.

## Install WinISO on a bootable USB

Almost impossible although there is [this python3 GUI application](https://github.com/WoeUSB/WoeUSB-ng) that works, easy to install. Dependencies to be installed are `sudo apt install git p7zip-full python3-pip python3-wxgtk4.0 ` and nothing more. Then to install it, run `sudo pip3 install WoeUSB-ng`. **IMPORTANT**! you have to do it as a super user, it won't compile otherway. To uninstall it just run

```bash
sudo pip3 uninstall WoeUSB-ng
sudo rm /usr/share/icons/WoeUSB-ng/icon.ico \
    /usr/share/applications/WoeUSB-ng.desktop \
    /usr/local/bin/woeusbgui
sudo rmdir /usr/share/icons/WoeUSB-ng/
```

If you want to install on a virtual environment, read the `README` file in the github repo.

---

## Grub font settings

Solved typing the following command:

```bash
sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 --size=24 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf
```

that put it at a decent resolution, maybe I put 30. OK the font perhaps isn't great but whocares.

Then update the file `/etc/default/grub` inserting the following lines:

```bash
# More readable font on high dpi screen, generated with
# sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 \
#    --size=24 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf
GRUB_FONT=/boot/grub/fonts/DejaVuSansMono24.pf2
```

Eventually update grub with `sudo update-grub`.

## Optimize battery life and consumption

Download and install `sudo apt install tlp`.

### Linux Kernel clean-up

First run `sudo apt update && sudo apt -V upgrade` and then `sudo apt --purge autoremove` to remove automatically old kernels. If not working:

1. this will show all your installed kernels: `dpkg --list |grep linux-image`

2. To remove specifically write `sudo dpkg --purge autoremove linux-image-4.19.0-14-generic`, just change the 4.19.0-14 to the number of the kernel you want to remove - do this for each of the old kernels you want to get rid of -  once you are finished removing all old kernels.

3. this will check for any left over configuration files: `dpkg --list |grep "^rc"`. If it shows any you will need to run the following 2 commands:
   
   1. `dpkg --list |grep "^rc" |cut -d " " -f3`
   2. `dpkg --list |grep "^rc" |cut -d " " -f3 |xargs sudo dpkg --purge`

4. once that is done run ` sudo update-grub` and `sudo update-initramfs -u`

5. reboot and when it boots back up run step 1 again to verify kernels were removed and `uname -r` to see what is currently running. Just do not remove the kernel you are currently using.

# Examples

Program that makes an updated list of files in a directory. It should be called with  `./filename.sh`

```bash
#!/bin/bash

TARGET="Libri comuni"

if [ -e lista.txt ]
then
    rm lista.txt
fi
touch lista.txt

IFS="~"

for link in $( find . -type l -print | tr "\n" "~" ) ; do
    echo -n $link >> lista.txt 
    echo -n "~" >> lista.txt
    echo -n $(find $TARGET -name "$(echo $link | rev | cut -d "/" -f 1 | rev)" -print ) >> lista.txt
    echo -n "#" >> lista.txt
done
```
