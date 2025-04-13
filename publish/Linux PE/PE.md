

- `whoami` - what user are we running as
- `id` - what groups does our user belong to?

```shell-session
echo $PATH
```
- `echo`: Displays text or variable values.
- `$PATH`: Refers to the `PATH` variable. The `$` is used to access its value.

```
uname -a
```
- `uname`: Stands for **Unix name**, used to get system info.
- `-a`: Shows **all** details.

List Current Processes
```shell-session
ps aux | grep root
```
- `ps`: Stands for “process status”.
- `a`: Show processes for **all users**.
- `u`: Show the **user**/owner of the process.
- `x`: Include processes **not attached to a terminal** (like background services/daemons).

```shell-session
ls -la 
```
- `ls`: Lists files and directories.
- `-l`: Long listing format — shows detailed info like permissions, owner, size, etc.
- `-a`: Includes **all** files, even hidden ones (those starting with a `.`).
- 
```shell-session
ls -l ~/.ssh
```

Bash history

```shell-session
history
```


```shell-session
sudo -l

sudo su
```

- `sudo`: Stands for “superuser do” — lets you run commands as another user (usually root).
- `-l`: **List** the allowed (or disallowed) commands for your current user.
- `su`: Stands for “substitute user” or “switch user”.
	- Without any options, it switches to the root user.


```
cat /etc/passwd
```
Not sensitive but good to use for password cracking offline
- `cat`: Short for "concatenate" — it reads and prints the content of files.
- `/etc/passwd`: The file that contains **user account information**.

```shell-session
cat /etc/os-release
```

- `cat`: see above
- `/etc/os-release`: A standard file that holds **OS identification data**.

```shell-session
cat /etc/shells
```
- `cat`: Prints the contents of a file.
- `/etc/shells`: A config file that holds the **approved shells** users can use.

```shell-session
cat /etc/group
```
- `cat`: Prints the contents of a file.
- `/etc/group`: The file that holds **group definitions**, including group names, IDs, and member users.
try something like [getent](https://man7.org/linux/man-pages/man1/getent.1.html) group sudo


```shell-session
route
```
Kernel IP routing table 
In a domain environment we'll definitely want to check `/etc/resolv.conf` if the host is configured to use internal DNS

```shell-session
lsblk
```
- `ls`:  list
- `blk`: short for **block devices**
Block devices are hardware (or virtual) devices that read/write data in blocks — examples:
- `/dev/sda` – your main disk
- `/dev/sda1`, `/dev/sda2` – partitions
- `/dev/loop0` – loopback devices (e.g., for mounting `.iso` files)
Common options:
- `lsblk -f`: show **filesystem info** (like `ext4`, `xfs`, `vfat`)
- `lsblk -o +UUID`: add **UUID** info
- `lsblk -p`: show **full paths** (`/dev/sda`, not just `sda`)
```
lscpu
```
- list CPU info

```shell-session
 find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null
```
- `find /`  
    Start searching from the root of the filesystem.
- `-path /proc -prune`  
    If the current path is `/proc`, **skip it** and **don't descend into it**. 
- `-o`  
    **OR** — this is important: it separates the "prune" logic from the actual search logic.
- `-type f`  
    Only look for **regular files** (not directories, devices, etc.).
- `-perm -o+w`  
    Find files with **world-writable** permissions:
    - `-perm`: look at file permissions
    - `-o+w`: the “other” users (not owner or group) have write access
- `2>/dev/null`  
    Redirect **stderr** (error output) to `/dev/null` to **hide permission errors**.

#### Mounted File Systems

```shell-session
df -h
```
- `df`: Stands for **disk free** — shows how much disk space is used and available.
- `-h`: **Human-readable** — displays sizes in KB, MB, GB, etc. instead of raw bytes.

```
echo "$(<flag.txt )"
```
**Used to read from file in rbash**
- `echo`: Prints the text or output passed to it.
- `$()`: **Command substitution** — runs the command inside and replaces it with the output.
- `<flag.txt`: **Input redirection** — reads the contents of `flag.txt` as input.
- `"$(...)"`: **Double quotes** preserve the exact formatting of the file, including spaces and newlines.

```shell-session
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```
- `find /`: Starts searching from the root (`/`) directory.
- `-user root`: Looks for files owned by the **root** user.
- `-perm -4000`: Finds files with the **SUID** bit set (`4000`), which allows users to execute the file with the file owner's (root's) privileges.
- `-exec ls -ldb {} \;`: For each matching file, runs `ls -ldb` to show detailed file info.
    - `-ldb`: Lists the file (not its contents), shows permissions, and does **not follow symlinks**.
    - `{}`: Placeholder for each found file.
    - `\;`: Ends the `-exec` command (escaped to prevent shell interpretation).
- `2>/dev/null`: Suppresses **error messages** (like permission denied) by redirecting `stderr` to `/dev/null`.