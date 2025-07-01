## Installing AVD

```
ansible-galaxy collection install arista.avd
pip3 install pyavd
pip3 install anta
pip3 install distlib
```
### Add SSH Key

On the Linux system, run the command `ssh-keygen`

```
[tony@localhost AVD]$ ssh-keygen 
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/tony/.ssh/id_ed25519): 
Enter passphrase for "/home/tony/.ssh/id_ed25519" (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/tony/.ssh/id_ed25519
Your public key has been saved in /home/tony/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:vykbR3OCKuLMld4RS7Xkyy5Ae6kffC3RmCKQ9gUDQLA tony@localhost.localdomain
The key's randomart image is:
+--[ED25519 256]--+
|=o..o            |
| . . o123        |
|E +   \. o       |
| . .. + *        |
|   .o.+.S = .    |
|    o=h  * +     |
|  . ++* * +      |
| + +.o.=.+ o     |
|  + ..o.123      |
+----[SHA256]-----+
```
Then cat the pub file: 
```
[tony@localhost AVD]$ cat ~/.ssh/id_ed25519.pub 
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5A233AIOhcjG4QuZ31AAsnZ4uu6CYQqaOCdYw0fgl1YbqgYof7 tony@localhost.localdomain
```
Paste the contents of the pub file into the group_vars/FABRIC.yml at the end, under ssh_key:

```yaml
local_users:
  - name: admin
    privilege: 15
    role: network-admin
    sha512_password: $6$bCfsjvLF/HKQtYdf$kTZV/b/sieDAzhC9V18lmtw9j8ULvDmBn3.lE/It4O67zBfm4xS4B11GxClPP8wI6j260318sctP/K/2/Duxk1 # This hashes out to "admin"
    ssh_key: ""
```
So it would look something like: 

```yaml
local_users:
  - name: admin
    privilege: 15
    role: network-admin
    sha512_password: $6$bCfsjvLF/HKQtYdf$kTZV/b/sieDAzhC9V18lmtw9j8ULvDmBn3.lE/It4O67zBfm4xS4B11GxClPP8wI6j260318sctP/K/2/Duxk1 # This hashes out to "admin"
    ssh_key: "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOhcjG4QuZ31AAsnZ4uu6CYQqaOCdYw0fgl1YbqgYof7 tony@localhost.localdomain"
```



