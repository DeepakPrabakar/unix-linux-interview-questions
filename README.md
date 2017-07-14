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
`$ grep -v '^\s*$' file.txt`

**2. Print number of times each word appears in a file**

`$ cat file | tr '[:space:]' '[\n*]' | grep -v '^\s*$' | sort | uniq -c | sort -bnr`
<br/>`tr` just replaces spaces woth newlines
<br/>`grep -v '^\s*$'` trims out empty lines
<br/>`sort` to prepare as input for uniq
<br/>`uniq -c` to count occurrences
<br/>`sort -bnr` sorts in numeric reverse order while ignoring whitespace

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
