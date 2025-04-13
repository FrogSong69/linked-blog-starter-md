
We ssh into the box as htb-student

`find / \( -path /proc -o -path /sys -o -path /dev \) -prune -o -type f -exec grep -E -m 1 "HTB{" {} + 2>/dev/null`

#### `find /`

Start searching from the root of the filesystem.

`\( -path /proc -o -path /sys -o -path /dev \) -prune`
- This **excludes** the directories `/proc`, `/sys`, and `/dev`
- These are virtual or device directories that:
    - Don’t contain flags
    - Often cause permission errors or slowdowns

The `-prune` tells `find` **not to descend into** those paths.
 
 `-o -type f`
This means **OR**: if the path isn't pruned, then match regular files.

`-exec grep -E -m 1 "HTB{" {} +`

For each file found, run:
- `grep -E`: Use **extended regex** (optional here, but good practice)
- `-m 1`: Stop after the **first match** (speeds things up)
- `"HTB{"`: The pattern you’re looking for (start of a flag)
- `{}`: Placeholder for the found file
- `+`: Pass **multiple files at once** to `grep` (more efficient than calling it for each one)

 `2>/dev/null`

Suppresses **error messages**, like permission denied, so the output is clean.



We were able to escalate it to lab_adm bot not to root using

```
sudo -u lab_adm /bin/ncdu
b
```