# File Globbing

## Matching with *

The first glob we'll learn is `*`. When it encounters a `*` character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```

Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```

When zero files are matched, by default, the shell leaves the glob unchanged:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```

The `*` matches any part of the filename except for `/` or a leading `.` character. For example:

```bash
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

#### Challenge

Now, practice this yourself! Starting from your home directory, change your directory to `/challenge`, but use globbing to keep the argument you pass to `cd` to at most four characters! Once you're there, run `/challenge/run` for the flag!

Lets see first 

```jsx
hacker@globbing~matching-with-:~$ ls
This challenge resets your working directory to /home/hacker unless you change
directory properly...
```

if we write `echo file_*`

```jsx
file_*
  ↓
file_a file_b file_c
```

so i will going to searching for match  `/cha*`

```jsx
hacker@globbing~matching-with-:~$ cd /cha*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
```

becomes:

```
cd /challenge
```

and `/challenge` is **10 characters**, so it gets rejected.

```jsx
hacker@globbing~matching-with-:~$ cd /challenge
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
```

and want:

```
/challenge
```

There is a directory entry `challenge` at `/`, so we need a glob pattern that expands to a path of ≤4 characters. The key is to use `*` to match the **entire path component**:

```
cd /*
```

we will try every passiople ways so that we get 

`cd /*` , `cd /???*` , `cd /c*`

```jsx
hacker@globbing~matching-with-:~$ cd /*
bash: cd: too many arguments
hacker@globbing~matching-with-:~$ cd /???*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
hacker@globbing~matching-with-:~$ cd /c*
hacker@globbing~matching-with-:/challenge$
```

to `ls`  to see and run the file 

```jsx
hacker@globbing~matching-with-:/challenge$ ls
Dockerfile  run
```

and running `run`  file 

```jsx
hacker@globbing~matching-with-:/challenge$ ./run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{...}
```

Well Done 

---

## Matching with ?

Next, let's learn about `?`. When it encounters a `?` character in any argument, the shell will treat it as a **single-character** wildcard. This works like `*`, but only matches *one* character. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

#### Challenge

Now, practice this yourself! Starting from your home directory, change your directory to `/challenge`, but use the `?` character instead of `c` and `l` in the argument to `cd`! Once you're there, run `/challenge/run` for the flag!

we will first try `?ha?lenge`

```jsx
hacker@globbing~matching-with-:~$ cd /?ha?lenge
You used either the 'c', 'l', or '*' characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
```

Disallowed , add ? with second l 

try this `?ha??enge`

```jsx
hacker@globbing~matching-with-:~$ cd /?ha??enge
```

and 

```jsx
hacker@globbing~matching-with-:/challenge$ ls
Dockerfile  run
hacker@globbing~matching-with-:/challenge$ ./run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{...}
```

Well Done 

---

## Matching with []

Next, we will cover `[]`. The square brackets are, essentially, a limited form of `?`, in that instead of matching any character, `[]` is a wildcard for some subset of potential characters, specified within the brackets. For example, `[pwn]` will match the character `p`, `w`, or `n`. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

#### Challenge

Try it here! We've placed a bunch of files in `/challenge/files`. Change your working directory to `/challenge/files` and run `/challenge/run` with a single argument that bracket-globs into `file_b`, `file_a`, `file_s`, and `file_h`!

```jsx
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ ls
file_a  file_d  file_g  file_j  file_m  file_p  file_s  file_v  file_y
file_b  file_e  file_h  file_k  file_n  file_q  file_t  file_w  file_z
file_c  file_f  file_i  file_l  file_o  file_r  file_u  file_x
hacker@globbing~matching-with-:/challenge/files$
```

after this step So use:  `/challenge/run file_[bash]` 

how its going work ? 

The shell expansion will work like this:

```jsx
file_[bash]
     ↓
file_b file_a file_s file_h
```

Then it actually becomes:

```jsx
/challenge/run file_b file_a file_s file_h
```

so 

```jsx
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{...}
```

Well Done 

---

## Matching paths with []

Globbing happens on a *path* basis, so you can expand entire paths with your globbed arguments. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

#### Challenge

First 

```jsx
hacker@globbing~matching-paths-with-:~$ cd /challenge/files
hacker@globbing~matching-paths-with-:/challenge/files$
```

all the result 

```jsx
hacker@globbing~matching-paths-with-:/challenge/files$ ls
file_a  file_d  file_g  file_j  file_m  file_p  file_s  file_v  file_y
file_b  file_e  file_h  file_k  file_n  file_q  file_t  file_w  file_z
file_c  file_f  file_i  file_l  file_o  file_r  file_u  file_x
```

and running input 

```jsx
hacker@globbing~matching-paths-with-:/challenge/files$ /challenge/run file_[bash]
Error: please run with a working directory of /home/hacker!
```

The only problem here is that you are not in /home/hacker

Return to home:

```jsx
hacker@globbing~matching-paths-with-:/challenge/files$ cd ~
hacker@globbing~matching-paths-with-:~$
```

and running input 

```jsx
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{...}
```

And Done 

---

## Multiple globs

So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

```bash
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```

What happens above is that the shell looks for all files in `/` that start with *anything* (including nothing), then have an `f` and an `l`, and end in *anything* (including `ag`, which makes `flag`).

#### Challenge

Now you try it. We put a few happy, but diversely-named files in `/challenge/files`. Go `cd` there and run `/challenge/run`, providing a single argument: a short (3 characters or less) globbed word with two `*` globs in it that covers every word that contains the letter `p`.

start with 

```jsx
hacker@globbing~multiple-globs:/$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial

```

then start with P 

why is P ?

Because the challenge says:

> **every word that contains the letter `p`**
> 

So `p` is the **literal character we're searching for**.

For example:

```
happy
  ↑
  p
```

And:

```
optimistic
  ↑
  p
```

The pattern:

```
*p*
```

so `/challenge/run *p*`

```jsx
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{...}
```

and Done 

---

## Mixing globs

#### Challenge

Now, let's put the previous levels together! We put a few happy, but diversely-named files in `/challenge/files`. Go `cd` there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to `/challenge/run`) will match **only** the files "challenging", "educational", and "pwning"!

---

**HINT:** Make sure to look at the names of the files in `/challenge/files`. Do you see any patterns that could help you make your glob?

Look at the three target names:

```
challenging
educational
pwning
```

They all **end with `ing`**.

Start by going to the directory

```jsx
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
hacker@globbing~mixing-globs:/challenge/files$

```

A good way to solve these levels is to test a candidate with:

```jsx
hacker@globbing~mixing-globs:/challenge/files$ echo *ing
amazing challenging laughing pwning thrilling uplifting
```

Try:

```jsx
hacker@globbing~mixing-globs:/challenge/files$ echo *a*
amazing beautiful challenging educational fantastic great happy jovial laughing magical radiant xenial
```

Try : 

```jsx
hacker@globbing~mixing-globs:/challenge/files$ echo *n*
amazing challenging educational fantastic incredible kind laughing nice pwning queenly radiant splendid thrilling uplifting wonderful xenial
```

Exactly. `*n*` is still too broad.

We can use the **first letter** to narrow it down with a bracket glob:

```
echo [cep]*n*
```

Why?

- `[cep]` → first character must be `c`, `e`, or `p`
- → anything in between
- `n` → must contain `n`
- → anything after

```jsx
hacker@globbing~mixing-globs:/challenge/files$ echo [cep]*n*
challenging educational pwning
```

Then run:

```jsx
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{...}
```

Done 

---

## Exclusionary globbing

Sometimes, you want to filter out files in a glob! Luckily, `[]` helps you do just this. If the first character in the brackets is a `!` or (in newer versions of bash) a `^`, the glob inverts, and that bracket instance matches characters that *aren't* listed. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

#### Challenge

Armed with this knowledge, go forth to `/challenge/files` and run `/challenge/run` with all files that don't start with `p`, `w`, or `n`!

**NOTE:** The `!` character has a different special meaning in bash when it's not the first character of a `[]` glob, so keep that in mind if things stop making sense! `^` does not have this problem, but is also not compatible with older shells.

start with : 

```jsx
hacker@globbing~exclusionary-globbing:~$ cd  /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
```

run `/challenge/run` with all files that don't start with `p`, `w`, or `n`! 

take look in `echo [^pwn]*`

```jsx
hacker@globbing~exclusionary-globbing:/challenge/files$ echo [^pwn]*
amazing beautiful challenging delightful educational fantastic great happy incredible jovial kind laughing magical optimistic queenly radiant splendid thrilling uplifting victorious xenial youthful zesty
```

then running code with 

```jsx
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{...}
```

and Done 

---

## tab completion

As tempting as it might be, using `*` to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the `rm` command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is *tab completion*. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

#### Challenge

This challenge has copied the flag into `/challenge/pwncollege`, and you can freely `cat` that file. But you can't type the filename: we used some serious trickery to make sure that you *must* tab-complete it. Try it out!

```bash
hacker@dojo:~$ ls /challenge
Dockerfile  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

so start with do to directory  :

```jsx
hacker@globbing~tab-completion:~$ pwd
/home/hacker
hacker@globbing~tab-completion:~$ cd /challenge
hacker@globbing~tab-completion:/challenge$ ls
Dockerfile  pwncollege
```

then cat pwncollege file 

```jsx
hacker@globbing~tab-completion:/challenge$ cat pwncollege
pwn.college{...}
```

Done !! 

---

## multiple options for  tab completion

Consider the following situation:

```bash
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default `bash` will auto-expand until the first point when there are multiple options (in this case, `fl`). When you hit tab a *second* time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

#### Challenge

This challenge has a `/challenge/files` directory with a bunch of files starting with `pwncollege`. Tab-complete from `/challenge/files/p` or so, and make your way to the flag!

if we try to `ls`  

```jsx
hacker@globbing~multiple-options-for-tab-completion:~$ ls
No ls for you in this level! Use tab-completion instead!
```

go to directory `/challenge/files`  

```jsx
hacker@globbing~multiple-options-for-tab-completion:~$ cd /challenge/files
```

Since all files start with pwncollege, start by typing: `cat p`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat p
```

then pw + tap  :  `cat pwncollege`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege
```

we see `cat pwncollege-`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege-
```

try every letter and u will see result like this  `cat pwncollege-hacking`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege-hacking
```

we get message `No flag in this file!`  so keep trying 

we get the match `cat pwncollege-f`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege-f
pwncollege-family      pwncollege-flag        pwncollege-flamingo    pwncollege-flyswatter
```

choice flag and `pwncollege-flag`

```jsx
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege-flag
pwn.college{...}
```

Done !!

---

## tab completion on commands

Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with `pwncollege`, and it'll give you the flag. Type `pwncollege` and hit the tab key to auto-complete it!

---

**NOTE:** You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

#### Challenge

start with `pwncollege` + TAP 

the completion 

```jsx
hacker@globbing~tab-completion-on-commands:~$ pwncollege-13575
Correct! Here is your flag:
pwn.college{...}
```

Done !!