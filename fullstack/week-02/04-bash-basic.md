# Linux / Bash Basic Commands


## Terminal, Shell and Bash

### Terminal

A terminal is a text input and output environment. It is a way to interact with the shell and execute commands.

- Acts as a bridge between the user and the shell
- You type commands and see the output here

### Shell

A shell is a command-line interpreter. It allows users to execute commands, run scripts, and manage system processes.

Common shells:
- Bash (Bourne Again Shell)
- Zsh (Z Shell)
- Fish (Friendly Interactive Shell)

### Bash

Bash is the default shell on most Linux and macOS systems. It supports scripting, command history, job control and a lot more.

### Difference

- Terminal — the window where you type
- Shell — the program that reads and runs your commands
- Bash — a specific type of shell (the most common one)

---

## File and Directory Operations

---

### ls

Lists the contents of a directory.

```bash
ls           # list files in current directory
ls -l        # long format — shows permissions, size, date
ls -a        # show hidden files (starting with .)
ls -lh       # long format with human readable sizes
ls -lah      # all of the above combined
```

```
output (ls -l):
drwxr-xr-x  2 user group 4096 Jan 1 10:00 folder/
-rw-r--r--  1 user group  512 Jan 1 10:00 file.txt
```

---

### cd

Change the current working directory.

```bash
cd folder         # go into folder
cd ..             # go up one level
cd -              # go back to previous directory
cd /path/to/dir   # go to a specific path
```

```
output:
/home/user
/home              ← after cd ..
```

---

### pwd

Prints the current working directory.

```bash
pwd
```

```
output:
/home/user/projects
```

---

### mkdir

Creates a new directory.

```bash
mkdir new-folder               # create a folder
mkdir -p a/b/c                 # create nested folders all at once
```

```
output (mkdir -p):
creates a/ → a/b/ → a/b/c/  all in one go
```

---

### rmdir

Removes an empty directory.

```bash
rmdir empty-folder
rmdir -p a/b/c     # remove nested empty directories
```

---

### cp

Copy files and directories.

```bash
cp file1.txt file2.txt              # copy file
cp -r folder1/ folder2/             # copy entire folder
cp -i file1.txt file2.txt           # ask before overwriting
```

```
output (cp -r):
folder1/ → folder2/  (with all its contents)
```

---

### mv

Move or rename files and directories.

```bash
mv old.txt new.txt                  # rename
mv file.txt /path/to/folder/        # move to another folder
mv -i old.txt new.txt               # ask before overwriting
```

---

### rm

Remove files or directories.

```bash
rm file.txt               # remove a file
rm -r folder/             # remove a folder and everything inside
rm -f file.txt            # force remove, no prompts
rm -rf folder/            # force remove folder — be careful with this
```

> Note: `rm -rf` is irreversible. There is no trash/recycle bin.

---

### touch

Create an empty file or update a file's timestamp.

```bash
touch newfile.txt
```

```
output:
creates newfile.txt  (empty, 0 bytes)
```

---

## File Viewing and Editing

---

### cat

Display the content of a file.

```bash
cat file.txt           # print file content
cat -n file.txt        # print with line numbers
```

```
output (cat -n):
1   Hello
2   World
```

---

### less

View file content one screen at a time. Use arrow keys to scroll, `q` to quit.

```bash
less file.txt
less -N file.txt     # with line numbers
```

---

### head

Show the first part of a file.

```bash
head file.txt          # first 10 lines (default)
head -n 5 file.txt     # first 5 lines
```

---

### tail

Show the last part of a file.

```bash
tail file.txt          # last 10 lines
tail -n 5 file.txt     # last 5 lines
tail -f file.txt       # keep watching file as it grows (useful for logs)
```

---

### grep

Search for a pattern inside a file.

```bash
grep "error" file.txt             # find lines with "error"
grep -i "error" file.txt          # case insensitive
grep -r "error" /path/to/folder   # search inside all files in a folder
grep -v "error" file.txt          # lines that do NOT match
```

```
output:
line 4: error: something went wrong
line 9: error: undefined variable
```

---

### sed

Find and replace text in a file.

```bash
sed 's/old/new/' file.txt          # replace first match per line
sed -i 's/old/new/g' file.txt      # replace all matches, edit file directly
```

---

### awk

Pattern scanning and text processing.

```bash
awk '{print $1}' file.txt          # print first word of each line
awk -F, '{print $1}' data.csv      # first column of a CSV
```

---

## System Information

---

### uname

Print system information.

```bash
uname          # kernel name
uname -a       # all system info
uname -r       # kernel version
```

```
output (uname -a):
Linux hostname 5.15.0 #1 SMP x86_64 GNU/Linux
```

---

### top

Show running processes and system usage live. Press `q` to quit.

```bash
top
top -u username    # show only processes for a specific user
```

---

### ps

Snapshot of current running processes.

```bash
ps             # current shell processes
ps -e          # all processes
ps -ef         # all processes, full detail
```

---

### df

Disk space usage of file systems.

```bash
df             # disk usage
df -h          # human readable (KB, MB, GB)
```

```
output (df -h):
Filesystem  Size  Used  Avail  Use%  Mounted on
/dev/sda1    50G   20G    30G   40%  /
```

---

### du

Estimate space used by files and folders.

```bash
du -h /path/to/folder     # human readable size
du -sh /path/to/folder    # total size only
```

---

### free

Show memory usage.

```bash
free -h     # human readable
free -m     # in megabytes
```

```
output:
              total   used   free
Mem:          7.7G    3.2G   4.5G
Swap:         2.0G    0.0G   2.0G
```

---

## File Permissions

---

### chmod

Change file permissions.

```bash
chmod 755 file.sh              # set permissions
chmod -R 755 folder/           # set permissions for all files inside folder
```

```
755 means:
owner  → read, write, execute
group  → read, execute
others → read, execute
```

---

### chown

Change file owner.

```bash
chown user file.txt                      # change owner
chown user:group file.txt                # change owner and group
chown -R user:group folder/              # recursively change ownership
```

---

## Networking

---

### ping

Check if a host is reachable.

```bash
ping google.com           # keep pinging
ping -c 4 google.com      # send exactly 4 packets
```

```
output:
64 bytes from 142.250.67.46: icmp_seq=1 ttl=118 time=12.3 ms
```

---

### curl

Transfer data from or to a server.

```bash
curl http://example.com                      # fetch a URL
curl -O http://example.com/file.txt          # download a file
curl -L http://example.com                   # follow redirects
curl -I http://example.com                   # fetch headers only
```

---

### wget

Download files from the web.

```bash
wget http://example.com/file.txt              # download file
wget -O output.txt http://example.com/file    # save with different name
wget -r http://example.com                    # download entire site recursively
```

---

## Compression and Archiving

---

### tar

Create or extract archives.

```bash
tar -cvf archive.tar folder/         # create archive
tar -xvf archive.tar                 # extract archive
tar -tvf archive.tar                 # list contents
```

- `-c` create, `-x` extract, `-v` verbose, `-f` file

---

### gzip / gunzip

Compress or decompress `.gz` files.

```bash
gzip file.txt            # compress → file.txt.gz
gzip -d file.txt.gz      # decompress
gzip -k file.txt         # compress and keep original
gunzip file.txt.gz       # same as gzip -d
```

---

### zip / unzip

```bash
zip archive.zip file1 file2          # create zip
zip -r archive.zip folder/           # zip a folder
unzip archive.zip                    # extract
unzip -l archive.zip                 # list contents without extracting
```

---

## Package Management

---

### apt-get (Ubuntu / Debian)

```bash
apt-get update                      # update package list
apt-get upgrade                     # upgrade all packages
apt-get install package-name        # install a package
```

---

### yum (CentOS / RHEL)

```bash
yum install package-name
yum update package-name
yum remove package-name
```

---

## Miscellaneous

---

### echo

Print text to the terminal.

```bash
echo "Hello World"
echo -n "no newline"
echo -e "line1\nline2"     # \n becomes a real newline
```

---

### date

Display current date and time.

```bash
date                        # full date and time
date +%Y-%m-%d              # YYYY-MM-DD format
```

```
output:
2024-01-15
```

---

### whoami

Print current logged-in user.

```bash
whoami
```

```
output:
nishi
```

---

### man

Open the manual/docs for any command.

```bash
man ls         # manual for ls
man grep       # manual for grep
```

> Tip: use `man` whenever you forget flags for any command. Press `q` to quit.

---

### history

Show previously run commands.

```bash
history           # list all past commands
history -c        # clear history
```

---

### alias

Create a shortcut for a long command.

```bash
alias ll='ls -lah'         # now ll runs ls -lah
alias gs='git status'
```

To remove:

```bash
unalias ll        # remove specific alias
unalias -a        # remove all aliases
```
