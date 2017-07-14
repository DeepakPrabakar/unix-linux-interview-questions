# unix-linux-interview-questions
My Unix / Linux Interview Questions

### 1. Delete blank lines in file
```bash
$ sed '^\s*$'/d' file.txt
```
To save changes back to file
```bash
$ sed -i '^\s*$'/d' file.txt
```
Also
```bash
$ grep -v '^\s*$' file.txt
```

