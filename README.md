# Unix / Linux Interview Questions
> This repo contains questions that have been taken from various sources. Most of these involve the use of two or more commands. 
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
$ vi input.txt

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

