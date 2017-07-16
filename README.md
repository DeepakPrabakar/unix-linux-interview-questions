# Unix / Linux Interview Questions
> This repo contains questions that have been taken from various sources. Most of these involve the use of two or more commands. 
> I have used **GIT Bash** to execute the below scripts.
>
>*All the Best !!!*

## Question List

- [ ] [1. Delete blank lines in file](#1-delete-blank-lines-in-file)<br/>
- [x] [2. Print number of times each word appears in a file](#2-print-number-of-times-each-word-appears-in-a-file)<br/>
[3. List all the files in directory except .txt and .pdf](#3-list-all-the-files-in-directory-except-txt-and-pdf)<br/>
[4. Rename all .jpg files to .jpeg](#4-rename-all-jpg-files-to-jpeg)<br/>
[5. Delete files of size more than 100mb in a folder which are older than 90 days](#5-delete-files-of-size-more-than-100mb-in-a-folder-which-are-older-than-90-days)<br/>
[6. Reverse the words in a sentence](#6-reverse-the-words-in-a-sentence)<br/>
[7. Given an input file having lines with alphabets and numbers. Print only the distinct alpha-numberic lines.](#7-given-an-input-file-having-lines-with-alphabets-and-numbers-print-only-the-distinct-alpha-numberic-lines)<br/>
[8. Given a comma separated input file with items, category and cost. Display the category and its sum.](#8-given-a-comma-separated-input-file-with-items-category-and-cost-display-the-category-and-its-sum)<br/>
[9. Output of following command `ps -ef | awk '{ print $1}' | sort | uniq | wc -l`](#9-output-of-following-command-ps--ef--awk--print-1--sort--uniq--wc--l)<br/>
[10. Kill process based on user and process.](#10-kill-process-based-on-user-and-process)<br/>
[11. Print contents of a file starting from the nth line.](#11-print-contents-of-a-file-starting-from-the-nth-line)

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
### 3. List all the files in directory except .txt and .pdf
```bash
$ ls -I "*.txt" -I "*.pdf"
```
If you want to iterate across all the subdirectories:
```bash
$ ls -I "*.txt" -I "*.pdf" -R
```
Also
```bash
$ find -not -iname "*.txt"
$ find . ! '(' -name '*.txt' -o -name '*.pdf' ')'
```
Reference: [https://unix.stackexchange.com/questions/47151/how-do-i-list-every-file-in-a-directory-except-those-with-specified-extensions](#https://unix.stackexchange.com/questions/47151/how-do-i-list-every-file-in-a-directory-except-those-with-specified-extensions)
<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

### 4. Rename all .jpg files to .jpeg
```bash
$ vi image.sh

for x in `ls ./images/`;
do
    a=`echo $x | cut -d'.' -f1`
    mv ./images/$x ./images/$a".jpeg";
done

$ ./image.sh
```
### 5. Delete files of size more than 100mb in a folder which are older than 90 days
```bash
$ find /folder -size +204800 -mtime +90 -exec rm {} \;
```
### 6. Reverse the words in a sentence
```bash
$  echo "Have a good day" | awk '{ for(i=0;i<NF;++i){ x=NF-i; printf "%s ",$x;}  }'    
```
**Output:** day good a Have
<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

### 7. Given an input file having lines with alphabets and numbers. Print only the distinct alpha-numberic lines.
**Input**
```
$ cat input.txt

1234567890
0987654321
ABCDEFGH
123456789X
1234567890
123456789X
```
**Output**
```
123456789X
```
```bash
$ vi script.sh

#!/bin/bash
awk '
BEGIN {
i=0; 
}
{ 
    if (($1 ~ /[0-9]/) && ($1 ~ /[A-Z]/)) { 
        flg=0; 
        for (x = 0; $x < $i; x=$x+1) { 
            if($arr[$x] == $1) {
                flg=1;
                break;
            } 
        }
        if(flg==0) {
            arr[$i] = $1; i=$i+1;
        } 
    } 
}
END { 
    for (x = 0; x < $i; x++)
        print $arr[0]
}' input.txt | uniq

$ ./script.sh
```
<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

### 8. Given a comma separated input file with items, category and cost. Display the category and its sum.
**Input**
```
$ cat input.txt

item1,category1,200
item2,category2,100
item3,category3,300
item4,category1,400
item5,category2,500
item6,category1,600
```
**Output**
```
category1 - 1200
category2 - 600
category3 - 300
```
```bash
$ vi script.sh

awk '
BEGIN{
x=0;
flag=0
}
{ 
    split($0,arr,",")           # split - arr[1] has item, arr[2] has category, arr[3] has cost
    flag=0;
    for(i=0;i<=x;i++){
        if(arr[2]==cat_arr[i]){
            flag=1;
            sum_arr[i]=sum_arr[i]+arr[3]
        }
    }
    if(flag==0){
        cat_arr[x]=arr[2]
        sum_arr[x]=arr[3]
        x++;
    }
}
END {
    for(i=0;i<x;i++){
        print(cat_arr[i],"-",sum_arr[i])
    }
}' input.txt

$ ./script.sh
```
<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

### 9. Output of following command `ps -ef | awk '{ print $1}' | sort | uniq | wc -l`
**Answer** 2
```bash
$ ps -ef
     UID     PID    PPID  TTY        STIME COMMAND
prabakad   20464       1 ?          Jul 13 /usr/bin/mintty
prabakad    4940   18944 pty2       Jul 14 /usr/bin/bash
prabakad   18944       1 ?          Jul 14 /usr/bin/mintty
prabakad   19944   20464 pty1       Jul 13 /usr/bin/bash
prabakad   11492    4940 pty2       Jul 14 /usr/bin/winpty
prabakad   20708   16868 pty0     20:38:09 /usr/bin/ps
prabakad   16868   13672 pty0       Jul 12 /usr/bin/bash
prabakad   13672       1 ?          Jul 12 /usr/bin/mintty

$ ps -ef | awk '{ print $1}'
UID
prabakad
prabakad
prabakad
prabakad
prabakad
prabakad
prabakad
prabakad
prabakad

$ ps -ef | awk '{ print $1}' | sort | uniq
prabakad
UID

$ ps -ef | awk '{ print $1}' | sort | uniq | wc -l
2
```
<div align="right">
    <a href="#question-list">Back To Top</a> 
</div>

### 10. Kill process based on user and process.
- Using grep to search
```bash
$ ps -ef | grep "bash" | grep "prabakad"| awk 'BEGIN{print $2}{kill -9 $2}

$ ps -ef | grep "bash" | grep "prabakad"| awk '{print $2}' | xargs kill -9
```
- Using ps command with -u and -p
```bash
$ ps -ef -u prabakad -p 8552 | tail -n +2 | awk '{print $2}' | xargs kill -9
```
Explanation
```bash
$ ps -ef
     UID     PID    PPID  TTY        STIME COMMAND
prabakad   19208   18800 pty0     21:46:39 /usr/bin/bash
prabakad   11440   19208 pty0     21:46:43 /usr/bin/ps
prabakad   18800       1 ?        21:46:38 /usr/bin/mintty

$ ps -ef -u prabakad -p 19208
     UID     PID    PPID  TTY        STIME COMMAND
prabakad   19208   18800 pty0     21:46:39 /usr/bin/bash

$ ps -ef | grep "bash" | grep "prabakad"
prabakad   19208   18800 pty0     21:46:39 /usr/bin/bash
prabakad   19484   19208 pty0     21:47:52 /usr/bin/bash
```
`grep` command does not give header.<br/>
`ps` command gives header, so use `tail` command to remove it.<br/>
The PIDs are sent as arguments using `xargs` and killed using `kill -9`
### 11. Print contents of a file starting from the nth line.
For example, print the give file starting from the 4th line

**Input**
```bash
$ cat lines.txt
line1
line2
line3
line4
line5
line6
line7
line8
line9
line10
line11
```
- Using tail command
```bash
$ cat lines.txt | tail -n +4
line4
line5
line6
line7
line8
line9
line10
line11
```
- Using sed command
```bash
$ sed '1,3d' lines.txt
line4
line5
line6
line7
line8
line9
line10
line11
```
Additional Information

`head` command displays first n lines.<br/>
`tail` command displays last n lines. If `tail` is used with `+`, displays lines starting from nth line as show above.<br/>
The `sed` command above deletes the first 3 lines and prints output starting from 4th line.
