# Shell
#linux #shell

--- 
### Add Environment Variable to PATH

```
$ sudo nano /etc/paths
Password:
$ nano ~/.bash_profile
$ cat ~/.bash_profile 
export PATH=“/Users/arunsah/bin/kafka_2.13-2.4.0/bin:$PATH”
```


### Generating SSH Key

```
$ ssh-keygen -t rsa
¬* Enter filename of key [provide path relative to current folder else there is default path].
¬* Enter pass-phase.
¬* Confirm pass-phase.

// two file will be generated <filename> and <filename.pub>
```
