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

**2. Print number of times each word appears in a file**

```bash
$ cat file | tr '[:space:]' '[\n*]' | grep -v '^\s*$' | sort | uniq -c | sort -bnr
```
tr : just replaces spaces woth newlines
grep -v '^\s*$' : trims out empty lines
sort : to prepare as input for uniq
uniq -c : to count occurrences
sort -bnr : sorts in numeric reverse order while ignoring whitespace

