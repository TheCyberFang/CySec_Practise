# MrRobot Machine

## Progress

- [x] User Owned
- [x] Root Owned

---

## Walkthrough

### Enumeration

- Ran nmap
- Ran gobuster
- Found out site is running on wordpress
- Ran wpscan for username enumeration
- "/robots.txt" revealed 2 file "fsocity.dic" and "key-1-of-3.txt"
- Downloaded both files
- On wordpress login page tried different usernames, for "elliot" it said the pwd is wrong so the username is right!

### Exploitation

- Bruteforce using metaspoit, username "elliot", pwd_file "fsocity.dic" spit out the password "ER28-0652" 
- Found username password pair for web "elliot:ER28-0652"
- Log in to wordpress
- Elliot is Administrator so can edit any files
- Tried adding vulnerable code in header.php file, reverse shell to be clear
- Did not work, maybe try adding new page
- Added new page with reverse shell and started listner on local machine
- Visit the page and Voila! got the shell!
- `cd /home/robot` reveals 2nd key "key-2-of-3.txt" and password file with extension raw-md5
- Cracked password file and found out password "abcdefghijklmnopqrstuvwxyz"
- Found new pair of credentials "robot:abcdefghijklmnopqrstuvwxyz" for system

### Post-Exploitation

- `su robot` and enter password, now we are more privileged user: robot
- Tried doing PrivEsc using kernal, sudo nothing worked
- Enter "linpeas", ran it and found nmap is present
- `nmap --interactive` and after that `!sh`
- And boom ez pz root :)
- 3rd key in "/root" folder, "key-3-of-3.txt"

---

## Credentials Found

| Username | Password | Type |
|--------|-----------|---------------|
| elliot | ER28-0652 | Web |
| robot | abcdefghijklmnopqrstuvwxyz | System |