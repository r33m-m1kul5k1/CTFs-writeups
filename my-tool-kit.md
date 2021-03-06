# Basic tools
- `du -h <file name>` - human readable file and directories size
- `base64` - decode encrypted data with base64
- `tar -xf <file name>` - extract tar files
- `diff`- compares two files line by line
- `git log --all` show all commits!
- `truncate -s -1 filename` remove last byte of a file 

# Linux
- `setuid` - a file flag, that tells that the current user can execute the specific file as the file's creator user.
- `wc -c` - number of bytes a file have
- truncate -s -1 /tmp/x -> removes a file end
the flage symbol is `s`.
- `cron` - cron is a daemon to execute scheduled commands. The cron config is inside `/etc/cron.d`.
- `tmux / screen` - terminal managers. tmux basic commands:
    ```
    ctrl + b + % -> vertical split
    ctrl + b + " horizontal
    ctrl + b + arrows -> move between splits
    ctrl + b + arrows holding -> resize splits
    exit - exit
    ```
- `echo -e` with \x can represent hex in the bash shell.
- (command; command;) called command grouping. you can pipe it into another program to run these commands.
- `more` - cat file.txt | less
- `/etc/passwd` - file with info about users.
- `dash` - shell for debian.

# Reversing
- `strings` - get all the human readable strings inside a file
- `file` - get the file format
    ```bash
    # debugging info
    file -d <filename>
    # report info about compressed file
    file -Z
    ```

- `xxd` - creates hexdumps or do the reverse, with the `-r` flag
- `strace` - trace syscalls
- `ltrace` - trace libraries
- `objdump` - reverse an executable file
  ```
  - objdump -t | grep func name -> find function address
  ```
- `gdb`
  ```
  gcc -g -> for symbols
  tui disable (close layout window)
  disas main
  x/<num of bytes><format> $<register>
  (formats -> i for instruction and $eip)
  Example:
   - x/100s $ebp -> shows the first 100 bytes as a string from the stack frame
  b *assembly addr
  info registers/frame/proc mappings
  o
  gdb hooks -> a functions that will run every time we do something depending on its name:
  define hook-stop -> for break point
  i r
  end
  
  set exec-wrapper env -u LINES -u COLUMNS
  the address space in gdb:
  0x0  
  0xff
  ```

# Netowrking
- `ssh` 
    ```bash
    ssh username@host -p <port>
    # enter with ceritficate 
    ssh -i ssh_private.key username@host -p <port>
    # You can add a command to automatically execute when the ssh connection is started
    ssh username@host -p <port> [command]
    # enter a shell inside current machine
    ssh username@localhost 
    # copying a file with ssh
    scp -P[port] user@host:[file-path] [copy directory]
    scp -P2222 col@pwnable.kr:col.c .
    ```
    
- `nmap`
    ```bash
    # show who is connect to the current network 
    nmap -sP <netwok ip>
    # finds server on specify porst using TCP three way handshake 
    nmap -sT -p 80,443 <netwok ip> 
    # for scanning the network more secured (only syn connection)
    # if you don't specify ports then namp will take the most 1000 common ports and scan them
    sudo nmap -sS -p 80,443 <netwok ip> 
    # Get the type of OS your target is running
    sudo nmap -O <target ip>
    # to get a lot of stuff on your target use -A flag
    # obescation (creating a decoy)
    sudo nmap -sS -D <decoy ip> <target ip>

    # nmap scrips -> scripts that other people wrote
    nmap --script vuln <ip to scan for vunrablilites> 
    ```
- `nc` - read and write data throw TCP and UDP connection
    ```bash
    # run a server with netcat
    nc -l host port 
    nc -lnvp host port
    # connect through a socket
    nc host port
    ```
- `openssl s_client` - ssl and stl client
    ```bash
    openssl s_client -connect host:port
    ```

