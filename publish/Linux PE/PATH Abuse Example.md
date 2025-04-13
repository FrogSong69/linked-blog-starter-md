Adding `.` (the current directory) to a user's `PATH` lets us run executables in the current directory _just by typing their name_, without needing to specify `./`.

If we can modify the user's `PATH`, we could place a malicious script with the same name as a common command (like `ls`). This way, typing `ls` would run **our script** instead of the real `/bin/ls`.

#### Example

Check the original `PATH`:

```
htb_student@NIX02:~$ echo $PATH 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
```
Add `.` to the beginning of the `PATH`:
```
htb_student@NIX02:~$ PATH=.:$PATH
htb_student@NIX02:~$ export PATH
htb_student@NIX02:~$ echo $PATH
.:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
```
Create a fake `ls` command:
```
htb_student@NIX02:~$ echo 'echo "PATH ABUSE!!"' > ls
htb_student@NIX02:~$ chmod +x ls
```
Now, running `ls` executes your script:
```
htb_student@NIX02:~$ ls
PATH ABUSE!!
```