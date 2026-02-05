# Day 10 – File Permissions & File Operations Challenge

## Task 1: Create Files (10 minutes)
### 1. Create empty file devops.txt using touch
- Command: `touch devops.txt`
### 2. Create notes.txt with some content using cat or echo
- Command: `echo "Hello dosto" > notes.txt`
### 3. Create script.sh using vim with content: echo "Hello DevOps"
- Command: `vim script.sh`
### Verify: ls -l to see permissions ✅

---

## Task 2: Read Files (10 minutes)
### 1. Read notes.txt using cat
- Command: `cat notes.txt`
### 2. View script.sh in vim read-only mode
- Command: `vim -R script.sh`
### 3. Display first 5 lines of /etc/passwd using head
- Command: `cat /etc/passwd | head -n5`
### 4. Display last 5 lines of /etc/passwd using tail
- Command: `cat /etc/passwd | tail -n5`

---

## Task 3: Understand Permissions (10 minutes)
- Format: rwxrwxrwx (owner-group-others)
- r = read (4), w = write (2), x = execute (1)
- Check your files: ls -l devops.txt notes.txt script.sh
- Answer: What are current permissions? Who can read/write/execute?
  - -rw-rw-r--  owner and group has read/write permission, others has only read permission

---

## Task 4: Modify Permissions (20 minutes)
### 1. Make script.sh executable → run it with ./script.sh
- Command: `chmod 764 script.sh`, `./script.sh`
### 2. Set devops.txt to read-only (remove write for all)
- Command: `chmod 444 devops.txt`
### 3. Set notes.txt to 640 (owner: rw, group: r, others: none)
- Command: `chmod 640 notes.txt`
### 4.Create directory project/ with permissions 755
- Command: `mkdir project && chmod 755 project`
### Verify: ls -l after each change ✅

---

## Task 5: Test Permissions (10 minutes)
### 1. Try writing to a read-only file - what happens?
- Getting error: `Warning: Changing a readonly file `, `-bash: devops.txt: Permission denied`
### 2. Try executing a file without execute permission
- Getting error: `-bash: ./hello.sh: Permission denied`
### 3. Document the error messages
```
Warning: Changing a readonly file
-bash: devops.txt: Permission denied
-bash: ./hello.sh: Permission denied
```
