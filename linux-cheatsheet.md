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

## Git & GitHub
git init  Turn folder into a repo
git status  See what changed / staged
git add <file>  Stage a file (git add . = all)
git commit -m "msg"  Save a snapshot
git push  Upload commits to GitHub
git pull  Download commits from GitHub
git log  Commit history (q to quit)
git clone <url>  Download a repo
git remote -v  Show linked GitHub URL
git remote set-url origin <url>  Change linked URL
gh auth login  Log machine into GitHub
gh auth status  Check Github login
gh repo create <name> --private --source=. --push
loop: add, commit, push
.env = secrets, never commit, keep in .gitignore

## Shell Customization
source ~/.bashrc  Reload config after editing
alias name="command"  Make a shortcut
function: mkcd() { mkdir -p "$1" && cd "$1"; }  Make + enter a folder in one command
$1 = first argument passed to a function
# at line start = comment (disabled line)

## Packages
Arch/Omarchy: sudo pacman -S <pkg>
AUR (Omarchy extras): yay -S <pkg>  Use <pkg>-bin for precompiled (faster)
Ubuntu/Debian: sudo apt install <pkg>
Update Ubuntu: sudo apt update && sudo apt upgrade -y

## SSH & Remote Servers
ssh user@ip  Connect to a remote machine
exit  Disconnect (back to local)
First connect ask to trust host  Type yes
hostname  Shows which machine you're on
private IP (192.168.x.x) = Local network only
rachable only on same network (no internet exposure)

## Networking (checks)
ip route | grep default  Show gateway + interface
ping -c 3 <host>  Test internet (3 pings, then stop)
resolvectl status  DNS info

## Drives & Boot Media
lsblk  List drives (RM=1 means removable)
sudo unmount /dev/sdX1  Unmount before removing
sudo ventoy -i /dev/sdX  make a Ventoy multi-ISO USB (Then just copy ISO files into it)

## Static IP (Ubuntu Server / Netplan)
config file: /etc/netplan/50-cloud-init.yaml
edit with sudo; YAML = spaces only, no tabs
sudo netplan try  Apply with 120s auto-revert safety
sudo netplan apply  Apply permanently
