# Overpass Machine

## Progress

- [x] User Owned
- [ ] Root Owned

---

## Walkthrough

### Enumeration

- Ran nmap, found 22,80 open ( nmap/nmap_init.nmap & nmap/nmap_all_ports.nmap )
- Read source code - Found out used Ceaser cipher in passwords
- Gobuster found /admin
- Tried using common pairs, didn't work
- Source code - using API for authentications
- Source code - "Incorrect Credentials" if wrong creds, token set if right creds

### Exploitation

- Ran burpsuite and intercepted the request
- Enabled intercept response too
- In response, removed "Incorrect Credentials" and set Token to "admin"
- Response shows SSH key posted by Paradoc for user James ( files/ssh_private.pem )
- Used ssh2john to generate hash file ( files/ssh_private.hash )
- Cracked password "james13" using john the ripper, wordlist rockyou.txt
- New credential pair found for SSH "james:james13"
- Tried creds in web, didn't work
- Login using SSH using `ssh -i <private key> james@<IP>`
- `ls -la` reveals "user.txt" and ".overpass"
- Found user flag in "user.txt"
- `cat .overpass` reveals bunch of nonsense text
- Went to [dcode.fr](https://www.dcode.fr/) to find encryption algorithm, it was ROT47
- Used same website [dcode.fr](https://www.dcode.fr/) to decrypt text from ".overpass" file
- Decrypted text reads "saydrawnlyingpicture"
- `sudo -l` asked for password, "james13" didn't worked, "saydrawnlyingpicture" worked
- New credential pair found for user on system "james:saydrawnlyingpicture"
- `sudo -l` reveals user "james" have no program to run as super user
- Working on getting root

---

## Credentials

| Username | Password | Type |
|----|----|----|
| james | james13 | SSH |
| james | saydrawnlyingpicture | System |