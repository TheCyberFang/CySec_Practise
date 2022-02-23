# Blue Machine

## Progress

- [x] User Owned
- [x] Root Owned

---

## Walkthrough

### Enumeration

- Ran basic nmap scan `nmap <IP>`
- Found 9 ports open
- Netbios/Samba running on 139,445
- It's called blue and samba is running so it might be vulnerable to "EternalBlue"
- Checked for "EternalBlue" (ms17-010), Found vulnerable

### Exploitation

- Metasploit has module for EternalBlue so fired up `msfconsole`
- Searched "EternalBlue", found exploit `exploit/windows/smb/ms17_010_eternalblue`
- Ran `check` to confirm the target is vulnerable and it was
- Set required options and `run`
- Got meterpreter shell back
- Ran `shell` to drop into system shell
- Typing `whoami` revealed "nt authority\system", the highest priviledge user
- Typing `exit` will drop back to meterpreter shell
- Ran `find -f flag*` to find all flags in system
- Found 1st flag, do `cat c:/flag1.txt` to see flag
- Found 2nd flag, do `cat c:/Windows/System32/config/flag2.txt` to see flag
- Found 3rd flag, do `cat c:/Users/Jon/Documents/flag3.txt` to see flag 

### Extras

- Ran `hashdump` to see password hashes
- Copied all hashes to a file
- Cracked using John the Ripper
- Found pair "Jon:alqfna22"