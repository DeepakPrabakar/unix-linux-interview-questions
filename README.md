# Unix / Linux Interview Questions

## Question List

1. [Delete blank lines in file](#delete-blank-lines-in-file)
2. [Print number](#print-number)
[5) CCC](#5-ccc)
[6. DDD](#6-ddd)
[7. Delete blank lines in file](#7-delete-blank-lines-in-file)
[8. How to write](#8-how-to-write)




<a href="#question_2">2. Print number of times each word appears in a file</a>
- [Why use it?](#why-use-it)
- [What is it?](#what-is-it)
[4. AAA](#aaa)
[BAA](#baa)


[3. Print number](#-3-print-number)

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
<br/>
<div align="right">
    <b><a href="#----">↥ back to top</a></b>
    
</div>
<br/>
[Question List](#question-list)

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



- [What is it?](#what-is-it)

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

## What is it?

### 4. AAA
### BAA

### 3. A
### - B
### - C

3. A
- B
- C

3. A
* B
* C

