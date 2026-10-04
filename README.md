# Linux Luminarium — pwn.college Writeups

My personal notes and solutions for the [Linux Luminarium](https://pwn.college/linux-luminarium/) course on **pwn.college**, covering Linux fundamentals for offensive security practice: file paths, permissions, regex, and more.

> ⚠️ Real flags have been redacted from these writeups. This content is for educational/reference purposes only.

## Progress

| Module | Status |
| --- | --- |
| Paths | ✅ Done |
| Commands | ✅ Done |
| Digesting Documentation | ✅ Done |
| File Globbing | ✅ Done |
| Permissions | 🔲 Not started |
| Regex | 🔲 Not started |

## Notes

- [**Pondering Paths**](./Pondering%20Paths.md) — Linux filesystem basics: absolute vs. relative paths, navigating with `.`/`..`, and how the shell expands `~` before a program ever sees it.
- [**Comprehending Commands**](./Comprehending%20Commands.md) — Core file/command tools: `cat`, `grep`, `diff`, `ls`, `mkdir`, `find`, and symbolic links with `ln`.
- [**Digesting Documentation**](./Digesting%20Documentation.md) — Getting help from the system: reading arguments, `man` pages, searching with `/` and `man -k`, `--help`, and the `help` builtin.
- [**File Globbing**]([./File%20Globbing.md](https://github.com/mosadiq22/linux-luminarium-notes/blob/feb7fbe03bdbab7b21adbda4f790f43096cdffa7/File%20Globbing)) — Shell wildcards: `*`, `?`, `[]`, exclusion with `[^]`/`[!]`, combining multiple globs, and tab completion for files and commands.

## About Me

- GitHub: [@mosadiq22](https://github.com/mosadiq22)
- TryHackMe: [mbq10](https://tryhackme.com/p/mbq10)
- Networks & Cybersecurity student, focused on offensive/ethical penetration testing

## Disclaimer

These notes are written for learning purposes as I work through pwn.college challenges. Feel free to use them as a reference, but I'd encourage you to solve challenges yourself first!
