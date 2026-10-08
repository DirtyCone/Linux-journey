# Linux Command Cheatsheet

## Navigation
pwd                  Print working directory (where am I)
cd <folder>          Go into a folder
cd ..                Go up one level
cd ~                 Go home
cd /                 Go to root (top of system)
ls  \ls              List contents (plain ls = \ls, no eza)
ls -l                Long format (permissions, size, date)
ls -a                Include hidden (dot) files
ls -la               Both
Tab                  Autocomplete names and commands

## Files & Folders
touch <file>         Make an empty file
mkdir <dir>          Make a directory (folder)
mkdir -p a/b/c       Make nested folders at once
cp <src> <dst>       Copy a file
cp -r <src> <dst>    Copy a folder + contents
mv <src> <dst>       Move OR rename
rm <file>            Delete a file (permanent, no undo)
rm -r <dir>          Delete a folder + contents
find ~ -name x       Find by name under home
find ~ -type d -name x   Directories only
find ~ -type f -name x   Files only

## Reading Files
cat <file>           Dump whole file (short files)
less <file>          Scrollable viewer (long; q to quit)
head <file>          First 10 lines
tail <file>          Last 10 lines
tail -f <file>       Follow live (Ctrl+C to stop)

## Text Flow & Filtering
cmd > file           Send output to file (OVERWRITES)
cmd >> file          Append output to file
cmd1 | cmd2          Pipe: cmd1 output becomes cmd2 input
grep <pattern>       Filter lines matching pattern (e.g. ps aux | grep sleep)

## Permissions & Ownership
chmod <mode> <file>  Change permissions
  numeric: r=4 w=2 x=1 ; three digits = owner/group/others
  755 = rwxr-xr-x (runnable) ; 644 = rw-r--r-- (plain file)
  700 = owner only ; 600 = private file
chmod +x <file>      Add execute (make runnable)
chown <user>:<group> <file>   Change owner/group (needs sudo)
classes = owner (u) / group (g) / others (o)
UID 0 = root (full access)

## Processes
ps aux               List all running processes
ps aux | grep x      Find a specific process
top                  Live process view by CPU (q to quit)
kill <PID>           Politely stop a process
kill -9 <PID>        Force kill (last resort)
<cmd> &              Run command in the background

## System Inspection
df -h                Disk space
free -h              Memory (RAM) usage
du -h                Folder/file size
whoami               Who am I logged in as
uname -a             System/kernel info
history              Recent commands run
which <cmd>          Full path to a program

## Editor (Neovim)
nvim <file>          Open/create file
i                    Insert mode (type text)
Esc                  Back to Normal mode
:w                   Save
:q                   Quit
:wq                  Save and quit
:q!                  Quit without saving
:set paste           Paste mode (avoids auto-indent mangling)
dd                   Delete (cut) a line
u                    Undo ;  Ctrl+r  Redo
G                    Bottom of file ;  gg  Top

## Scripting
#!/bin/bash          Shebang (first line; names interpreter)
NAME=value           Set a variable (no spaces around =)
$NAME                Use a variable
$(command)           Command substitution (run cmd, use its output)
chmod +x script.sh   Make runnable, then: ./script.sh

## Shell Customization (~/.bashrc)
source ~/.bashrc     Reload config after editing
alias name="command" Make a shortcut
mkcd() { mkdir -p "$1" && cd "$1"; }   Function: make + enter a folder
$1                   First argument passed to a function
# at line start      Comment (disabled line)

## Shell Environment (PATH)
export PATH="$PATH:$HOME/path/to/bin"  Add a folder to PATH (its commands run anywhere)
  - put in ~/.bashrc to make permanent, then: source ~/.bashrc
  - $PATH = current path, $HOME = home folder; we append, not replace

## My Custom Shortcuts (in ~/.bashrc)
cheat                Show this cheatsheet
mkcd <name>          Make a folder and cd into it
server               SSH into home server (ssh rhythmbyte@192.168.40.210)

## Packages
sudo pacman -S <pkg>     Install (Arch/Omarchy)
sudo pacman -R <pkg>     Remove
yay -S <pkg>             AUR install (Omarchy extras); <pkg>-bin = precompiled (faster)
pacman -Qi <pkg>         Info about installed pkg (check "Required By" before removing)
sudo pacman -Rns <pkg>   Remove pkg + configs + unused deps (check -Qi first)
sudo apt install <pkg>   Install (Ubuntu/Debian)
sudo apt update && sudo apt upgrade -y   Update Ubuntu

## Help
man <command>        Manual for any command
inside man: /word search, n next, q quit, g top, G bottom

## Git & GitHub
git init             Turn folder into a repo
git status           See what changed / staged
git add <file>       Stage a file (git add . = all)
git commit -m "msg"  Save a snapshot
git push             Upload commits to GitHub
git pull             Download commits from GitHub
git log              Commit history (q to quit)
git clone <url>      Download a repo
git remote -v        Show linked GitHub URL
git remote set-url origin <url>   Change linked URL
git checkout <name>  Switch to an existing branch
git checkout -b <name>   Create + switch to a new branch
git branch           List branches (* = current)
git branch -d <name> Delete a local branch
git push origin --delete <name>   Delete a remote branch
gh auth login        Log machine into GitHub
gh auth status       Check GitHub login
gh repo create <name> --private --source=. --push
.env = secrets, never commit, keep in .gitignore

## Git Workflow Rhythm (one task = one branch)
1. git checkout main
2. git pull                          (get latest)
3. git checkout -b descriptive-name  (fresh branch for this task)
4. make changes -> git add . -> git commit -m "msg" -> git push
5. open Pull Request on GitHub -> reviewed -> merged
6. delete branch (local + remote) when done
7. repeat from step 1 for next task
- never commit straight to main on a live/shared project
- branches are disposable: fresh one per task, like gloves

## SSH & Remote Servers
ssh user@ip          Connect to a remote machine
exit                 Disconnect (back to local)
hostname             Shows which machine you're on
first connect        asks to trust host -> type yes
private IP (192.168.x.x) = local network only
  (reachable only on same network, no internet exposure)

## SSH Keys
ssh-keygen -t ed25519 -C "label"   Generate a key pair (ed25519 = modern/secure)
  - private key (id_ed25519): NEVER share; stays on this machine; used automatically
  - public key (id_ed25519.pub): safe to share; give to servers to authorize you
  - one key pair works for unlimited servers (give each your public key)
cat ~/.ssh/id_ed25519.pub   Show public key (to send to a server admin)

## Networking (checks)
ip route | grep default   Show gateway + interface
ping -c 3 <host>     Test internet (3 pings, then stop)
resolvectl status    DNS info
ss -tlnp             Listening ports on this machine

## System Logs & Security
journalctl -f        Live system log (Ctrl+C to stop)
journalctl -f | grep UFW   Live firewall blocks only

## Drives & Boot Media
lsblk                List drives (RM=1 means removable)
sudo umount /dev/sdX1     Unmount before removing
sudo ventoy -i /dev/sdX   Make a Ventoy multi-ISO USB (then copy ISO files onto it)

## Static IP (Ubuntu Server / Netplan)
config file: /etc/netplan/50-cloud-init.yaml
edit with sudo; YAML = spaces only, no tabs
sudo netplan try     Apply with 120s auto-revert safety
sudo netplan apply   Apply permanently
