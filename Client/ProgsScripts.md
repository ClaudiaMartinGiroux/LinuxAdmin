# Programs and Scripts

General info on Source Code, Interpreters, Compilers, bit on Makefiles and how scripts are interpreted.
Did Hello World examples for C, Perl, Python and Bash.

## Pipes
Let's say we have hello.c and we want to do a word count on hello (so use `wc` command for that).
- doing `./hello | wc` to redirect output to the wc command
- another example `ls -l | sort | wc` so we pass 'ls -l' to 'sort' which goes to the word count

## Files
Use `file [input]` to tell you info about a file or directory of files.
