# Unix / Linux Interview Questions
> This repo contains questions that have been taken from various sources. Most of these involve the use of two or more commands. 
>
>*All the Best !!!*

## Question List

- [ ] [1. Delete blank lines in file](#1-delete-blank-lines-in-file)<br/>
- [x] [2. Print number of times each word appears in a file](#2-print-number-of-times-each-word-appears-in-a-file)<br/>

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
### 2. Print number of times each word appears in a file
```bash 
$ cat file | tr '[:space:]' '[\n*]' | grep -v '^\s*$' | sort | uniq -c | sort -bnr
```

`tr` just replaces spaces woth newlines
<br/>`grep -v '^\s*$'` trims out empty lines
<br/>`sort` to prepare as input for uniq
<br/>`uniq -c` to count occurrences
<br/>`sort -bnr` sorts in numeric reverse order while ignoring whitespace

<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

