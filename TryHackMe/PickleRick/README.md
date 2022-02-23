# PickleRick Machine

## Progress

- [x] Challenge Completed

---

## Walkthrough

### Enumeration

- Ran nmap
- Ran gobuster
- Found 4 pic/gifs in "/assets"
- Tried to crack them using stegseek, no luck
- Checked source code, found username "R1ckRul3s"
- Found "/login.php" through gobuster
- Have username, no password
- Found "/robots.txt" with text "Wubbalubbadubdub", could be pasword

### Exploitation

- Tried in SSH no luck, in web, Voila!!!
- After logging in, it shows panel where we can execute command
- Tried `ls` to see list of files
- Found "Sup3rS3cretPickl3Ingred.txt" and "clue.txt"
- Tried to `cat` but found command disbaled 
- Tried looking at source code and found "Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0==" commented out
- Tried to decode it using base64 decoder, was another base64 string which decoded into one another and so on until the last one said "rabit hole", ANGRYYYYY
- Tried using alternatives of `cat` like `head` and `less`
- `less` worked, found contents of "Sup3rS3cretPickl3Ingred.txt"
- Found second ingredient in "/home/rick/second ingredients"
- Couldn't find 3rd so tried to run `sudo -l`, found out can ran anything with sudo
- Last possible place a flag could be was "/root"
- Found last ingredient in "/root/3rd.txt"

---

## Creds Found

| Username | Password | Type |
|--------|------|---------|
|R1ckRul3s | Wubbalubbadubdub | Web |