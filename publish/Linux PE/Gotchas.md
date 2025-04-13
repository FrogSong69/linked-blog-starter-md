
If a script created by the administrator in his path and whose rights have not been restricted, we can run it without going into the `root` directory.

```shell-session
ps aux | grep root
```

If `ALL=(ALL) NOPASSWD: /usr/sbin/tcpdump` is set in the sudoers file, it may be possible to escalate privileges and spawn a root shell by leveraging `tcpdump`'s ability to execute external programs (e.g., using the `-z` flag).