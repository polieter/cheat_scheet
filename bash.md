# Bash cheat sheet

# Table of content

- [Bash cheat sheet](#bash-cheat-sheet)
- [Table of content](#table-of-content)
- [Man save you!](#man-save-you)
- [Find file](#find-file)
  - [Advance search files](#advance-search-files)
  - [List ten biggest files/folder](#list-ten-biggest-filesfolder)

# Man save you!

```bash
#lets look on manual of man
man man
#look on any command manual
man command
#how to find appropriate command
man -k 'copy file'
#or
apropos 'copy file'
```

# Find file

```bash
#find file using name
find -name file.txt
#find file using name and ignore case
find -iname FilE.txt

find -name passwd
#find passwd file under root and one level down
find -maxdepth 2 -name passwd 
#find passwd file beetwen sub-directory level 2 and 4
find -mindepth 3 -maxdepth 5 -name passwd
```
Every file has an unique inode number, using that we can identify that file.

```bash
#create two files with the same name
ls -i1
find -inum 232321
```

```bash
#find file based on permissions
find . -perm 400 -type f

#find file by size
#find files that matches exacly given size
find . -size 100M
#find files smaller than 100M 
find . -size -100M
#find files bigger than 100M 
find . -size +100M
```

Executing command on files founded by the find command
```bash
find -maxdepth 1 -regex '.*txt' -exec vi {}\;
```

## Advance search files

Find file older than
```bash
#find file older than 10 days
find ./some-path/* -mtime +10
#count files older than 10 days
find ./some-path/* -mtime +10 | wc -l
#delete files older than 10 days
find ./some-path/* -mtime +10 | xargs rm -rf
```

## List ten biggest files/folder
```
du -ah ./some-path/ | sort -rh | head -n 10
```