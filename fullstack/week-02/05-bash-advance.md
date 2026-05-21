# Linux / Bash Advance Commands


## Navigation & Directory Management

these commands help you move around the file system.

```bash
pwd               # shows the full path of where you currently are
cd foldername     # go into a folder
cd ..             # go one level up
cd ../../         # go two levels up
```

eg:
```bash
$ pwd
/home/user/projects

$ cd myapp
$ pwd
/home/user/projects/myapp
```

---

## Listing Files & Directories

`ls` lets you see what's inside a folder. you can add flags to get more details.

```bash
ls                # basic list of files and folders
ls -l             # detailed list — permissions, size, date modified
ls -la            # same but also shows hidden files (files starting with .)
ls -lt            # sorted by time (newest first)
ls -lr            # reverse order
ls -R             # recursive — shows contents of all subfolders too
ls -s             # shows size of each file
ls ..             # list the parent directory
```

eg:
```bash
$ ls -l
drwxr-xr-x  2 user user 4096 Jan 10 10:00 scripts
-rw-r--r--  1 user user  220 Jan 10 09:00 index.js
```

### Pattern matching

you can use `*` as a wildcard to filter what you see.

```bash
ls *.js           # all .js files in current folder
ls Zoo*           # all files whose name starts with "Zoo"
```

eg:
```bash
$ ls *.js
index.js  app.js  utils.js
```

---

## File & Directory Operations

### Creating

```bash
touch filename.js           # creates a new empty file
mkdir foldername            # creates a new folder
mkdir -p frontend/scripts   # creates nested folders (frontend, then scripts inside it)
mkdir test && cd test        # create folder and immediately go into it
```

### Copying & Moving

```bash
cp source.js dest.js        # copy a file
cp -r folder1 folder2       # copy an entire folder

mv old.js new.js            # rename a file
mv file.js folder/          # move a file into a folder
```

eg:
```bash
mv script.js runtime_script.js    # renames script.js to runtime_script.js
```

### Deleting

```bash
rm filename                 # delete a file
rm -r foldername            # delete a folder and everything inside it
```


> Note: `rm -r` is irreversible. There is no trash/recycle bin.

---

## File Permissions

every file in linux has permissions that control who can read, write, or execute it.

permission types:
- `r` → read (4)
- `w` → write (2)
- `x` → execute (1)

user types:
- `u` → user (owner)
- `g` → group
- `o` → others

```bash
chmod u+x filename          # give execute permission to user
chmod g+wx filename         # give write & execute to group
chmod u-x filename          # remove execute from user
chmod ugo-rwx filename      # remove all permissions from everyone
chmod -R ugo-rwx folder     # same but for entire folder (recursive)
```

### Numeric mode

instead of `u+x` you can also use numbers. each permission has a value:

```
r = 4,  w = 2,  x = 1

eg: chmod 664 filename
6 = 4+2+0 → rw-  (user)
6 = 4+2+0 → rw-  (group)
4 = 4+0+0 → r--  (others)
```

```bash
chmod 755 filename     # rwxr-xr-x
chmod 777 filename     # rwxrwxrwx (everyone can do everything)
```

---

## Viewing File Contents

```bash
cat filename      # prints the entire file content to terminal
cat > a.txt       # lets you type and write into a file (Ctrl+D to save)
cat >> a.txt      # appends to an existing file instead of overwriting
```

### Head & Tail

instead of printing the whole file, you can view just the start or end.

```bash
head filename          # first 10 lines
tail filename          # last 10 lines
head -20 filename      # first 20 lines
tail -20 filename      # last 20 lines
```

### Viewing specific rows

```bash
tail -n +25 filename | head -n 5    # view rows 25 to 29
```

eg: view rows 100 to 110
```bash
tail -n +100 filename | head -n 11
```

### Word count

```bash
wc filename      # shows line count, word count, character count
```

eg:
```bash
$ wc data.txt
  150  800  5000 data.txt
#  ↑    ↑    ↑
# lines words chars
```

---

## Text Search — grep

`grep` searches for a pattern inside a file.

```bash
grep "one" filename         # find lines containing "one" (case sensitive)
grep -i "one" filename      # case insensitive
grep -w "one" filename      # match whole word only (won't match "money")
grep -o "one" filename      # show only the matched part, not the whole line
grep -v "INFO" filename     # show lines that do NOT contain "INFO"
```

### With count

```bash
grep -c "one" filename           # how many lines match
grep "one" filename | wc -l      # same thing using pipe
```

### With line numbers

```bash
grep -n "one" filename           # shows which line number the match is on
grep -hin "one" filename         # case insensitive + line numbers
grep -hinw "one" filename        # whole word + case insensitive + line numbers
```

eg:
```bash
$ grep -n "ERROR" log.txt
45:ERROR: File not found
67:ERROR: Connection timeout
```

### In directories

```bash
grep -r "one" foldername         # search through all files in a folder
grep -hir "one" foldername       # same but case insensitive, hides filename
```

### Context lines

sometimes you want to see the lines around the match to understand what happened.

```bash
grep -A 5 ERROR filename         # 5 lines after the match
grep -B 5 ERROR filename         # 5 lines before the match
grep -C 5 ERROR filename         # 5 lines before AND after
```

eg:
```bash
$ grep -A 3 "ERROR" log.txt
ERROR: Connection failed
retrying in 5 seconds...
attempt 2 of 3
still failing...
```

---

## sed — Stream Editor

`sed` is used to find and replace text inside a file.

```bash
sed -n '/ERROR/ p' filename                     # print only lines with ERROR
sed 's/ERROR/CRITICAL/' filename                # replace first match per line
sed 's/ERROR/CRITICAL/g' filename               # replace all matches in file
sed -i.backup 's/ERROR/CRITICAL/' filename      # replace and save backup of original
```

### Line-specific

```bash
sed '3 s/CRITICAL/VERYCRITICAL/' filename       # only replace on line 3
sed '3,5 s/ERROR/CRITICAL/' filename            # replace on lines 3 to 5
sed -n '3,/ERROR/ p' filename                   # print from line 3 until ERROR
```

---

## awk — Pattern Processing

`awk` is used to process and extract data from files, especially column-based data.

```bash
awk '/ERROR/{print $0}' filename               # print lines that contain ERROR
awk '{print $1, $2}' filename                  # print 1st and 2nd column
awk -F "," '{print $1, $2}' filename           # use comma as separator (for csv)
```

eg:
```bash
$ awk '{print $1, $2}' data.txt
John 25
Alice 30
Bob 22
```

### Find & Replace

```bash
awk '{gsub(/ERROR/, "CRITICAL")}{print}' filename
```

### Headers & Footers

```bash
awk 'BEGIN {print "LOG SUMMARY\n--------------"} 
     {print} 
     END {print "--------------\nEND OF LOG SUMMARY"}' filename
```

eg output:
```
LOG SUMMARY
--------------
INFO: server started
ERROR: disk full
--------------
END OF LOG SUMMARY
```

### Counting & conditionals

```bash
awk '{count[$2]++} END {print count["ERROR"]}' filename    # count how many times ERROR appears in column 2

awk '{ if ($1 > 1598863888) {print $0} }' log.txt          # print rows where column 1 is greater than a value
```

---

## System Commands

```bash
echo 'Hello World'     # print something to the terminal
history                # see all commands you've run before
bash filename          # run a bash script file
```

eg:
```bash
$ history
  245  ls -la
  246  cd projects
  247  grep -r "ERROR" logs/
```

---

## Pipes `|`

a pipe takes the output of one command and passes it as input to the next.

```bash
cat file.txt | grep "ERROR" | wc -l     # count how many error lines are in a file
ls -l | grep "\.js$"                    # list only .js files
history | grep "git"                    # find all git commands you've used
```

> Note: you can chain as many pipes as you want

```
command1 | command2 | command3
   ↓           ↓          ↓
output  →  process  →  final result
```
