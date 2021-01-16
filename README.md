# *X basic command set
## A command line cheat sheet
[M.E. Rosner][mrosner], 2021-01-14T16:28:49Z
[mrosner]: https://github.com/exo-mer/2030-research-os-some-basic-commands

#### If you like this document, consider to share url above or give it a star. Thanks for reading and enjoy!

### session
```
user $ man man      # display the manual pages (for the usage of man pages)
```

```
user $ echo 'welcome' $USER'!'      # print a welcome message to the current user
```

```
user $ login <USER>				# login to the user account <USER>
```

```
user $ exit					# leave the current shell (to enter the top one)
```

```
user $ hostname				# print the current fully qualified hostname (i.e. local.home)
```

```
user $ su					# switching to super user
```

```
user $ su <USER>				# switching to <USER>
```

```
user $ passwd <USER>				# changing the passphrase of <USER>
```

```
user $ which <CMD>        # display full path of a command <CMD> to screen
```

```
user $ sleep <SECONDS>      # suspend for a time frame (i.e. sleep 10 - supspend for 10 seconds)
```

### user
```
user $ whoami     # display the current user
```

```
root $ useradd -m <NEWUSER>			# create a home directory and add a <NEWUSER>
```

```
root $ userdel -r <OLDUSER>			# remove account and corresponding home directory for an <OLDUSER>
```

```
root $ usermod -d /home/<NEW-DIR> <USER>	# changing the home directory of user <USER> to a new one <NEW-DIR>
```

```
root $ groupadd <NEW-GROUP>			# add the group <NEW-GROUP> to the system
```

```
root $ groupdel <OLD-GROUP>			# remove the group <OLD-GROUP> from the system
```

```
root $ userinfo $USER			# print current user attributes to display (i.e. uid, dir, shell, etc.)
```

### permissions
```
user $ chmod -R 644 ./				# recursively changing the permissions of the current folder (to rw- r-- r--).
```

```
root $ chown <USER>:<GROUP> -R ./		# recursively changing the ownership of current directory to user and group of choice <USER>:<GROUP>
```


### files and directories
```
user $ mv <PATH/TO/SOURCE> <PATH/TO/TARGET>     # move files or directories from source <PATH/TO/SOURCE> to target <PATH/TO/TARGET>
```

```
user $ mkdir -p <SUPER-DIR>/<SUP-DIR>     # (if not present) create parent <SUPER-DIR> and child <SUB-DIR> directory (in one step)
```

```
user $ cat <FILE-A> <FILE-B> > <CONCAT-FILE-C>      # concatenate the files <FILE-A> and <FILE-B> to a new combinated file <CONCAT-FILE-C>
```

```
user $ tar cvzf <BASE-FILE-NAME>.tar.gz ./*     # create a gzip'd tar file using all files in current directory in verbose mode
```

```
user $ tar xvzf <BASE-FILE-NAME>.tar.gz     # gunzip and extract package to current directory in verbose mode
```

```
user $ diff <FILE-A> <FILE-B>
```

```
user $ pwd      # print the (current) working directory
```

```
user $ touch <FILE>				# creating and/or changing the access time a (new) file <FILE> (open to use [-t [[cc]yy]mmddHHMM[.SS]]).
```


```
user $ ls -lisa ./				# long listing for each file current directory (includes displaying hidden files)
```

```
user $ cd /home/$USER			# change directory to the home directory of the currently logged in user
```

```
$ user $ df -h      # get an overview of free disk space (human readable)
```

```
root $ dd if=/path/to/<IMAGE> of=/dev/<SDX> bs=1M     # write image file <IMAGE> to device file <SDX> (i.e. to create a bootable media)
```



### processes

```
user $ pstree				# print tree for all the currently running processes
```

```
user $ ps -p <PID>				# display all the information that is associated with the specified process id <PID>.
```

```
user $ kill -9 <PID>				# terminates the process with the process id <PID>
```

```
user $ top -U $USER     # print and update all information about CPU processes for the current user
```

### search and filter
```
user $ egrep -re '#include' ./		# list all files from current directory that match the regular expression / string '#include'
```

```
user $ find /home/$USER -name "*.c" -exec grep "include" {} \;	# print all includes for all files with the *.c extension in current user directory
```

### for loop one-liner
```
user $ for file in *.sh; do cat $file; done
```

### check, compress, crypt, hash, sign
```
user $ cksum <SOME-FILE>    # print checksum for a give file <SOME-FILE>
```

```
user $ md5 <SOME-FILE>    # print the md5 hash for a given file <SOME-FILE>
```

```
user $ sha256 -c <SOME-FILE-CONTAINING-SHA256SUMS>				# check for a valid signature for a present file in <SOME-FILE-CONTAINING-SHA256SUMS>
```

```
user $ du -sh ./       # provide disk usage of current directory in a human readable format (using Kilo, Mega, Giga.. byte units)
```

```
user $ xz -z <FILE>     # compress a given file <FILE> (resulting in <FILE>.xz) 
```

```
user $ xz -d <FILE>.xz      # decompress a given xz file <FILE>.xz (resulting in <FILE>)
```

### network
```
user $ ping 127.0.0.1    # ping the ipv4 address 127.0.0.1 (or ping localhost)
```

```
user $ arp -a    # list all arp table records
```

```
user $ ifconfig <INTERFACE>     # print the interface configurations and attributes for the interface <INTERFACE> (i.e. use iwn0)
```

```
user $ dhclient <INTERFACE>     # get a lease ip address from the dhcp server (for the interface <INTERFACE>; i.e. iwn0)
```

##### Sources
+ [OpenBSD manual page server](https://man.openbsd.org/man)
+ [Unix Text Processing Command Reference](https://github.com/nschneid/unix-text-commands)
+ [OpenBSD on wikibooks](https://de.wikibooks.org/wiki/OpenBSD/_Systemprogramme)

##### More sources and additional reading
+ [archlinux man page](https://wiki.archlinux.org/index.php/man_page)
+ [David R. Mortensen CMU](http://www.cs.cmu.edu/~dmortens/xz.html)
+ [FreeBSD Manual Pages](https://www.freebsd.org/cgi/man.cgi)
+ [funtoo man pages](https://www.funtoo.org/Man_Pages)
+ [gentoo man page](https://wiki.gentoo.org/wiki/Man_page)
+ [Miryung Kim UCLA](http://web.cs.ucla.edu/~miryung/teaching/EE461L-Spring2012/labs/posix.html)
+ [Phil Estes IBM diffs and patches](https://opensource.com/article/18/8/diffs-patches)
+ [The Linux man-pages project](https://www.kernel.org/doc/man-pages/)
+ [Ubuntu HowToSHA256SUM](https://help.ubuntu.com/community/HowToSHA256SUM)
+ [ubuntuusers Deutschland e.V.](https://wiki.ubuntuusers.de/man/)
+ [stackexchange standard commands](https://unix.stackexchange.com/questions/37064/which-are-the-standard-commands-available-in-every-linux-based-distribution)
+ [readthedocs linuxmint](https://linuxmint-installation-guide.readthedocs.io/de/latest/verify.html)



