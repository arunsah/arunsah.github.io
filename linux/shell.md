# Shell
📅 [2020-05-01](https://arunsah.github.io/meta/changelog#2020-05-01) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)


### Deleting Files

https://askubuntu.com/questions/707924/how-to-delete-this-files-with-wildcards-in-ubuntu-terminal

```shell
rm -rf ./*.txt
```

--- 
### Add Environment Variable to PATH

```
$ sudo nano /etc/paths
Password:
$ nano ~/.bash_profile
$ cat ~/.bash_profile 
export GOPATH="/users/arunsah/go"
export PATH="/Users/arunsah/bin/kafka_2.13-2.4.0/bin:$PATH”
```


### Generating SSH Key

```
$ ssh-keygen -t rsa
¬* Enter filename of key [provide path relative to current folder else there is default path].
¬* Enter pass-phase.
¬* Confirm pass-phase.

// two file will be generated <filename> and <filename.pub>
```

### Install C, C++ Compiler and Development (build-essential) Tools in Ubuntu

`$ sudo apt-get update && apt-get install build-essential`

- Speeding up comilation
`sudo apt-get install ccache`

```C
#include<stdio.h>
int main()
{
   int a, b, c;
   printf("Enter two numbers to add, separated by a space: ");
   scanf("%d%d",&a,&b);
   c = a + b;
   printf("The sum of equals %d\n",c);
   return 0;
}
// gcc hello.c -o hello
// ./hello
```
```shell

$ gcc hello.c -o hello
mario@mario:~/dev/sysprog/linuxproginterface/introduction$ ./hello 
Enter two numbers to add, separated by a space: 1 3
The sum of equals 4
mario@mario:~/dev/sysprog/linuxproginterface/introduction$ ^C
```

### Installation Issue

```shell
mario@mario:~$ sudo apt-get install build-essential
[sudo] password for mario: 
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?

mario@mario:~$ ps aux | grep [a]pt
root       481  0.0  0.0   4624   596 ?        Ss   14:38   0:00 /bin/sh /usr/lib/apt/apt.systemd.daily install
root       556  0.0  0.0   4624  1408 ?        S    14:38   0:00 /bin/sh /usr/lib/apt/apt.systemd.daily lock_is_held install
mario@mario:~$ sudo kill 481
mario@mario:~$ sudo kill 556
mario@mario:~$ ps aux | grep [a]pt

mario@mario:~$ sudo rm /var/lib/dpkg/lock-frontend
mario@mario:~$ sudo apt-get install build-essential

mario@mario:~$ sudo apt upgrade
mario@mario:~$ sudo apt-get update
mario@mario:~$ sudo apt update

```

### Checksum (on Mac)

https://medium.com/@EvgeniIvanov/how-to-verify-checksum-on-mac-988f166b0c4f

```shell
#other algorithms: 1, 256, 512
shasum -a 512 <absulute_file_path>

#other algorithms: sha1, sha256, sha512
openssl sha512 <absulute_file_path>

md5 <absulute_file_path>

openssl md5 <absulute_file_path>
```



### Eclipse - Maven

https://stackoverflow.com/questions/18790106/eclipsemaven-src-main-java-not-visible-in-src-folder-in-package-explorer

https://stackoverflow.com/a/31674132

- Right click the Maven Project -> Build Path -> Configure Build Path
- In Order and Export tab, you can see the message like '2 build path entries are missing'
- Now select 'JRE System Library' and 'Maven Dependencies' checkbox
- Click OK

