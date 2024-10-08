# pimpmykali.sh

![pimpmykali](https://github.com/Dewalt-arch/pimpmykali/assets/81341961/dd4ec6b0-dd27-4ff7-a60b-e9822255ff5f)

# Fixes for new imported Kali Linux virtual machines
  - Author assumes zero liability for any data loss or misuse of pimpmykali
  - Can be used on a bare metal machines, but thats on you
  - Menu breakdown added below revision history

# Github index updated added +x permission:
  - Script is now be executable upon clone (perms: 755 rwxr-xr-x added to github)
  - There is no need to chmod +x pimpmykali.sh upon git clone

# Installation:
```bash
# Remove existing pimpmykali folder
rm -rf pimpmykali/

# Clone pimpmykali repository & enter the folder
git clone https://github.com/Dewalt-arch/pimpmykali
cd pimpmykali

# Execute the script - For a new Kali VM, run menu option 'N'
# (The script must be run with root privileges)
sudo ./pimpmykali.sh
```
# Special Thanks to Pimpmykali-Mirrors Testers!!
  - Crazy_Man - https://github.com/The-Crazy-Man
  - Andro

# Code Contributors
  - Yaseen - https://github.com/AhamedYaseen03
  - Crazy_Man - https://github.com/The-Crazy-Man
  - blindpentester https://github.com/blindpentester
  - pswalia2u https://github.com/pswalia2u
  - Alek https://github.com/wodensec
  - Gr1mmie https://github.com/Gr1mmie
  - Aksheet https://github.com/Aksheet10
  - 0xC0FFEE VirtualBox Home Lab Build (updated link!)
    https://benheater.com/building-a-security-lab-in-virtualbox/
  - TheMadHuman https://github.com/TMH-Sec
  - Aashiksamuel https://github.com/aashiksamuel  (sublime install fix)
  - m4ul3r 
  - lbalmaceda https://github.com/lbalmaceda

# Writeups / Honorable Mentions
  - ip3c4c_n00b https://ip3c4c.com/2202_homelab_vmware/

# Revision 1.8.1b - Updated Ghidra Download function
  - corrected download

# Revision 1.8.1a - Added Andrew B's IoT and Hardware Hacking Course Setup 
  - Menu option Y or y
    - stand alone function
    - installs dependencies sigrok xxd zlib1g-dev liblzma-dev liblzo2-dev
    - clone sasquatch to /opt/sasquatch
    - patches sasquatch with M1-Kali.patch.txt
    - builds patched sasquatch
    - installs to /usr/local/bin/sasquatch
    - calls fix_ghidra function to install ghidra from github
    - installs ghidra dark theme to /opt/ghidra-dark-theme
  - updated fix_ghidra function to always pull latest release

# Revision 1.8.1 - Ghidra
  - Menu option G - Install Ghidra
    - Included in menu options 0, N and 1
    - removes ghidra installed from apt repository
    - downloads and installs ghidra from github
    - ghidra dark-theme added to /opt/ghidra-dark-theme

# Revision 1.8.0 - Added Alex T's C# 101 for Hackers Course Setup
  - Menu Option Z
    - installs vscode
    - installs vscode course extensions
      - C# Dev Kit (microsoft)
      - C# Extensions (JosKreativ)
      - VSCode Solutions Explorer (Fernando Escolar)
      - Jupyter (microsoft)
      - Polyglot Notebooks (microsoft)
      - Material Icon Theme (Philipp Kief) 
    - installs dotnet, aspnetcore, dotnet-runtime
    - adds DOTNET_ROOT and PATH= statements to $HOME/.nameofshellrc
    - status screen at end of install with version information

# Revision 1.7.9a6 - docker-compose / docker.io
  - Enabled menu option 7 for Fix DockerCompose
  - fix_dockercompose is included in options 0 (fix_all), N (new setup) or 1 (fix_missing)
  - New function added fix_dockercompose lines 253 to 330
    - check if docker-compose is installed if not install latest from github
    - if docker-compose is installed will version check system vs github and install newer version
      - case statement exit code handling
  - Consolidated docker-compose and docker.io installations in updated functions 
    - hacking_api_prereq
    - map_prereq
    - pbb_lab_setup
    - peh_weblab_setup
      - now uses fix_dockercompose function to install docker-compose and docker.io
  - revision notes 1.7.9 to 1.7.9a3 moved to changelog.txt
  - Readme.md updated for Menu option 7

# Revision 1.7.9a5 - curl --w 
  - Thanks Alek, updated curl from --w to -w 
    - functions small_speedtest, large_speedetest

# Revision 1.7.9a4 - updated fix_linwinpeas function
  - Thanks lbalmaceda! for the updated url and code submission
  - corrected url for Lin/WinPeas
  - updated function to always pull latest release  

# Menu Breakdown of Pimpmykali 

- Menu option N  (New Users/New VM's Should start here!)
  - executes menu option 0 fix all ( options 1 thru 8 )
  - executes menu opiion 9 (pimpmyupgrade)


- Menu option = Pimpmykali-Mirrors (rev 1.3.2)
  - obtain kali mirror list and process
    - round-trip-time ping test to all mirrors, select top 10 with shortest rtt
    - small download >1MB from the top 10 mirrors, select top 5 fastest transfers
    - large download 10MB test the final 5 mirrors, select fastest transfer
    - generate new /etc/apt/sources.list with the new selected mirror
    - prompt Y or N to write new changes to /etc/apt/sources.list
      - Y writes changes /etc/apt/sources.list
      - create backup of original sources.list in /etc/apt/sources.list_date_time
      - write new deb and deb-src lines with new mirror to /etc/apt/sources.list
      - N exits and makes no change to /etc/apt/sources.list


- Menu Option ! - Nuke Impacket (yes its literally the ! character)
  - removes any prior installation of impacket (gracefully and forcefully)
  - installs impacket-0.9.19


- Menu Option @ - Install Nessus (amd64 or arm64)
  - downloads and installs the current version of Nessus 
  - starts nessusd service 


- Menu Option $ - Uninstall Nessus (amd64 or arm64) 
  - stops all nessusd service
  - uninstalls nessus 


- Menu Option 1 - Fix missing
  - fix_sources
    - uncomment #deb-src from /etc/apt/sources.list
  - python-pip installation via curl
  - python3-pip installed
  - seclists installed
  - gedit installed (feature request)
  - flameshot installed (feature request)
  - locate installed (feature request)
  - fix_rockyou function
    - gunzip /usr/share/wordlists/rockyou.gz to /usr/share/wordlists/rockyou.txt
  - fix_golang function
    - installs golang
    - adds golang GOPATH to .bashrc and .zshrc
  - installs htop
  - installs python requests
  - installs python xlrd==1.2.0
  - disables xfce power management
  - blacklists pcspkr kernel module /etc/modprobe.d/nobeep.conf
  - intalls python pyftpdlib


- Menu Option 2 - Fix smb.conf
  - adds below [global] in /etc/samba/smb.conf
    - client min protocol = CORE  below [global]
    - client max protocol = SMB3  below [global]


- Menu Option 3 - Fix Golang 
  - Installs golang
    - checks for GOPATH in .bashrc and .zshrc
    - if GOPATH is found, adds nothing
    - if not found, adds GOPATH statements to both .zshrc and .bashrc


- Menu Option 4 - Fix Grub
  - adds mitigations=off to GRUB_CMDLINE_LINUX_DEFAULT


- Menu Option 5
  - installs Impacket-0.9.19


- Menu Option 6 - Enable root login
  - installs kali-root-login
    - prompts for root password
    - copy /home/kali/* to /root prompt (1.1.2)
    - prompt are you sure? to copy /home/kali to /root prompt (1.1.3)


- Menu Option 7
  - fix_dockercompose
    - installs docker.io from kali repo
    - check if docker compose is installed or not
    - if not installed, install latest from github
    - if installed, check local version vs github version
      - install newer version if found
    - Menu option 7 is included in fix_all and fix_missing functions


- Menu Option 8 - Fix Nmap
  - wget nmap script fixes
    - clamav-exec.nse
    - http-shellshock.nse (Thank you Alek!)


- Menu Option 9 - Pimpmyupgrade
  - additional notes will be added
  - fix : Hypervisor detection (vmware, virtualbox, qemu/libvirt)
    - add additional details here
  - fix : virtualbox shared folder fix applied     


- Menu Option 0 - Fix all (1-8)
  - Executes ONLY Menu options 1 thru 8


- Menu Option B  ( Changed 11.02.2023 )  
  - Installs labs for TCM Practical Bugbounty course 


- Menu Option C
  - Install Google-Chrome


- Menu Option D
  - Apply gedit unable to open display as root fix


- Menu Option E 
  - Install TCM PEH Course WebApp Labs, docker


- Menu Option F
  - Fixes XFCE Broken Icons "TerminalEmulator" Not Found
  - Fixes XFCE Open Catfish instead of Thunar when double clicking Home or FileSystem Icon
  - this fix is a temporary fix and will be removed once xfce has been corrected


- Menu Option G
  - Install Ghidra from Github


- Menu Option K
  - Reconfigure Keyboard, Language and Layout + Variant


- Menu Option M
  - Kali linux setup for Mayors Movement Pivoting and Persistance Course
    - installs covenant  


- Menu Option O - Practical API Hacking Course
  - Practical API Hacking course setup 
  - amd64 and arm64 aware
  - root user and normal user aware
  - installs docker.io docker-compose
   - docker service is enabled 
  - installs postman to /opt/Postman/Postman 
   - symlink is created for /opt/Postman/Postman at /usr/bin/postman
  - cleanup.sh script created 
  - installs crAPI to $HOME/labs


- Disable Power Management function moved to Menu options 0, N or 1
  - Based upon detection disable power management for that environment
    - Detect desktop environment
      - XFCE
      - Gnome


- Menu Option S - Fix Spike
    - Fixes undefined symbol error thrown when using generic_send_tcp
    - this fix is temporary and will be removed once a corrected version is available


- Menu Option T
  - Reconfigure Timezone


- Menu Option U
  - Install Netexec (nxc)


- Menu Option V
  - Install MS VSCode


- Menu Option W
  - Install GoWitness precompiled binary


- Menu Option Y
  - Andrew B's IoT and Hardware Hacking Course Setup 
    - installs dependencies sigrok xxd zlib1g-dev liblzma-dev liblzo2-dev
    - clone sasquatch to /opt/sasquatch
    - patches sasquatch with M1-Kali.patch.txt
    - builds patched sasquatch
    - installs to /usr/local/bin/sasquatch
    - calls fix_ghidra function to install ghidra from github
    - installs ghidra dark theme to /opt/ghidra-dark-theme


- Menu Option Z
  - Install course requirements for Alex T's C# 101 for Hackers
    - installs vscode
    - installs vscode course extensions
    - installs dotnet, aspnetcore, dotnet-runtime
    - adds DOTNET_ROOT path statments to $HOME/.nameofshellrc 


# TODO   
  - clean up todo list :)