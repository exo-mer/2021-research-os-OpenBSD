# *NIX basic command set
----------------------------
# A command line cheat sheet
###### [rosner][exo-mer], 2021-03-06T13:39:18Z

[command line set](https://github.com/exo-mer/2021-research-os-OpenBSD/blob/main/basic-command-line-set.md)

### sessions and first steps
```
user $ login <USER>				                                         # login to the user account <USER>
```

```
user $ which <CMD>                                                 # display full path of a command <CMD> to screen
```

```
user $ whoami                                                      # display the current user
```

```
user $ clear                                                       # clear the screen
```

```
root $ shutdown -h now                                             # shutdown and halt the system
```

```
user $ exit                                                        # leave the current shell (to enter the top one)
```

### reading and navigating
```
user $ man 1 man                                                   # display the manual pages (for the usage of man pages)
```

```
user $ pwd                                                         # print the (current) working directory
```

```
user $ cd /home/$USER                                              # change directory to the home directory of the currently logged in user
```

```
user $ ls -lisa /etc/fstab                                         # long listing for each file current directory (includes displaying hidden files)
```

```
user $ more /usr/share/man/man1/whoami.1                           # to view the first section of the whoami command on screen (use 'q' for quit and cursor for scrolling the document)
```

```
user $ less /usr/share/man/man1/whoami.1                           # to view the first section of the whoami command on screen (use 'q' for quit and cursor for scrolling the document; less is more)
```

### date, time and timestamp
```
user $ touch -d 1968-11-03T18:18:01.032407414Z <FILE>               # creating and/or changing the access time a (new) file <FILE> (open to use [-t [[cc]yy]mmddHHMM[.SS]]).
```

```
user $ date -z UTC +%C%y-%m-%dT%H:%M:%SZ                            # display current universal time code (UTC) of date and time (and use this specific zulu date time format)
```

```
user $ sleep <SECONDS>                                              # suspend for a time frame (i.e. sleep 10 - supspend for 10 seconds)
```

### about the system, users and changing user roles
```
user $ echo 'welcome' $USER'!'                                      # print a welcome message to the current user
```

```
user $ hostname                                               			# print the current fully qualified hostname (i.e. local.home)
```

```
user $ uname -a                                                     # display all specific information on the operating system (architecture, domainname, hostname, os name, os version)
```

```
user $ su					                                                  # switching to super user
```

```
user $ su <USER>				                                            # switching to <USER>
```

```
user $ passwd <USER>				                                        # changing the passphrase of <USER>
```

### users and groups

```
root $ useradd -m <NEWUSER>			                                    # create a home directory and add a <NEWUSER>
```

```
root $ userdel -r <OLDUSER>			                                    # remove account and corresponding home directory for an <OLDUSER>
```

```
root $ usermod -d /home/<NEW-DIR> <USER>	                          # changing the home directory of user <USER> to a new one <NEW-DIR>
```

```
root $ groupadd <NEW-GROUP>			                                    # add the group <NEW-GROUP> to the system
```

```
root $ groupdel <OLD-GROUP>			                                    # remove the group <OLD-GROUP> from the system
```

```
root $ userinfo $USER			                                          # print current user attributes to display (i.e. uid, dir, shell, etc.)
```

### permissions
```
user $ chmod -R 644 ./                                              # recursively changing the permissions of the current folder (to rw- r-- r--).
```

```
root $ chown <USER>:<GROUP> -R ./                                   # recursively changing the ownership of current directory to user and group of choice <USER>:<GROUP>
```

### files and directories
```
user $ cp -R <PATH/TO/SOURCE> <PATH/TO/TARGET>                      # cp files or directories from source <PATH/TO/SOURCE> to target <PATH/TO/TARGET>
```

```
user $ mv <PATH/TO/SOURCE> <PATH/TO/TARGET>                         # move files or directories from source <PATH/TO/SOURCE> to target <PATH/TO/TARGET>
```

```
user $ rm -Rf <PATH/TO/TARGET>                                      # remove files or directories </PATH/TO/TARGET> (use carefully, ones deleted etc.)
```

```
user $ mkdir -p <SUPER-DIR>/<SUP-DIR>                               # (if not present) create parent <SUPER-DIR> and child <SUB-DIR> directory (in one step)
```

```
user $ cat <FILE-A> <FILE-B> > <CONCAT-FILE-C>                      # concatenate the files <FILE-A> and <FILE-B> to a new combinated file <CONCAT-FILE-C>
```

```
user $ cmp <FILE-A> <FILE-B>                                        # compare two files and line by line and output the differences
```

```
user $ diff <FILE-A> <FILE-B>                                       # display differentials of two files <FILE-A> <FILE-B> line by line (used to retrieve a delta, used as patch)
```

### disk space and backups

```
user $ xz -z <FILE>                                                 # compress a given file <FILE> (resulting in <FILE>.xz) 
```

```
user $ xz -d <FILE>.xz                                              # decompress a given xz file <FILE>.xz (resulting in <FILE>)
```

```
user $ tar cvzf <BASE-FILE-NAME>.tar.gz ./*                         # create a gzip'd tar file using all files in current directory in verbose mode
```

```
user $ tar xvzf <BASE-FILE-NAME>.tar.gz                             # gunzip and extract package to current directory in verbose mode
```

```
user $ du -sh ./                                                    # provide disk usage of current directory in a human readable format (using Kilo, Mega, Giga.. byte units)
```

```
user $ df -h                                                        # get an overview of free disk space (human readable)
```

```
root $ dd if=/path/to/<IMAGE> of=/dev/<SDX> bs=1M                   # write image file <IMAGE> to device file <SDX> (i.e. to create a bootable media)
```

### processes

```
user $ pstree                                                       # print tree for all the currently running processes
```

```
user $ ps -p <PID>                                          			  # display all the information that is associated with the specified process id <PID>.
```

```
user $ kill -9 <PID>	                                              # terminates the process with the process id <PID>
```

```
user $ top -U $USER                                                 # print and update all information about CPU processes for the current user
```

### search and filter
```
user $ egrep -re '#include' ./		                                  # list all files from current directory that match the regular expression / string '#include'
```

```
user $ find /home/$USER -name "*.c" -exec grep "include" {} \;      # print all includes for all files with the *.c extension in current user directory
```

### miscellaneous: aliases, replace characters, sort, cut, md5, export
```
user $ alias giga="du -sh * | grep [0-9]'G' | sort"                 # giga as an alias for getting a sorted disk space list disk space on files and directories
```

```
user $ tr '\t' ';' < <INPUT-FILE> > <OUTPUT-FILE>                   # replace all tab '\t' with semicolon ';' and file out to <OUTPUT-FILE>
```

```
user $ export PATH=$PATH:~/.local/bin                               # add ~/.local/bin to PATH variable
```

```
user $ md5 <SOME-FILE> | cut -d' ' -f4                              # print the extracted md5 hash value using cut with space (-d' ') delimiter
```

### git
```
user $ git remote remove origin                                     # solve issues "remote: Invalid username or password. fatal: Authentication failed for 'https://github.com'" remove the origin first

```

```
user $ git remote add origin git@github.com:<USER>/<REPOSITORY>.git     # add a remote origin to push via ssh (works for me)

```


### for loop one-liner
```
user $ for file in *.sh; do cat $file; done                         # for each file having the extension '.sh' print to screen
```

### check, crypt and hashes
```
user $ cksum <SOME-FILE>                                            # print checksum for a give file <SOME-FILE>
```

```
user $ md5 <SOME-FILE>                                              # print the md5 hash for a given file <SOME-FILE>
```

```
user $ sha256 -c <SOME-FILE-CONTAINING-SHA256SUMS>                  # check for a valid signature for a present file in <SOME-FILE-CONTAINING-SHA256SUMS>
```

```
root $ bioctl -c C -l /dev/sd3i softraid0                           # create a file softraid0 for a given crypted container sd3i using bioctl (RAID management interface)
```

```
user $ openssl rand -base64 32                                      # use openssl to generate a random string that is base64-encoded (suitable as base for a passphrase)
```

### network
```
user $ ping 127.0.0.1                                               # ping the ipv4 address 127.0.0.1 (or ping localhost)
```

```
user $ arp -a                                                       # list all arp table records
```

```
user $ ifconfig <INTERFACE>                                         # print the interface configurations and attributes for the interface <INTERFACE> (i.e. use iwn0)
```

```
user $ dhclient <INTERFACE>                                         # get a lease ip address from the dhcp server (for the interface <INTERFACE>; i.e. iwn0)
```

##### If you like this document, consider to share the url above or give it a star. Thanks for reading and enjoy!

##### Sources
+ [OpenBSD manual page server](https://man.openbsd.org/man)
+ [Unix Text Processing Command Reference](https://github.com/nschneid/unix-text-commands)
+ [OpenBSD on wikibooks](https://de.wikibooks.org/wiki/OpenBSD/_Systemprogramme)

##### More sources and additional reading
+ [archlinux man page](https://wiki.archlinux.org/index.php/man_page)
+ [debian manpages](https://manpages.debian.org/)
+ [David R. Mortensen CMU](http://www.cs.cmu.edu/~dmortens/xz.html)
+ [FreeBSD Manual Pages](https://www.freebsd.org/cgi/man.cgi)
+ [funtoo man pages](https://www.funtoo.org/Man_Pages)
+ [gentoo man page](https://wiki.gentoo.org/wiki/Man_page)
+ [Miryung Kim UCLA](http://web.cs.ucla.edu/~miryung/teaching/EE461L-Spring2012/labs/posix.html)
+ [Phil Estes IBM diffs and patches](https://opensource.com/article/18/8/diffs-patches)
+ [readthedocs linuxmint](https://linuxmint-installation-guide.readthedocs.io/de/latest/verify.html)
+ [stackexchange standard commands](https://unix.stackexchange.com/questions/37064/which-are-the-standard-commands-available-in-every-linux-based-distribution)
+ [ssh + github Reconfigure existing repositories to use SSH](https://kamarada.github.io/en/2019/07/14/using-git-with-ssh-keys/#.YBFoCEWYUUE)
+ [stackexchange generate a random string](https://unix.stackexchange.com/questions/230673/how-to-generate-a-random-string)
+ [The Linux man-pages project](https://www.kernel.org/doc/man-pages/)
+ [Ubuntu HowToSHA256SUM](https://help.ubuntu.com/community/HowToSHA256SUM)
+ [ubuntuusers Deutschland e.V.](https://wiki.ubuntuusers.de/man/)
+ [unix for dummies questions and answers](https://www.unix.com/unix-for-dummies-questions-and-answers/42783-replacing-comma-tab.html)
