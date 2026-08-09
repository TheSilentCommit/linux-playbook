## 1. Filesystem and disk usage

Display mounted filesystems with type information and sort the output:

```bash
{ df -Th | head -n 1; df -Th | tail -n +2 | sort; }
```

Display disk usage of directories in the current location, sorted from largest to smallest:

```bash
du -h --max-depth=1 | sort -hr
```

Display the size of files and hidden files in the current directory, sorted from largest to smallest:

```bash
du -sh --apparent-size .[!.]* * 2>/dev/null | sort -hr
```



