# *X basic command set
## A command line cheat sheet
[M.E. Rosner][mrosner], 2021-01-14T16:28:49Z
[mrosner]: https://github.com/exo-mer/2030-research-os-some-basic-commands

#### If you like this document, consider to share it or give star. Thanks for reading!

### session
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

### check, crypt, hash, sign
```
user $ cksum <SOME-FILE>    # print checksum for a give file <SOME-FILE>
```

```
user $ md5 <SOME-FILE>    # print the md5 hash for a given file <SOME-FILE>
```

```
user $ sha256 -c <SOME-FILE-CONTAINING-SHA256SUMS>				# check for a valid signature for a present file in <SOME-FILE-CONTAINING-SHA256SUMS>
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
