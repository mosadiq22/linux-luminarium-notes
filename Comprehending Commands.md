# Comprehending Commands

https://pwn.college/linux-luminarium/commands/ 

---

## cat : not the pet , but the commend

One of the most critical Linux commands is `cat`. `cat` is most often used for reading out files, like so:

```bash
hacker@dojo:~$ cat /path/to/file
Hello Hackers!
```

`cat` will con**cat**enate (hence the name) multiple files if provided multiple arguments. For example:

```bash
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```

### Challenge

In this challenge, I will copy the flag to the `flag` file in your home directory (where your shell starts). Go read it with `cat`!

```jsx
hacker@commands~cat-not-the-pet-but-the-command:~$ ls
Desktop  f  flag
hacker@commands~cat-not-the-pet-but-the-command:~$ cat f
pwn.college{I-g8Vactaich8TN5eP2g0hBBX0Y.QXzMDO0wiM1YTNwIzW}
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{w5pOTQb1Xvx6gTipksyFuzCQY0C.QXxcTN0wiM1YTNwIzW}
```

cat f incorrect 

but flag its on flag file 

```jsx
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{...}
```

get the flag  

---

## catting absolute paths

In the last level, you did `cat flag` to read the flag out of your home directory! You can, of course, specify `cat`'s arguments as absolute paths:

```bash
hacker@dojo:~$ cat /path/to/file
Hello Hackers!
```

### Challenge

In this challenge, I will not copy it to your home directory, but I will make it readable. You can read it with `cat` at its absolute path: `/flag`.

**FUN FACT:** `/flag` is where the flag *always* lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

```jsx
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{...}
```

get the flag 

---

## more catting practice

You can specify all sorts of paths as arguments to commands, and we'll practice some more with `cat`. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with `cd`, so no `cat flag` for you. You must retrieve the flag by absolute path, wherever it is.

### Challenge

You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/share/info/flag. Go cat it out without using cd!

`/usr/share/info/flag`

```jsx
hacker@commands~more-catting-practice:~$ cat /usr/share/info/flag
pwn.college{...}
```

get the flag 

---

## grepping for a needle in a haytsack

Sometimes, the files that you might `cat` out are too big. Luckily, we have the `grep` command to search for the contents we need! We'll learn it in this challenge.

There are many ways to `grep`, and we'll learn one way here:

```bash
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

Invoked like this, `grep` will search the file for lines of text containing `SEARCH_STRING` and print them to the console

### Challenge

In this challenge, I've put a hundred thousand lines of text into the `/challenge/data.txt` file. `grep` it for the flag!

HINT: The flag always starts with the text `pwn.college`.

so what inside data.txt ? 

if we read it by cat we can see some rondom data 

```jsx
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ cat /challenge/data.txt
```

the output a thousandof random data 

here come grep 

let’s to test it 

if we use grep flag /challenge/data.txt 

```jsx
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep flag /challenge/data.txt
camouflage
flagellum's
flagpole
unflagging
flagpole's
```

but with using hint `pwn.college`

so the commend will be 

`grep pwn.college /challenge/data.txt`

```jsx
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{...}
```

get the flag 

---

## Comparing files

When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the `diff` command becomes invaluable.

`diff` compares two files line by line and shows you exactly what's different between them. For example:

```bash
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```

The output tells us that line 2 changed (`2c2`), with `world` in the first file (`<`) being replaced by `universe` in the second file (`>`).

Sometimes, when new lines are added, you'll see something like:

```bash
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

This tells us that after line 1 in the first file, the second file has an additional line (`1a2` means "after line 1 of file1, add line 2 of file2").

### Challenge

Now for your challenge! There are two files in `/challenge`:

- `/challenge/decoys_only.txt` contains 100 fake flags
- `/challenge/decoys_and_real.txt` contains all 100 fake flags plus the one real flag

Use `diff` to find what's different between these files and get your flag!

- `/challenge/decoys_only.txt`

```jsx
hacker@commands~comparing-files:~$ cat /challenge/decoys_only.txt
pwn.college{fake_flag_number_1_Od5YEH3Ek2U}
pwn.college{fake_flag_number_2_fkuAX7uO8ww}
pwn.college{fake_flag_number_3_l6EvuSpToQ}

.
.
.
```

- `/challenge/decoys_and_real.txt`

```jsx
hacker@commands~comparing-files:~$ cat /challenge/decoys_and_real.txt
pwn.college{fake_flag_number_1_Od5YEH3Ek2U}
pwn.college{fake_flag_number_2_fkuAX7uO8ww}
pwn.college{Y2LgGQjexSBJFDEEbB-W6nxEQnw.01MwMDOxwiM1YTNwIzW}
...
```

see a lot of fskr flags , so we ganna use `diff` function to get the flag from both files 

`diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt`

```jsx
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
6a7
> grep pwn.college /challenge/data.txt
```

result one flag 

---

## listung files

So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to **l**i**s**t their contents using the `ls` command!

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

```bash
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

### Challenge

In this challenge, we've named `/challenge/run` with some random name! List the files in `/challenge` to find it. Then invoke the discovered absolute path to get the flag.

```jsx
hacker@commands~listing-files:~$ ls
Desktop  f
hacker@commands~listing-files:~$ cat f
pwn.college{I-g8Vactaich8TN5eP2g0hBBX0Y.QXzMDO0wiM1YTNwIzW}
```

wrong flag so 

let see the directs of folder 

```jsx
hacker@commands~listing-files:~/Desktop$ cd /challenge
hacker@commands~listing-files:/challenge$ ls
28453-renamed-run-7749  Dockerfile
hacker@commands~listing-files:/challenge$ cat 28453-renamed-run-7749
#!/usr/bin/exec-suid -- /bin/bash -p

echo "Yahaha, you found me! Here is your flag:"
cat /flag
```

as we see in message , the flag in dirc `/flag`

```jsx
hacker@commands~listing-files:/$ cat /flag
cat: /flag: Permission denied
```

why does not work ? 

```jsx
#!/usr/bin/exec-suid -- /bin/bash -p
```

This means that the challenge file is designed to be run using a SUID, so that the program obtains the necessary permissions during its operation.

so we ganna do 

```jsx
/challenge/28453-renamed-run-7749
```

we get 

```jsx
Yahaha, you found me! Here is your flag:
pwn.college{...}
```

core idea 

```jsx
hacker
  │
  │ cat /flag
  ▼
Permission denied ❌

hacker
  │
  │ ./28453-renamed-run-7749
  ▼
SUID program
  │
  │ cat /flag
  ▼
Flag ✅
```

Note : ls helped you discover the name of the program, and cat revealed to you what the program does. But having the ability to read /flag directly is not a requirement; The program is designed to read the SUID for you.

---

## touching files

Of course, you can also *create* files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by *touching* it with the `touch` command:

```elixir
hacker@dojo:~$cd /tmp
hacker@dojo:/tmp$ls
hacker@dojo:/tmp$touch pwnfile
hacker@dojo:/tmp$ls
pwnfile
hacker@dojo:/tmp$
```

### Challenge

It's that simple! In this level, please create two files:

- `/tmp/pwn` and `/tmp/college`
- run `/challenge/run` to get your flag!

```jsx
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
```

```jsx
hacker@commands~touching-files:~$ bash /challenge/run
Success! Here is your flag:
cat: /flag: Permission denied
```

let see the code that we run 

```jsx
hacker@commands~touching-files:/challenge$ cat run
#!/usr/bin/exec-suid -- /bin/bash -p

if [ ! -f /tmp/pwn ]
then
        fold -s <<< "Uh oh! /tmp/pwn does not exist. Please use the 'touch' command to create it!"
        exit 1
fi

if [ ! -f /tmp/college ]
then
        fold -s <<< "Uh oh! /tmp/college does not exist. Please use the 'touch' command to create it!"
        exit 2
fi

echo "Success! Here is your flag:"
cat /flag
```

we see 2 condtions of 

- `/tmp/pwn` and `/tmp/college`

theen  its tells 

 you bypass the special executable/SUID behavior of `/challenge/run`.

`let do bash /challenge/run again` 

```jsx
hacker@commands~touching-files:/challenge$ /challenge/run
Success! Here is your flag:
pwn.college{...}
```

we get the flag 

summary work 

```jsx
1. Create required files
   /tmp/pwn
   /tmp/college

2. Execute the SUID challenge correctly
   /challenge/run
```

---

## removing files

Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you **r**e**m**ove files with the `rm` command, as so:

```bash
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

### Challenge

This challenge will create a `delete_me` file in your home directory! Delete it, then run `/challenge/check`, which will make sure you've deleted it and then give you the flag!

1. create a `delete_me` file in your home directory

```jsx
hacker@commands~removing-files:~$ touch delete_me
```

1. run `/challenge/check`

```jsx
hacker@commands~removing-files:~$ bash /challenge/check
It looks like /home/hacker/delete_me still exists! rm it.
```

1. remove [delete.me](http://delete.me) file 

```jsx
hacker@commands~removing-files:~$ bash /challenge/check
Excellent removal. Here is your reward:
cat: /flag: Permission denied
```

let see what in /challenge/check 

```jsx
hacker@commands~removing-files:~$ cat /challenge/check
#!/usr/bin/exec-suid -- /bin/bash -p

if [ -f /home/hacker/delete_me ]
then
        fold -s <<< "It looks like /home/hacker/delete_me still exists! rm it."
else
        fold -s <<< "Excellent removal. Here is your reward:"
        cat /flag
fi
```

we see SUID so know we know how its work 

```jsx
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{...}
```

get the flag

---

## moving files

You can also *move* files around with the `mv` command. The usage is simple:

```bash
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

### Challenge

This challenge wants you to move the `/flag` file into `/tmp/hack-the-planet` (do it)! Note, you *must* use the `mv` command rather than other methods (such as renaming the file in VSCode). When you're done, run `/challenge/check`, which will check things out and give the flag to you

first :  move the `/flag` file into `/tmp/hack-the-planet` by using `mv`

```jsx
hacker@commands~moving-files:~$ mv /tmp/hack-the-planet /flag
ERROR: please make sure that you specify the flag file (/flag)
as your SOURCE! (You specified /tmp/hack-the-planet).
```

why this is wrong , becouse to undertand it ( mv <this file> into <this> 

so the correct way 

```jsx
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
/bin/mv: cannot stat '/flag': No such file or directory
```

note that : /bin/mv: cannot stat '/flag': No such file or directory

so move to root director 

```jsx
hacker@commands~moving-files:/$ cd /
hacker@commands~moving-files:/$
```

after that run `/challenge/check`

```jsx
hacker@commands~moving-files:/$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{...}
```

bravo get the flag 

---

## copying files

But what if you want to keep the original file? You can do so with the `cp` command. The usage is the same as with `mv`, but it will keep the source file. The command is `cp SOURCE DESTINATION`: the first argument is the existing file, and the second is where the copy should be created.

### Challenge

This challenge wants you to copy the `/flag` file to `/tmp/hack-the-planet` (do it)! When you're done, run `/challenge/check`, which will check things out and give the flag to you

**NOTE:** When a `cp` destination is a directory, `cp` places the copy inside it using the source file's name. For this challenge, `/tmp/hack-the-planet` should name the copied file itself, rather than an existing directory.

source ( `/flag`) → destination (`/tmp/hack-the-planet` ) by usting `cp`  , 

the commend wil be `cp /source /destination`  

first : wants you to copy the `/flag` file to `/tmp/hack-the-planet` , run `/challenge/check` 

```jsx
hacker@commands~copying-files:~$ cp /flag /tmp/hack-the-planet
Correct! Performing 'cp /flag /tmp/hack-the-planet'.
```

then run `/challenge/check`

```jsx
hacker@commands~copying-files:~$ /challenge/check
Congrats! You successfully copied the flag to /tmp/hack-the-planet! Here it is:
pwn.college{...}

```

---

## Hidden files

nterestingly, `ls` doesn't list *all* the files by default. Linux has a convention where files that start with a `.` don't show up by default in `ls` and in a few other contexts. To view them with `ls`, you need to invoke `ls` with the `-a` flag, as so:

```bash
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

### Challenge

Now, it's your turn! Go find the flag, hidden as a dot-prepended file in `/`.

first start with `ls -a`  

```jsx
hacker@commands~hidden-files:~$ ls -a
.  ..  .ICEauthority  .bash_history  .cache  .config  .local  .ssh  Desktop  f
```

after see it go to `/.`  by cd 

```jsx
hacker@commands~hidden-files:~$ cd /.
```

using `ls -a`  to see hidden files 

```jsx
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    media  nix  proc  run   srv  tmp  var
..  .flag-41062097710196  boot  dev        home  lib64  mnt    opt  root  sbin  sys  usr
```

you see `.flag-41062097710196`  use cat to read it 

```jsx
hacker@commands~hidden-files:/$ cat .flag-41062097710196
pwn.college{...}
```

bravo get the flag 

---

## An Epic Filesystem Quest

With your knowledge of `cd`, `ls`, and `cat`, we're ready to play a little game!

We'll start it out in `/`. Normally:

```bash
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```

That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the `flag` file and the `challenge` directory.

### Challenge

In this challenge, I have *hidden the flag*! Here, you will use `ls` and `cat` to follow my breadcrumbs and find it! Here's how it'll work:

1. Your first clue is in `/`. Head on over there.
2. Look around with `ls`. There'll be a file named HINT or CLUE or something along those lines!
3. `cat` that file to read the clue!
4. Depending on what the clue says, head on over to the next directory (or don't!).
5. Follow the clues to the flag!

1. Your first clue is in `/`. Head on over there.

```jsx
hacker@commands~an-epic-filesystem-quest:~$ pwd
/home/hacker
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.   .dockerenv  bin   challenge  etc   home  lib64  mnt  opt   root  sbin  sys  usr
..  LEAD        boot  dev        flag  lib   media  nix  proc  run   srv   tmp  var
```

we found that theres LEAD file let read it 

```jsx
hacker@commands~an-epic-filesystem-quest:/$ cat LEAD
Yahaha, you found me!
The next clue is in: /var/lib/man-db

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$
```

The next clue is in: /var/lib/man-db

```jsx
hacker@commands~an-epic-filesystem-quest:/$ cd /var/lib/man-db
hacker@commands~an-epic-filesystem-quest:/var/lib/man-db$ ls
CLUE  auto-update
```

read file CLUE

```jsx
hacker@commands~an-epic-filesystem-quest:/var/lib/man-db$ cat CLUE
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__
```

The next clue is in: `/usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__`

```jsx
hacker@commands~an-epic-filesystem-quest:/var/lib/man-db$ cd  /usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__$ ls -a
.  ..  WHISPER  __init__.cpython-312.pyc  known.cpython-312.pyc
```

read file **`WHISPER`**

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__$ cat WHISPER
Tubular find!
The next clue is in: /usr/share/doc/python3-packaging

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```

The next clue is in: /usr/share/doc/python3-packaging

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.

so we go to 

`cd /usr/share/doc/python3-packaging`

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/util/crc/__pycache__$ cd /usr/share/doc/python3-packaging
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ ls
SPOILER  changelog.Debian.gz  copyright
```

read filr SPOILER 

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat SPOILER
Yahaha, you found me!
The next clue is in: /usr/lib/python3/dist-packages/pip/_internal/cli

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```

The next clue is in: /usr/lib/python3/dist-packages/pip/_internal/cli
Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct! 

so i did rad by cd and that what happend 

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cd /usr/lib/python3/dist-packages/pip/_internal/cli
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pip/_internal/cli$ ls
INFO-TRAPPED  autocompletion.py  command_context.py  parser.py         spinners.py
__init__.py   base_command.py    main.py             progress_bars.py  status_codes.py
__pycache__   cmdoptions.py      main_parser.py      req_command.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pip/_internal/cli$ cat INFO-TRAPPED
BOOM! This hint has self-destructed because you entered this directory (using cd)! You will need to restart the challenge to continue.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pip/_internal/cli$

```

now i need to redtart the challenge 

from SPOTLER file 

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat SPOILER
Yahaha, you found me!
The next clue is in: /usr/lib/python3/dist-packages/pip/_internal/cli

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ ls /usr/lib/python3/dist-packages/pip/_internal/cli
INFO-TRAPPED  autocompletion.py  command_context.py  parser.py         spinners.py
__init__.py   base_command.py    main.py             progress_bars.py  status_codes.py
__pycache__   cmdoptions.py      main_parser.py      req_command.py
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat /usr/lib/python3/dist-packages/pip/_internal/cli/INFO-TRAPPED
Great sleuthing!
The next clue is in: /var/lib/apt/lists

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$

```

The next clue is in: /var/lib/apt/lists Watch out! The next clue is **trapped**. 

You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$

The next clue is also **trapped**, so you must **NOT** use `cd`. Stay exactly where you are at `/usr/share/doc/python3-packaging`.

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ ls /var/lib/apt/lists
DOSSIER-TRAPPED
archive.ubuntu.com_ubuntu_dists_noble-backports_InRelease
archive.ubuntu.com_ubuntu_dists_noble-backports_main_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-backports_multiverse_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-backports_universe_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-updates_InRelease
archive.ubuntu.com_ubuntu_dists_noble-updates_main_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-updates_multiverse_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-updates_restricted_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble-updates_universe_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble_InRelease
archive.ubuntu.com_ubuntu_dists_noble_main_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble_multiverse_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble_restricted_binary-amd64_Packages.lz4
archive.ubuntu.com_ubuntu_dists_noble_universe_binary-amd64_Packages.lz4
auxfiles
lock
partial
security.ubuntu.com_ubuntu_dists_noble-security_InRelease
security.ubuntu.com_ubuntu_dists_noble-security_main_binary-amd64_Packages.lz4
security.ubuntu.com_ubuntu_dists_noble-security_multiverse_binary-amd64_Packages.lz4
security.ubuntu.com_ubuntu_dists_noble-security_restricted_binary-amd64_Packages.lz4
security.ubuntu.com_ubuntu_dists_noble-security_universe_binary-amd64_Packages.lz4
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$
```

Remember, **do not use `cd`**. Stay exactly where you are and read the file by executing `cat` with the absolute path:

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat /var/lib/apt/lists/DOSSIER-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/common

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$
```

The next clue is in: `/usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/common`

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.

It is **not** trapped or delayed, but to play it completely safe and avoid any hidden triggers, let's **stay where we are** and list the hidden files from a distance using `ls -a`.

```jsx
ls -a /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/common
.  ..  .BRIEF  __doc__  freebsd  label.asm  linux
```

Excellent! The hidden file is **`.BRIEF`**.Since it is safe to read from where you are, run `cat` using its full absolute path:

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/common/.BRIEF
Congratulations, you found the clue!
The next clue is in: /var/cache/apt/archives
```

Congratulations, you found the clue!
The next clue is in: `/var/cache/apt/archives`

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ ls /var/cache/apt/archives
REVELATION  lock  partial
```

The clue file inside that directory is named **`REVELATION`**

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat /var/cache/apt/archives/REVELATION
Yahaha, you found me!
The next clue is in: /usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```

The next clue is in: `/usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata`

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.

so te commend `ls -a /usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata`

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ ls -a /usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata
.   .DISPATCH    __pycache__   _collections.py  _functools.py  _meta.py        _text.py
..  __init__.py  _adapters.py  _compat.py       _itertools.py  _py39compat.py
```

The hidden file is **`.DISPATCH`**.

Commend:`cat /usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata/.DISPATCH`

```jsx
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/python3-packaging$ cat /usr/lib/python3/dist-packages/setuptools/_vendor/importlib_metadata/.DISPATCH
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{...}
```

and DONE 

---

## making directories

We can create files. How about directories? You **m**a**k**e **dir**ectories using the `mkdir` command. Then you can stick files in there!

Watch:

```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```

### Challenge

Now, go forth and create a `/tmp/pwn` directory and make a `college` file in it! Then run `/challenge/run`, which will check your solution and give you the flag!

create a `/tmp/pwn` directory 

```jsx
hacker@commands~making-directories:~$ mkdir /tmp/pwn
```

 make a `college` file in it

```jsx
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ ls
college
```

Then run `/challenge/run`

```jsx
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{...}
```

Well Done 

---

## finding files

So now we know how to list, read, and create files. But how do we find them? We use the `find` command!

The `find` command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, `find` matches every file. If you don't specify a search location, `find` uses the current working directory (`.`). For example:

```bash
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```

And when specifying the search location:

```bash
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```

And, of course, we can specify the criteria! For example, here, we filter by name:

```bash
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```

You can search the whole filesystem if you want!

```bash
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```

### Challenge

Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called `flag`. Go find it!

Several notes. First, there are other files named `flag` on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause `find` to generate errors, but you can ignore those; we won't hide the flag there! Finally, `find` can take a while; be patient!

first lets use `find / -name flag`

u will  see a lot of promission denied 

```jsx
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
```

If you want to hide Permission denied messages while searching:

`find / -name flag 2>/dev/null`

```jsx
hacker@commands~finding-files:/usr/lib/python3/dist-packages/pwnlib/flag$ find / -name flag 2>/dev/null
/usr/lib/python3/dist-packages/pwnlib/flag
/usr/share/terminfo/x/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/c07wba3nrck81kdh0yg5h8rx22di35xi-radare2-6.0.4/share/radare2/6.0.4/flag
/nix/store/gfyhjlxav9nczmnanb3jxr73kb22yp42-rizin-0.8.1/share/rizin/flag
/nix/store/61dd247b72i7xnm0mw9qaxgfx3gs2lyy-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/sh1s72wwgvcq50kp830nlhm5cjpxmyh7-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/1wn496frzskd2drjwyyskk3g50rd1nbd-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/rszkfmr2mp5r4dyvhwqcj3521nyqfyzc-rizin-0.8.2/share/rizin/flag
/nix/store/kdlmh9h9hmq225jarh6rk927lb7jsxsv-radare2-6.1.8/share/radare2/6.1.8/flag
/nix/store/p9vjrnqyl7hy1k0ik9dw0lb9ib3c4582-python3.13-pwntools-4.15.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/f42x3k5mrk3qq79ixwy991p6g6a5l9f6-python3.13-pwntools-4.15.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/hss94rqc4ha0y229f8fwcy304wnzdsq7-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/4ckl0p6mafmm242c9qv3sln5dbd9rr9j-source/packages/core/src/flag
```

we can not read all the files 

but we know the flag start  with [pwn.college](http://pwn.college) so wee can type commend  

`find / -type f -name flag -readable -exec grep -H "pwn.college" {} \; 2>/dev/null` 

find / ← Search the system

- name flag ← The files are named flag
- readable ← readable
- exec grep ... ← Search for pwn.college

```jsx
hacker@commands~finding-files:~$ find / -type f -name flag -readable -exec grep -H "pwn.college" {} \; 2>/dev/null
/usr/share/terminfo/x/flag:pwn.college{...}
```

and Well done , Found the flag 

---

## linking files

If you use Linux (or computers) for any reasonable length of time to do any real work, you will eventually run into some variant of the following situation: you want two programs to access the same data, but the programs expect that data to be in two different locations. Luckily, Linux provides a solution to this quandary: *links*.

Links come in two flavors: *hard* and *soft* (also known as *symbolic*) links. We'll differentiate the two with an analogy:

- A **hard** link is when you address your apartment using multiple addresses that all lead directly to the same place (e.g., `Apt 2` vs `Unit 2`).
- A **soft** link is when you move apartments and have the postal service automatically forward your mail from your old place to your new place.

In a filesystem, a file is, conceptually, an address at which the contents of that file live. A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data. A soft/symbolic link, instead, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file. In most cases, both situations result in accessing the original data, but the mechanisms are different.

Hard links sound simpler to most people (case in point, I explained it in one sentence above, versus two for soft links), but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.

In this challenge, we will learn about symbolic links (also known as *symlinks*). Symbolic links are created with the `ln` command using the syntax `ln -s TARGET LINK_NAME`. `TARGET` is the path that the link will point to, and `LINK_NAME` is the new path you are creating. For example:

```bash
hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
```

You can see that accessing the symlink results in getting the original file contents! In this example, `/tmp/myfile` is the target and `/home/hacker/ourfile` is the link name.

A symlink can be identified as such with a few methods. For example, the `file` command, which takes a filename and tells you what type of file it is, will recognize symlinks:

```bash
hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
```

### Challenge

now you try it! In this level the flag is, as always, in `/flag`, but `/challenge/catflag` will instead read out `/home/hacker/not-the-flag`. The path `/home/hacker/not-the-flag` is the link name in this challenge. Choose the target that will fool `/challenge/catflag` into giving you the flag!

---

**WARNING:** If a previous experiment left something at `/home/hacker/not-the-flag`, remove it first so `ln` can create the symbolic link there.

1. Delete any old file

```jsx
hacker@commands~linking-files:~$ rm -f /home/hacker/not-the-flag
```

2. Create a symbolic link

```jsx
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
```

meams 

<aside>
💡

/flag

↑

│ Target

│

not-the-flag

↑

│ Symlink

│

/home/hacker/not-the-flag

</aside>

3. Run the program

```jsx
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{...}
```

and Well Done
