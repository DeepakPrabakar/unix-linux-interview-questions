# Unix / Linux Interview Questions
> This repo contains random questions that have a possibility of being asked in the Interview.

## Question List

[1. Delete blank lines in file](#1-delete-blank-lines-in-file)<br/>
[2. Print number of times each word appears in a file](#2-print-number-of-times-each-word-appears-in-a-file)<br/>

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
<hr />

### 2. Print number of times each word appears in a file
```bash 
$ cat file | tr '[:space:]' '[\n*]' | grep -v '^\s*$' | sort | uniq -c | sort -bnr
```

`tr` just replaces spaces woth newlines
<br/>`grep -v '^\s*$'` trims out empty lines
<br/>`sort` to prepare as input for uniq
<br/>`uniq -c` to count occurrences
<br/>`sort -bnr` sorts in numeric reverse order while ignoring whitespace

### Print number
### 4. ePrint number
### 5) CCC
### 6. DDD
### 7. Delete blank lines in file
### 8. How to write


- [ ] [Programming Interviews Exposed: Secrets to Landing Your Next Job, 2nd Edition](http://www.wiley.com/WileyCDA/WileyTitle/productCd-047012167X.html)
    - answers in C++ and Java
    - recommended in Google candidate coaching
    - thi
    
    **Create a new branch so you can check items like this, just put an x in the brackets: [x]**


    Fork a branch and follow the commands below

`git checkout -b progress`

`git remote add jwasham https://github.com/jwasham/google-interview-university`

`git fetch --all`

    Mark all boxes with X after you completed your changes
    ## Why use it?

<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

