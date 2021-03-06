# bash-cheat-sheet  
  
# Command Line Shortcuts  
Ctrl-a - go to beginning of line  
Ctrl-e - go to end of line  
  
Ctrl-d - delete one character forward  
Ctrl-h - delete one character backwards  
Ctrl-w - delete the last typed word on cli  
  
Ctrl-k - delete everything after the cursor  
Ctrl-u - delete everything before the cursor  
Ctrl-c - delete currently typed command  
  
Ctrl-l - clear all terminal output while preserving currently typed command  
  
Ctrl-f - go forward one character  
Ctrl-b - go backwards one character  
  
Ctrl-p - same as up arrow. Show last executed command  
  
Ctrl-r - backwards search  

# Useful linux commands  

ls - list files & directories
* -l - long listing. Additional info with permissions, size, etc.  
* -a - include hidden files (dotfiles)  

mkdir - create directory  
* -p - create directory along with path  

cp - copy file/directory
* -r - recursively copy path  
* -i - prompt for overwrite  
* -f - copy force  

mv - move file/directory


file - show file type  

stat - additional info about file
* -f - filesystem information  
* -t - space-delimited list of info  

touch - create empty file OR if it exists, update timestamp  
* -t - specify timestamp explicitly  

grep - search for pattern in file/text stream  
  
find - find something in the system  
* Usage: find \<location\> \<flags\>  
* Flags: -name, -perm, -type  
* -iname - like -name, but case-insensitive  
* -exec - perform a command on a find result    
    * Usage: find <path> <term> -exec <command> {} \;

locate - similar to find, but uses a db. Also, searches in the whole system, not a particular dir.  
* /etc/updatedb.conf - settings about how locate updates its database  

which {cmd} - see the full path to the command you want to execute  

whereis - find all associated files of binary  

type {cmd} - give me info about the type this command is. Alias, binary?
* -a - all info (binaries + aliases)

dd - create iso images  
* Usage: dd if=<dev name> of=<iso name>  
* Works in reverse as well  

whoami - who is logged on system  
  
pwd - current working directory  
  
diff - check difference between two files  
  
ls - list contents of directory  
* Useful Options:  
  * -a - show all files (including hidden)  
  * -l - long listing (show extended info for file)  
  
tee - read from stdin and write to file AND stdout  
* Usage:  
    * \<command\> | tee \<file1\> \<file2\>...  
* Useful options:  
    * -a - append instead of overwriting  

more - text view cli utility  
* -d - show small help line  
* -p - clear screen before opening file  

less - similar to more, but allows moving backwards  

# Globbing

> a set of operators for using wild cards when selecting files/dirs

\* - match 0 or more characters  
? - match exactly 1 character  
[a-z] - specify range of characters  

## Examples

* ls \*.sh - show all `sh` files  
* ls \*.?? - show all 2 symbol file extensions  
* ls [a-c]\*.sh - all `sh` files containing symbols in given range  


# Text utilities

sort - sort a file alphabetically
* -n - sort numerically  
* -k{num} - sort by {num} column  

nl - cat file with line numbers  

wc - word count of file (not only)  
* -l - total lines of file  
* -w - count of words  
* -c - count of characters  

expand - expand the tab width
* -t {num} - set tab width

cat - concat contents of file  
* E.g. cat file1 file2 - concatenates output of both files  
  
tac - show contents of file backwards  

split - split file into files named xaa, xab, xac...
* -a {num} - the count of letters to use for combinations  
* -b {num} - split by {num} bytes  
* -l {num} - split by {num} lines  

od - cli octal viewer
* -d - decimal format  
* -f - floating point format  
* -x - hex format  

pr - format file for printing  
* --columns - format into columns  
* --header - specify header of file  

fmt -{num} - format a file into {num} character columns  

tr - find and replace symbols in files
* Usage: tr 'a' 'A' < file.txt  
* Usage: tr 'a-e' 'A-E' < file.txt  

head - show first lines of file  
* -n {num} - show first {num} lines  

tail - show last lines of file  
* -n {num} - show last {num} lines  
* -f - follow file being updated real time  

cut - cut file into columns  
* Options:  
    * -f {num1},{num2}...{numN} - the columns to display  
    * -d{delim} - the delimiter to use  
    * -c {start}-{finish} - show characters in range  
* e.g. cut -f1 -d: passwd  

paste - concatenate two files side by side  
join - show only duplicate lines of two files (like joining db)  

uniq - show unique lines of file  
* -d - show only duplicate lines of file  
* -D - show only duplicate lines along with redundant ones  

# Grepping  
  
grep - command for filtering lines from stream  
* e.g. grep "hello" hello.txt  
* Can use regular expressions  
    * e.g. grep "^hello$" hello.txt  
  
### Useful options  
  
-i - case-insensitive search  
-n - show line numbers of matched lines  
-f - read expression from file  
-E - extended RegEx  
-F - don't use regex. Treat expression literally  
-e - grep for several expressions.  
* e.g. grep -e "hello" -e "world" hello.txt  
  
egrep == grep -E  
fgrep == grep -F  
  
# Sed stream editor  
sed - command for manipulating streams  
  
## Basic usage:  
sed '\<range\>\<option\>/\<pattern\>/\<flags\>'  
* range - define range for sed to operate on  
    * e.g. % - operate on all lines  
    * e.g. 2, - operate on lines [2, $)  
    * e.g. ,5 - operate on lines (^, 5]  
    * e.g. 2,5 - operate on lines [2, 5]  
* option - can be one of the following  
    * s - substiture matched pattern with something else  
    * d - delete line where pattern is found  
    * i - insert after line where pattern matched  
* pattern - a single regex expression  
    * if s option used - use <pattern>/<replaced> instead of simply <pattern>  
* flags  
    * g - global match. Match more than one pattern on a line if applicable.  
    * c - ask before performing operation  
    * w <file> - write matched patterns operation to file  
  
## Options
* -e - enumerate different patterns to process  
* -f {file} - read patterns to use from {file} (separated in lines)  

# Manipulating streams  
  
\> - redirect stdin to file (overwriting it)  
\>\> - redirect stdin to file (appending)  
2\> - redirect stderr to file (overwriting it)  
2\>&1\> - redirect stderr to stdout to file  
\| - redirect output of left-hand command as input to right-hand command  
\< - redirect contents of file to command  

<command> | tee <file> - redirect stdout to file AND show it on screen  

# Archiving and Compression utilities

tar - archiving (and compression) utility
* flags:
    * -c - create tar archive  
    * -z - gzip compression  
    * -j - bzip2 compression  
    * -t - display contents of archive  
    * -x - extract archive  
    * -v - verbose mode  
    * -f - specify file for given operation  

## Examples

tar -cvfz out.tar.gz in-dir - create gzip archive  
tar -cvfj out.tar.bz2 in-dir - create bzip2 archive  
tar -xvfz out.tar.gz . - extract gzip archive  
tar -xvfj out.tar.gz . - extract bzip2 archive  

# Viewing Hardware Information  
  
lscpu - info about CPU  
lsmod - info about currently loaded kernel modules  
lsblk - info about block devices (e.g. partitions)  
lspci - info about pci devices (peripherals & controllers)  
lsscsi - info about hard disk/ssd devices  
lsusb - info about usb devices  
  
# Managing shared libaries  
  
ldd <executable> - see shared libraries the executable is dependent upon  
ldconfig - updates local system cache with shared libaries on system  
* use when a new shared library is added  
  
## Configuration  
/etc/ld.so.conf.d/\*.conf - include path for all shared libraries on system  
  
# Debian package management  
  
/etc/apt - location for apt configuration files (e.g. list of repositories)  
/etc/apt/sources.list - a repository list that comes with our distro  
/etc/apt/sources.list.d/\*.list - store all third-party repositories here  

## Using apt to manage packages
apt install <package> - install deb package with dependencies  
apt install -d <package> - only download package + dependencies, without installing  
apt install -f - search installed packages and finish installing unconfigured packages  
* Used to fix dependency problems from installing with dpkg  

apt update - refresh the list of packages taken from repos  
apt upgrade - upgrade the packages installed on the system  
apt dist-upgrade - upgrade to latest distro  

apt remove <package> - remove package without conf files  
apt purge <package> - remove app AND related configuration files  

## Using apt-cache to search repo of installed packages
apt-cache search <name> - search repos for given package  
apt-cache show <package-name> -detailed info about package  

## Using dpkg to manually install .deb packages
dpkg vs. apt - dpkg only installs package, apt installs package along with dependencies  

dpkg -i (--install) <package> - install a package  
* dpkg -i --force-reinstreq - force reinstalling a package (overwrite all config files and package related files)  

dpkg -c (--contents) <package> - show files contained in package (and where they will get installed  
dpkg -S (--search) <keyword> - search for keyword in all installed packages  
dpkg -L (--listfiles) <package> - similar to --contents, but for already installed packages  
dpkg -P (--purge) <package> - remove package along with conf files  

dpkg-reconfigure <package> - run external configuration of package if any and overwrite the existing one  
* e.g. postfix package - runs a GUI window after installation for configuring mail server  

# Red Hat Package management
yum - analog to apt-get  
rpm - analog to dpkg  

/etc/yum.conf - main yum configuration file  
/etc/yum.repos.d/ - location of yum repositories  
* gpgcheck - an option of a yum repository. Verifies that a package comes from a given repo with a gpgkey. Security against man in the middle attacks.  

/var/log/yum.log - log file for the yum package manager  

yum update (same as upgrade) == apt-get update && apt-get upgrade  
yum install == apt-get install  
yum install --downloadonly - only download package without installing  
* Downloaded packages are located in /var/cache/yum/(x86\_64/base/packages). (Specified in /etc/yum.conf)  

yumdownloader - yum util tool for downloading packages

yumdownloader --source <package> - download source only  
yumdownloader --urls <package> - urls from where the package will be downloaded  
yumdownloader --resolve <package> - download package and dependencies  
yumdownloader --destdir <dir> <package> - specify destination directory  

## Using rpm to install .rpm packages
/var/lib/rpm - location of rpm database

rpm -i (--install) <package> - install rpm package  
* -v (--verbose) - verbose mode  
* -h (--hash) - see status bar  
* --nodeps - ignore dependencies  

rpm -e <package> - remove rpm package  

rpm -q <package> - query for package. Check if installed  
* -i - detailed info about package  
* -l - info about installed files on system  
* -R - see dependencies  
* -p - provide info about package even if not installed. NOTE: The full path to .rpm file is needed then.  

rpm -V <package> - difference between original package and installed package  

rpm -U <package> - update installed .rpm package to new version (the provided package should be the newer version).
If rpm package does not exists, it acts like an installation.

rpm2cpio - archive .rpm package in a cpio. Used to extract rpm packages on a non-redhat system and later manually install.  
* Use `cpio` command to extract archive in current directory  

# Environment variables

set - show bash settings + environment variables  
env - show environment variables  
shopt - show bash settings  

PATH - env variable with info about directories to look for executables  
HIST\_FILE - location of bash history file  
HISTCONTROL - Bash history options  
HISTFILESIZE - count of commands to record in history  

# Processes management

top - task manager-like cli utility for monitoring processes  
* h - show help while inside program  

ps - monitor processes  
* -a - processes for all users  
* -u - show additional info (like user)  
* -x - show tty-started processes along with all other processes  

ps -ef == ps -aux
* the -ef is the unix way, the other - the FreeBSD/Linux way  

pstree - show processes in tree-mode  
* -a - show additional info (like passed parameters to processes  
* -p - show PIDs  

kill {PID} - kill a program. By default, sends SIGTERM signal.  
* -9 (-SIGKILL) - send a SIGKILL signal  

killall {identifier} - attempt to kill all processes related to {identifier}  

pgrep - grep for PIDs related to a given filter (like a process name)  

## SIG types

* SIGHUP - shut down and restart process  
* SIGINT - interrupt a process from running (can be ignored)  
* SIGKILL - kill process (can't be ignored)  
* SIGTERM - kill process, but allow process to clean up resources (Ctrl-C)  
* SIGSTOP - stop process, not kill (can't ignored).  
* SIGTSTP - Pause a process and allow it to run in the background (Ctrl-Z)  

# Process Execution Priorities

> Every process has a "nice" level. The lower it is, the higher the priority.  
> Minimum nice level is -20 and max is +20  

nice - start a process run by default "nicer" (with lower priority)  
renice [+/-]{modifier} {PID} - change process nice level by [+/-]{modifier}  

# Memory monitoring

free - shows info about RAM memory  
* -m - show in MB (default is KB)  
* -h - human-readable format  

# Jobs management

Ctrl-Z - move current running command to background in Stopped mode  
{command} & - execute command in background  

jobs - show current jobs  
bg {JOB\_ID} - move job to background  
fg {JOB\_ID} - move job to foreground  

nohup {command} - execute command independently of tty  
* (won't stop after you exit terminal)  

# Filesystems and Partitions

/dev - devices directory
* hdN - IDE drives  
* sdN - SATA/SCSI drives  

fdisk - tool for partitioning devices  
* -l - show devices information  
* Usage: fdisk {dev} - start partitioning given device through interactive menu  

gdisk - tool for partitioning devices with GPT partition table  
* Usage: gdisk {dev} - similar to fdisk  

mkfs -t {type} {device} - format {device} with {type} file system type  

/etc/mke2fs.conf - info about possible file system types and what features they provide  

du - see space taken by files and directories
* -h - human readable format
* -a - show all files
* -s - show only root directory

df - show space taken in devices
* -h - human readable format  
* -t - show total line  

fsck - check filesystem for corruption and attempt fix  
* -f - force

# Mounting

mount - shows current mounts on the system
* same info available in /proc/mounts

mount -t {filesystem type} {device} {mount target location}  - mount device  

mount -a - automatically mount default devices from /etc/fstab  

umount {mount point} - unmount device  

/etc/fstab - default mounts when system boots. Modify to have a specific partition mounted by default  
* use uuid when defining mounts
* Template: UUID={uuid} {mount point} {filesystem type} defaults 0 1
* NOTE: Use tabs instead of spaces when pasting the above line

blkid - show uuid, filesystem type and labels of available devices

# Manage disk quotas

> A disk quota is a limitation on usage of system resources enforced by sys admins on users and groups

quotacheck -avugc - create initial quota files

edquota -u {user} - edit quota for user

quotaon -p {mounted filesystem} - check if quotas are on on given filesystem  
quotaon -uagv - turn user and group quotas on  

quota {user} - check quota for user  

# File permissions

chmod {ABCD} {file} - change permissions of file
* A/B/C/D - a digit between 0 and 7. A bitmask representation of rwx permissions.
* A - special bits (suid, sticky bit)
* B - user
* C - group
* D - all

umask - Override default system defined permissions.
* set at bashrc to override umask value
* a set of values subtracted from 666 to get default permissions
* Example: umask = 002; 666 - 002 = 664 --> default permissions: 664

ll - show directory listing + permissions

### Format: 

```
           d rwx rwx rwx 
           - --- --- ---
extra flag-|  |   |   |
              |   |   |
        user--|   |   |
                  |   |
           group--|   |
                      |
                 all--|
                     

extra flag - d for directory. l for symbolic link.
r - read (4)
w - write (2)
x - execute (1)

# Special permissions
user suid (4). Denoted as s on the execute flag of user permissions.
group suid (2). Denoted as s on the execute flag of group permissions.
sticky bit (1). Denoted as s on the execute flag of all permissions.

# set uid - a program with permission to access resources the user can't normally access.
# sticky bit - restricted deletion. Can only append to file

```

# Hard & Symbolic links

symlink - just a pointer to the original file.
hardlink - a pointer to the inode pointing to the original file.

ln -s - create symbolic link
ln - create hard link
