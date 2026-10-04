# Digesting Documentation

https://pwn.college/linux-luminarium/man/

---

## Learning From Documentation

The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the `-a` of `ls -a` in the `hidden files` challenge of the [Basic Commands](https://pwn.college/linux-luminarium/commands) module: that `-a` was an *argument* that told `ls` to list out hidden files as well as non-hidden files. Because we *wanted* to list out hidden files, invoking `ls` with the `-a` argument was the correct way to use it in our scenario.

#### Challenge

Welcome to the documentation for `/challenge/challenge`! To properly run this program, you will need to pass it the argument of `--giveflag`. Good luck!

```jsx
/challenge/challenge   --giveflag
        │                  │
      Program            Argument
```

which means 

- /challenge/challenge → the program you want to run.
- --giveflag → argument We pass it to the program.
- The program recognizes --giveflag and gives you the flag.

```jsx
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{...}
```

Done ✅

---

## Learning Complex Usage

While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like `sed` and `awk`, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between `cd` and `awk` are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the `find` level in [Basic Commands](https://pwn.college/linux-luminarium/commands). `find` has a `-name` argument, and the `-name` argument itself takes an argument specifying the name to search for. Many other commands are analogous.

#### Challenge

Welcome to the documentation for `/challenge/challenge`! This program prints arbitrary files to the terminal when given the `--printfile` argument. The argument to `--printfile` is the path of the file to read. For example, `/challenge/challenge --printfile /etc/hostname` will print the container's hostname!

```jsx
/challenge/challenge --printfile <path>
```

- /challenge/challenge → program
- --printfile → tells the program that we want to print a file
- After --printfile, we must put the path to the file we want to read.

```jsx
/challenge/challenge   --printfile   /flag
        │                    │           │
     Program              Argument    Argument
                 program --printfile
```

Answer : 

```jsx
hacker@man~learning-complex-usage:~$  /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{...}
```

Done ✅

---

## Reading Manuals

`man` is short for **manual**. It is used to display the documentation for a command.

Example:

```
man yes
```

This opens the **manual page** for the `yes` command.

Important `man` sections:

```
NAME
→ The name of the command and a short description.

SYNOPSIS
→ Shows how to use the command and its arguments.

DESCRIPTION
→ Explains the command and its options in detail.

SEE ALSO
→ Other related commands or manual pages.
```

Navigation:

```
↑ ↓       → Move up/down
PgUp/PgDn → Move between pages
q         → Quit the manual
```

> **Note:** `q` only works for quitting when you are inside `man`. If you type `q` in the normal terminal, Bash will try to run a command called `q`.

#### Challenge

The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for `challenge`!

The challenge has a **secret option** that prints the flag. We need to discover it from the `man` page.

First:

```
man challenge
```

We found:

```
--fortune
       read a fortune

--version
       output version information and exit

--jhfuju NUM
       print the flag if NUM is 849
```

The important part is:

```
--jhfuju NUM
```

This means `--jhfuju` requires an additional **argument**.

The required number is:

```
849
```

So the correct command is:

```
/challenge/challenge --jhfuju 849
```

❌ Incorrect

```
/challenge/challenge --jhfuju NUM849
```

Why?

Because `NUM` is a **placeholder**. It means:

> "Put a number here."
> 

It is **not** something we type literally.

✅ Answer

```
hacker@man~reading-manuals:~$ /challenge/challenge --jhfuju 849
Correct usage! Your flag: pwn.college{...}
```

---

## Searching Manuals

You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with `/`. After searching, you can hit `n` to go to the next result and `N` to go to the previous result. Instead of `/`, you can use `?` to search backwards!

#### Challenge

Find the option that will give you the flag by reading the `challenge` man page.

```jsx
hacker@man~searching-manuals:~$ man challenge
```

```jsx
CHALLENGE(1)                                             Challenge Commands                                            CHALLENGE(1)

NAME
     /challenge/challenge - print the flag!

SYNOPSIS
     challenge OPTION

DESCRIPTION
     Output the flag when called with the right argument.

     --fortune
            read a fortune

     --version
            output version information and exit

.
.
.

```

 you can hit `n` to go to the next result and `N` to go to the previous result

```jsx

                   SUMMARY OF LESS COMMANDS

      Commands marked with * may be preceded by a number, N.
      Notes in parentheses indicate the behavior if N is given.
      A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.

  h  H                 Display this help.
  q  :q  Q  :Q  ZZ     Exit.
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  ESC-j             *  Forward  one file line (or N file lines).
  ESC-k             *  Backward one file line (or N file lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  ESC-b             *  Backward one window, but don't stop at beginning-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Right one half screen width (or N positions).
  ESC-(  LeftArrow  *  Left  one half screen width (or N positions).
  ESC-}  ^RightArrow   Right to last column displayed.
  ESC-{  ^LeftArrow    Left  to first column.
  F                    Forward forever; like "tail -f".
  ESC-F                Like F but stop when search pattern is found.
  ESC-f                Like F but ring the bell when search pattern is found.
  r  ^R  ^L            Repaint screen.
  R                    Repaint screen, discarding buffered input.
        ---------------------------------------------------
        Default "window" is the screen height.
        Default "half-window" is half of the screen height.
 ----------------------------------------------------------------
 .
 .
 .
 
```

Inside the man page, press `/` then type `flag` and hit Enter to jump to the matches 

![Searching for flag inside man page](images/searching-manuals-flag.png)

```jsx
     --swztk
            This argument will give you the flag!
```

try this `/challenge/challenge --swztk`

```jsx
hacker@man~searching-manuals:~$ /challenge/challenge --swztk
Initializing...
Correct usage! Your flag: pwn.college{...}
```

and Done ✅✅

> n → next search result
N → previous search result
? → search backwards
> 

---

## Searching For Manuals

This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the manpages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right manpage, read the `man` page manpage by doing: `man man`!

#### Challenge

**HINT 1:** `man man` teaches you advanced usage of the `man` command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use `/challenge/challenge`

**HINT 2:** though the manpage is randomly named, you still actually use `/challenge/challenge` to get the flag!

So:

```
man challenge
```

will **not** work.

so we take first hint  use `man man`

```jsx
hacker@man~searching-for-manuals:~$ man man
```

The important option is:

```
-k
```

- `k` searches the man-page database for a keyword.

```jsx
hacker@man~searching-for-manuals:~$ man -k challenge
vvcvgyfwiw (1)       - print the flag!
```

read `vvcvgyfwiw`

```jsx
hacker@man~searching-for-manuals:~$ man vvcvgyfwiw

CHALLENGE(1)                                           Challenge Commands                                           CHALLE
NGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --vvcvgy NUM
              print the flag if NUM is 154

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                 May 2024                                                CHALLENGE
```

that what we need `--vvcvgy NUM`

Inside it, you'll find the instructions for `/challenge/challenge`.

open it with:

```
/challenge/challenge <option> 
```

in this situation he have `--vvcvgy 154`

```jsx
hacker@man~searching-for-manuals:~$ /challenge/challenge --vvcvgy 154
Correct usage! Your flag: pwn.college{...}
```

Well Done ✅

---

## Helpful Programs

Some programs don't have a man page, but might tell you how to run them if invoked with a special argument. Usually, this argument is `--help`, but it can often be `-h` or, in rare cases, `-?`, `help`, or other esoteric values like `/?` (though that latter is more frequently encountered on Windows).

—help , -h , -? ,help /?

#### Challenge

In this level, you will practice reading a program's documentation with `--help`. Try it out!

we will use `/challenge/challenge --help`

```jsx
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]

options:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you
                        the flag
```

after view the options we can see `-g` but read carefully  

```jsx
hacker@man~helpful-programs:~$ /challenge/challenge -g
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: expected one argument
```

so first we’ll do `-p`

```jsx
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 149
```

Now use the secret value with `-g <NUM>`

```jsx
hacker@man~helpful-programs:~$ /challenge/challenge -g 149
Correct usage! Your flag: pwn.college{...}
```

Well Done ✅

---

## Help for Builtins

Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called *builtins*. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the *builtin* `help`, as so:

```bash
hacker@dojo:~$ help
```

You can get help on a specific one by passing it to the `help` builtin. Let's look at a builtin that we've already used earlier, `cd`!

```bash
hacker@dojo:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.

    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
...
```

#### Challenge

Some good information! In this challenge, we'll practice using `help` to look up help for builtins. This challenge's `challenge` command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it!

first use `help challenge`  

```jsx
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "ox1krBwM".
```

we will use --secret VALUE and the value its (ox1krBwM) 

```jsx
hacker@man~help-for-builtins:~$ challenge --secret ox1krBwM
Correct! Here is your flag!
pwn.college{...}

```

Well Done ✅
