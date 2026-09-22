# Pondering Paths

https://pwn.college/linux-luminarium/paths/

This module will teach you the basics of Linux file paths!

---

Here's a small summary of the deck, ready for Notion:

# Linux Luminarium: The File System — Summary

- **Files** — how computers store data (documents, notes, etc.)
- **Directories** — containers that organize files so they're findable, like boxes holding files
- **Nesting** — directories can hold other directories, for deeper organization
- **Root directory (`/`)** — the outermost "box"; every directory in Linux traces back to it
- **Path** — the route through nested directories to reach a specific file or directory (e.g. `/UserData/YansData/Personal/Cooking/PumpkinPieRecipe`)
- **Standard Linux filesystem layout:**

| Path | Purpose |
| --- | --- |
| `/` | Root — anchor of the filesystem |
| `/usr` | System files (Unix System Resource) |
| `/usr/bin` | Executable programs |
| `/usr/lib` | Shared libraries |
| `/usr/share` | Program resources (icons, assets) |
| `/etc` | System configuration |
| `/var` | Logs, caches |
| `/home` | User-owned data |
| `/proc` | Runtime process data |
| `/tmp` | Temporary storage |
- **Navigating:**
    - `pwd` → shows current working directory
    - `cd <dir>` → change directory
    - `ls` → list files in current (or specified) directory
- **Path types:**
    - **Absolute path** — starts with `/` (e.g. `/usr`, `/home/yans/flags/TOPSECRET`)
    - **Relative path** — doesn't start with `/`; relative to current directory
- **Path syntax notes:**
    - `.` = current directory
    - `..` = parent directory
    - Final segment = the file/directory name being referenced

---

## The Root

Alright, so the filesystem starts at `/`. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, *flags*. In this level, we've added a program right in `/`, called `pwn`, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from `/`, so the path would be `/pwn`. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the `pwn` program using its absolute path, and Capture that Flag! Good luck!

#### Challenge

```jsx
hacker@paths~the-root:~$ cd /.
hacker@paths~the-root:/$ ls
bin   challenge  etc   home  lib64  mnt  opt   pwn   run   srv  tmp  var
boot  dev        flag  lib   media  nix  proc  root  sbin  sys  usr
```

- `pwn` program using its absolute path, and Capture that Flag

```jsx
hacker@paths~the-root:/$ cat pwn
#!/bin/bash

/challenge/.pwn
```

- so runining by bash <file> becouse the type of file

```jsx
hacker@paths~the-root:/$ bash pwn
BOOM!!!
Here is your flag:
pwn.college{Yd2Yt_fMmL0byMcQPsx8xAb2dlk.QX4cTO0wiM1YTNwIzW}
```

---

## Program and absolute paths

Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the `challenge` directory and the `challenge` directory is, in turn, right in the root directory (`/`). The path to the challenge directory is, thus, `/challenge`. The name of the challenge program in this level is `run`, and it lives in the `/challenge` directory. Thus, the path to the `run` challenge program is `/challenge/run`.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the `run` file that is in the `challenge` directory that is, in turn, in the `/` directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

**Absolute Path — Simple Summary**

An **absolute path** is the complete location of a file or program starting from `/` (the root directory).

In this challenge:

```jsx
/              → root directory
/challenge     → challenge directory
/challenge/run → challenge program
```

- So, you need to run:

```jsx
/challenge/run
```

**Key idea:** An absolute path always starts with `/` and works no matter which directory you are currently in.

---

#### Challenege

```jsx
hacker@paths~program-and-absolute-paths:/$ ls
bin   challenge  etc   home  lib64  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   media  nix  proc  run   srv   tmp  var
hacker@paths~program-and-absolute-paths:/challenge$ ls
Dockerfile  run
```

if we read the file we going to found out that its bash file 

```jsx
hacker@paths~program-and-absolute-paths:/challenge$ cat run
#!/usr/bin/exec-suid -- /bin/bash -p

if [ "${0:0:1}" != "/" ]
the
        echo -e "${COLOR_RED}Incorrect...${COLORLESS}"
        echo "You did not call this challenge using an absolute path!"
        echo "An absolute path is anchored at the root of the filesystem, so it starts with /"
        exit 1
fi

echo -e "${COLOR_GREEN}Correct!!!${COLORLESS}"
echo "$0 is an absolute path! Here is your flag:"
/bin/cat /flag
hacker@paths~program-and-absolute-paths:/challenge$ bash run
Incorrect...
You did not call this challenge using an absolute path!
An absolute path is anchored at the root of the filesystem, so it starts with /
```

- after runinng the file we found the message (Incorrect... You did not call this challenge using an absolute path! An absolute path is anchored at the root of the filesystem, so it starts with / )
- so the idea of this challenge is the complete location of a file or program starting from `/` (the root directory)
- Run this commend `/challenge/run`

```powershell
hacker@paths~program-and-absolute-paths:/challenge$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{UM95UAILtDlPuZEuZG9jOADxzfU.QX1QTN0wiM1YTNwIzW}
```

---

## Postion thy self

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the `cd` (`c`hange `d`irectory) command and passing a path to it as an argument, as so:

```bash
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the `~` was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the `/challenge/run` program from a specific path (which it will tell you). You'll need to `cd` to that directory before rerunning the challenge program. Good luck!

#### Challange

We tried:

```jsx
hacker@paths~position-thy-self:~$ cd /challenge/run  
bash: cd: /challenge/run: Not a directory   
```

**Finding Our Current Location**

```jsx
hacker@paths~position-thy-self:~$ pwd      
/home/hacker                                                                                                         hacker@paths~position-thy-self:~$                                                                                                                        
```

- `pwd` means **Print Working Directory**.

**Moving to `/home`** 

we can use `cd ..`  , `..` means **the parent directory**.

after moves to  **`/home`  runing** `/challenge/run` 

```jsx
hacker@paths~position-thy-self:~$ cd ..   
hacker@paths~position-thy-self:/home$ pwd               
home     
hacker@paths~position-thy-self:/home$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.                               
```

get a message of direcroty `You are not currently in the **/var** directory`

after moves to  **`/var`  runing** `/challenge/run` 

```jsx
hacker@paths~position-thy-self:/home$ cd /var
hacker@paths~position-thy-self:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{ENbWjIkz_jtDWE51jpfc83JWYhO.QX2QTN0wiM1YTNwIzW}

```

Bravo `pwn.college{ENbWjIkz_jtDWE51jpfc83JWYhO.QX2QTN0wiM1YTNwIzW}`

---

## **Position Elsewhere**

Same thing, but 5 times!

`/challenge/run` 

### Challenge

Level 1 

```jsx
hacker@paths~position-elsewhere:~$ /challenge/run
Starting level 1.
Incorrect...
You are not currently in the /usr/share/doc directory.
Please use the `cd` utility to change directory appropriately.
```

We move to  `/usr/share/doc` 

then run `/challenge/run`

```jsx
hacker@paths~position-elsewhere:~$ cd /usr/share/doc
hacker@paths~position-elsewhere:/usr/share/doc$ /challenge/run
Starting level 1.
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 2
Please use the `cd` utility to change directory to /sys/kernel
```

Level 2

We move on  `/sys/kernel`

then run `/challenge/run`

```jsx
hacker@paths~position-elsewhere:/usr/share/doc$ cd /sys/kernel
hacker@paths~position-elsewhere:/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 3
Please use the `cd` utility to change directory to /etc/apt/sources.list.d
hacker@paths~position-elsewhere:/sys/kernel$
```

Level 3

We move on `/etc/apt/sources.list.d`

then run `/challenge/run`

```jsx
hacker@paths~position-elsewhere:/sys/kernel$ cd /etc/apt/sources.list.d
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 4
Please use the `cd` utility to change directory to /var/lib/apt/lists
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$
```

Level 4

We move on `/var/lib/apt/lists`

then run `/challenge/run`

```jsx
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ cd /var/lib/apt/lists
hacker@paths~position-elsewhere:/var/lib/apt/lists$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 5
Please use the `cd` utility to change directory to /usr/include
hacker@paths~position-elsewhere:/var/lib/apt/lists$
```

Level 5 

We move on `/usr/include`

then run `/challenge/run`

```jsx
hacker@paths~position-elsewhere:/var/lib/apt/lists$ cd /usr/include
hacker@paths~position-elsewhere:/usr/include$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{QgBq0Go3vO4rAEes1NyqfIeQHh0.QX3QTN0wiM1YTNwIzW}
```

Bravo the flag `pwn.college{QgBq0Go3vO4rAEes1NyqfIeQHh0.QX3QTN0wiM1YTNwIzW}`

**Complete Path Sequence**

```jsx
/usr/share/doc
↓
/sys/kernel
↓
/etc/apt/sources.list.d
↓
/var/lib/apt/lists
↓
/usr/include
```

---

## **Implicit Relative Paths, From /**

<aside>
💡

Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for **relative** paths.

- A relative path is any path that does not start at root (i.e., it does not start with `/`).
- A relative path is interpreted **relative** to your **c**urrent **w**orking **d**irectory (`cwd`).
- Your `cwd` is the directory that your prompt is currently located at.

This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at `/tmp/a/b/my_file`.

- If my `cwd` is `/`, then a relative path to the file is `tmp/a/b/my_file`.
- If my `cwd` is `/tmp`, then a relative path to the file is `a/b/my_file`.
- If my `cwd` is `/tmp/a/b/c`, then a relative path to the file is `../my_file`. The `..` refers to the parent directory.

Changing directories and invoking a program are two separate actions. For example:

```bash
hacker@dojo:~$ cd /
hacker@dojo:/$ bin/echo Hello
Hello
```

The first command changes the current working directory to `/`. The second command invokes `/bin/echo` using the relative path `bin/echo`.

</aside>

A relative path does not start with `/`.

For example:

```
absolute: /challenge/run
relative: challenge/run
```

A relative path is interpreted based on our **current working directory**.

### Challenge

Note : Let's try it here! First, change your current working directory to `/`. Then invoke `/challenge/run` using a relative path. For this level, I'll give you a hint. Your relative path starts with the letter `c` 😊

First thing we need to see current path , after that move to `/` directory 

trying the note (`/challenge/run` using a relative path)

and we get 

```jsx
hacker@paths~implicit-relative-paths-from-:/$ /challenge/run
Incorrect...
You invoked this challenge with an absolute path. This challenge needs a relative path!
```

try without `/` at the first 

```jsx
hacker@paths~implicit-relative-paths-from-:/$ **challenge/run**
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{Ihsbl8iDXRiVAsstOcUfh1vKuE1.QX5QTN0wiM1YTNwIzW}
```

---

## Explicit Relative Paths, From /

**Quick note: Relative path using `.`**

- `.` refers to the current directory itself.
- So these absolute paths are all identical: `/challenge` = `/challenge/.` = `/./challenge/.`
- And these relative paths are all identical too: `challenge` = `./challenge` = `challenge/.`

**Task requirements:**

1. Your current working directory must be `/`
2. You must invoke the challenge using a relative path that begins with `.` (e.g. `./challenge`)

### Challenege

**Execution:**

```jsx
hacker@paths~implicit-relative-paths-from-:~$ pwd
/home/hacker
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ pwd
/
```

**Failed attempts first:**

```jsx
hacker@paths~explicit-relative-paths-from-:/$ ./challenge
bash: ./challenge: Is a directory
hacker@paths~explicit-relative-paths-from-:/$ challenge/.
bash: challenge/.: Is a directory
hacker@paths~explicit-relative-paths-from-:/$ ./././challenge
bash: ./././challenge: Is a directory
hacker@paths~explicit-relative-paths-from-:/$ challenge
bash: challenge: command not found
```

```
./challenge          → bash: ./challenge: Is a directory
challenge/.          → bash: challenge/.: Is a directory
./././challenge      → bash: ./././challenge: Is a directory
challenge            → bash: challenge: command not found
```

Reason: `challenge` is a directory, not an executable. Even though it contains a file called `run`, Linux doesn't execute it automatically just by referencing the directory.

**Correct solution:**

```jsx
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/./run
Correct!!!
./challenge/./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8Yo5Ko71-KKQh6MaSudk2vXrN-b.QXwUTN0wiM1YTNwIzW}
```

```
./challenge/./run
Correct!!!
./challenge/./run is a relative path, invoked from the right directory!
```

**Flag:**

```
pwn.college{8Yo5Ko71-KKQh6MaSudk2vXrN-b.QXwUTN0wiM1YTNwIzW}
```

---

## **Implicit Relative Path**

In this level, we'll practice referring to paths using `.` a bit more. This challenge will need you to run it from the `/challenge` directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

```bash
hacker@dojo:~$ cd /challenge
hacker@dojo:/challenge$ run
```

This will *not* invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

```docker
bash: run: command not found
```

We'll explore the mechanisms behind this concept later, but in this challenge, we'll learn how to explicitly use relative paths to launch `run` in this scenario. The way to do this is to *tell* Linux that you explicitly want to execute a program in the current directory, using `.` like in the previous levels. Give it a try now!

### Challenge

```jsx
hacker@paths~implicit-relative-path:/$ cd ./challenge/
hacker@paths~implicit-relative-path:/challenge$ run
bash: run: command not found
hacker@paths~implicit-relative-path:/challenge$ bash run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!

```

 the note we get : 

-This challenge must be called with a relative path that explicitly starts with a `.`!
so we will add to run ( `./run`) 

```jsx
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8WJhydtzv6HkzDkJfrE2ixn8FOe.QXxUTN0wiM1YTNwIzW}
```

**Why `./run` Works**

Think of:

```
.
```

as:

**“where I am right now.”**

So:

```
./run
```

means:

```
current directory + run
```

Since our current directory is `/challenge`:

```
./run
↓
/challenge/run
```

---

## **Home Sweet Home**

Every user has a *home directory*, typically under `/home` in the filesystem. In the dojo, you are the `hacker` user, and your home directory is `/home/hacker`. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:

```bash
hacker@dojo:~$
```

The `~` in this prompt is the current working directory, with `~` being shorthand for `/home/hacker`. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees `~` provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:

```bash
hacker@dojo:~$ echo LOOK: ~
LOOK: /home/hacker
hacker@dojo:~$ cd /
hacker@dojo:/$ cd ~
hacker@dojo:~$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~
hacker@dojo:~$ cd /home/hacker/asdf
hacker@dojo:~/asdf$
```

Note that the expansion of `~` is an *absolute* path, and only the leading `~` is expanded. This means, for example, that `~/~` will be expanded to `/home/hacker/~` rather than `/home/hacker/home/hacker`.

Fun fact: `cd` will use your home directory as the default destination:

```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
```

Now it's your turn to play! In this challenge, `/challenge/run` will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

1. Your argument must be an absolute path.
2. The path must be inside your home directory.
3. Before expansion, your argument must be three characters or less.

Again, you must specify your path as an *argument* to `/challenge/run` as so:

### Challenge

start with  `/challenge/run`

```jsx
hacker@paths~home-sweet-home:~$ /challenge/run
You must provide an argument to /challenge/run when you invoke it!
```

we get You must provide an argument to /challenge/run when you invoke it!

so we will try the clou that says 
`hacker@dojo:~$ /challenge/run YOUR_PATH_HERE`

```jsx
hacker@paths~home-sweet-home:~$ /challenge/run /home/hacker
The argument you provided must not have been longer than 3 characters (it's
currently 12 characters long)!
```

we get The argument you provided must not have been longer than 3 characters (it's
currently 12 characters long)! message , thee trick its This challenge is mainly about **shell expansion**.

we ganna type `/challenge/run ~/f`

```jsx
hacker@paths~home-sweet-home:~$ /challenge/run ~/f
Writing the file to /home/hacker/f!
... and reading it back to you:
pwn.college{I-g8Vactaich8TN5eP2g0hBBX0Y.QXzMDO0wiM1YTNwIzW}
```

Get tha Flag `pwn.college{I-g8Vactaich8TN5eP2g0hBBX0Y.QXzMDO0wiM1YTNwIzW}`

---

**Understanding the Trick**

This challenge is mainly about **shell expansion**.

We type:

```
~/f
```

but Bash expands it before the program receives the argument:

```
~/f
 ↓
/home/hacker/f
```

This lets us satisfy both requirements:

```
Before expansion → short argument
After expansion  → absolute path inside home
```