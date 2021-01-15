# *X basic command set
## A command line cheat sheet

#### [M.E. Rosner][mrosner], 2021-01-14T16:28:49Z

#### [mrosner]: https://github.com/exo-mer/2030-research-os-some-basic-commands

### session
```
$ login <USER>				# login to the user account <USER>
```

```
$ exit					# leave the current shell (to enter the top one)
```

```
$ hostname				# print the current fully qualified hostname (i.e. local.home)
```

```
$ su					# switching to super user
```

```
$ su <USER>				# switching to <USER>
```

```
$ passwd <USER>				# changing the passphrase of <USER>
```

### user

```
$ useradd -m <NEWUSER>			# create a home directory and add a <NEWUSER>
```

```
$ userdel -r <OLDUSER>			# remove account and corresponding home directory for an <OLDUSER>
```

```
$ usermod -d /home/<NEW-DIR> <USER>	# changing the home directory of user <USER> to a new one <NEW-DIR>
```

```
$ groupadd <NEW-GROUP>			# add the group <NEW-GROUP> to the system
```

```
$ groupdel <OLD-GROUP>			# remove the group <OLD-GROUP> from the system
```


```
$ userinfo $USER			# print current user attributes to display (i.e. uid, dir, shell, etc.)
```

### permissions
```
chmod -R 644 ./				# recursively changing the permissions of the current folder (to rw- r-- r--).
```

```
$ chown <USER>:<GROUP> -R ./		# recursively changing the ownership of current directory to user and group of choice <USER>:<GROUP>
```


### files and directories
```
$ touch <FILE>				# creating and/or changing the access time a (new) file <FILE> (open to use [-t [[cc]yy]mmddHHMM[.SS]]).
```


```
$ ls -lisa ./				# long listing for each file current directory (includes displaying hidden files)
```

```
$ cd /home/$USER			# change directory to the home directory of the currently logged in user
```

### processes

```
$ pstree				# print tree for all the currently running processes
```

```
$ ps -p <PID>				# display all the information that is associated with the specified process id <PID>.
```

```
$ kill -9 <PID>				# terminates the process with the process id <PID>
```

### search and filter
```
$ egrep -re '#include' ./		# list all files from current directory that match the regular expression / string '#include'
```

```
$ find /home/$USER -name "*.c" -exec grep "include" {} \;	# print all includes for all files with the *.c extension in current user directory
```

### for loop one-liner
```
for file in *.sh; do cat $file; done
```

##### Sources
+[OpenBSD manual page server](https://man.openbsd.org/man)
+[Unix Text Processing Command Reference](https://github.com/nschneid/unix-text-commands)
+[OpenBSD on wikibooks](https://de.wikibooks.org/wiki/OpenBSD/_Systemprogramme)

##### More sources and additional reading
+[Miryung Kim UCLA](http://web.cs.ucla.edu/~miryung/teaching/EE461L-Spring2012/labs/posix.html)
+[stackexchange standard commands](https://unix.stackexchange.com/questions/37064/which-are-the-standard-commands-available-in-every-linux-based-distribution)
+[archlinux man page](https://wiki.archlinux.org/index.php/man_page)
+[ubuntuusers Deutschland e.V.](https://wiki.ubuntuusers.de/man/)
+[The Linux man-pages project](https://www.kernel.org/doc/man-pages/)
+[FreeBSD Manual Pages](https://www.freebsd.org/cgi/man.cgi)
