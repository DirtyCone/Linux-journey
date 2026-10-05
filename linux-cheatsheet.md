# Linux Command Cheatsheet

## Navigation
pwd  Print working directory (where am I)
cd <folder>  Go into a folder
cd..  Go up one level
cd ~ Go home
cd / Go to root (top of system)
ls \ls  List contents (plain ls = \ls, no eza)
ls -l Long format (permissions, size, date)
ls -a  Include hidden (dot) files
ls -la  Both
Tab Autocomplete names and Commands

## Files & Folders
touch <file>  Make an empty file
mkdir <dir>   Make a directory (folder)
mkdir -p a/b/c  Make nested folders at once
cp <src> <dst>  Copy a file
cp -r <src> <dst> Copy a folder + contents
mv <src> <dst>  Move OR rename
rm <file>  Delete a file (permanent, no undo)
rm -r <dir>  Delete a folder + contents
find ~ -name x  Find by name under home
find ~ -type d -name x  Directories only
find ~ -type f -name x  Files only

## Reading Files
cat <file>  Dump whole file (short files)
less <file>  Scrollable viewer (long; q to quit)
head <file>  First 10 lines
tail <file>  Last 10 lines
tail -f <file>  Follow live (Ctrl+C to stop)

## Permissions & Ownership
chmod <mode> <file>  Change permissions
r=4 w=2 x=1 ; three digits = owner/group/others
755 = rwxr-xr-x (runnable by group and other)
chmod +x <file>  Add execute
chown <user>:<group> <file>  Change owner/group (needs sudo)
Permission classes = owner (u) / group (g) / others (o)
UID 0 = root (full access)

## Text Flow
cmd > file  Send output to file (OVERWRITES)
cmd >> file  Append output to file
cmd1 | cmd2  Pipe "|": cmd1 output becomes cmd2 input
grep <pattern>  Filter lines matching pattern (example: ps aux | grep sleep)

## Editor (Neovim)
nvim <file>  open/create file
i  Insert mode (type text)
Esc  Back to Normal mode
:w  Save
:q  Quit
:wq  Save and quit
:q!  Quit without saving
dd  Delete (cut) a line
u  Undo ; Ctrl+r  Redo

## Scripting
#!/bin/bash  Shebang (first line; names interperter)
NAME=value  Set a variable (no spaces around =)
$NAME  Use a variable
$(command)  Command substitution (run cmd, use output)
chmod +x script.sh then ./script.sh  Make runnable, run

## Packages (Arch / Omarchy)
sudo pacman -S <pkg>  Install
sudo pacman -R <pkg>  Remove

## Help
man <command>  Manual for any command
/word search, n next, q quit, g top, G bottom

## Security
ss -tlnp  Listening ports on this machine
journalctl -f  Live system log (Ctrl+C to stop)
journalctl -f | grep UFW  Live firewall blocks only

