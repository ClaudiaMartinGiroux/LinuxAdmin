# Linux Commane Line

**use `man` for manuals** 
Can also use `man # [command]` to see specific # of the man page for that command.

## View & create files
- Use `cat` to view but also nano, emacs, vim... to edit too.
- `mv [old] [new]` to move or remane
- `touch [filename]` to create empty file
- `rm [file]` but also take link would be `unlink [file]`

## File editing & searching
- Use `nano [filename]` to open and edit. _ctrl + x_ to leave. Similar for other editors.
- use `grep [what you looking for] [dir]` to find files that contain that. dir can be `*` to look at everything in local dir or `*/*` for dirs in local dir.

## Directory and Home Directory
- `pwd` present working directory
- `cd ~` or `cd .` or `cd` take you home (country road)
- `ls -a` and `ls -la` give more info and `ls -al` shows hidden files. Use `ls -l` to see number of links pointing to file. if number is 0, memory is released (use `unlink`)
- `mkdir [dir]` to make xD
- `rmdir [dir]` to remove directory but if it's empty so use `rm -rf`

## Environment variables
Name value pairs that are stored and your programs can use. For example: username [username: steve], paths...
`env` to show the environment vals. use `$[NAME]` to use the env variables.

## Terminal redirection
- something `>` something is to redirect output to file
- `<` direct file content into the input
- something `>>` something is appending to end of file...
- Date example: `$ date > 'date +"%d-%m-%Y"'.txt`

## Links
Links are entries that tell you where the contents are in the system (shortcut locations).
- `ln [file] [file2]` for hardlinks
- `ln -s [file] [file3]' for a symbolyc link
They will all have same contents (with hard and symlinks) but if we want to remove file, file2 will remain there with contents but file3 might still appear in dir but has no contents.

## Absolute vd Relative Path
#### Absolute
Starts with root of the system all the way down to location of path: `/[something]/`
Absolute path will always work.
#### Relative
Based on where you are currently at: `./[something]/`