# Over The Wire

Status: approved
Tags: Completed, Module 1: The Essentials, Week 1

## 🐱‍🏍Bandit

### bandit0

- The password was available into the readme file after ssh in to the given server.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

`boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

### bandit1

- ssh into bandit1 then there is a file named `-` and it cannot be opened normally using text editor or view it's content using cat
- to view this file I used `cat ./-`
- `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`

### bandit2

- password was stored in a file with spaces in it's name
- use `\` to escape the space
- `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`

### bandit3

- there was a folder `inhere1`
- used `ls -a` to list all the contents including the hidden ones
- `.hidden` file had the password
- `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`

### bandit4

- there were 9 files the file name started with `-` so used `./-filename`
- most files had non readable text but `file7`
- listed the contents of file using `cat ./-file07`

`proper way`

![assets/Untitled.png](assets/Untitled.png)

- `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`

### bandit5

- there were around 20 folders and each had many files
- looking at each file was not possible[time consuming]
- `3` properties of the file was given
- `find . -type f -size 1033c` using only 2 properties gave us the exact file
- `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`

### bandit6

- `find / -user bandit7 -group bandit6 -size 33`
- listed all the files with the requirement
- all files had `Permission denied` but one
- so used cat to get my password from the file `/var/lib/dpkg/info/bandit7.password`
- `HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs`

### bandit7

- there was a data.txt file and the password was stored next to word millionth
- so we could either use vim to look for word millionth or simply use `cat data.txt | grep millionth`
- `cvX2JJa4CFALtqS87jk27qwqGhBM9plV`

### bandit8

- again there was data.txt file but with only one column
- the password was in the line which repeated only once
- `uniq` command removes duplicate lines
- `uniq -u` only lists unique line but it needs file in sorted format

![assets/Untitled%201.png](assets/Untitled%201.png)

- `UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`

### bandit9

- data.txt contained non human readable strings mostly
- used vim and searched for `===`
- to search in vim `/` `enter` `n` `N` n for next match and N for previous match
- `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`

### bandit10

- base64 encoded data was stored in data.txt file
- use `base64 -d data.txt` to decode the value

![assets/Untitled%202.png](assets/Untitled%202.png)

- `IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`

### bandit11

- The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
- used `cyberchef` to decode the password

![assets/Untitled%203.png](assets/Untitled%203.png)

- `5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`

### bandit12

- Longest one till now
- cyberchef won't easily get you to solution
- you will need `xxd` `bzip2` `gzip` `file` extensively
- first make a copy of data.txt to `/tmp/myname1/`

![assets/Untitled%204.png](assets/Untitled%204.png)

- then use `xxd` to reverse hexdump

![assets/Untitled%205.png](assets/Untitled%205.png)

- use `file ./*` to get what type of compression is used and rename the file according and perform decompression

![assets/Untitled%206.png](assets/Untitled%206.png)

![assets/Untitled%207.png](assets/Untitled%207.png)

![assets/Untitled%208.png](assets/Untitled%208.png)

- `8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`

### bandit13

- there is a private sshkey in user's folder
- which can be used to login to next level rather than a password

```bash
ssh -i sshkey.private bandit14@localhost
```

### bandit14

- `nc` (netcat) is a command line utility that reads and writes data across network connection using TCP or UDP protocols.

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 | nc localhost 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

- `BfMYroe26WYalil77FoDi9qh59eK5xNr`

### bandit15

```bash
$ openssl s_client -connect localhost:30001
...
...
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

- `cluFn7wTiGryunymYOu4RcffSxQluehd`

### bandit16

```bash
bandit16@bandit:~$ nmap -sV -p 31000-32000 localhost

Starting Nmap 7.40 ( https://nmap.org ) at 2021-06-02 18:40 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00032s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

- -sV gives info about the running service on the port
- -p is used to specify port no. or range

```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790
CONNECTED(00000003)
...
...
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

```bash
cd /tmp/
touch key16.txt
# open with vim and paste the RSA key
ssh -i key16.txt bandit17@localhost
# bad permission
# give read only permission
bandit16@bandit:/tmp$ chmod 400 key16.txt
bandit16@bandit:/tmp$ ssh -i key16.txt bandit17@localhost
```

- `xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn`

### bandit17

```bash
bandit17@bandit:~$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
```

- `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd`

### bandit18

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t 'cat readme'
```

- `IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`

### bandit19

```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

- `setuid` makes bash think that we are bandit20 rather than bandit19 and hence perform actions as bandit20 i.e. view the password of bandit20
- `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

### bandit20

![assets/Untitled%209.png](assets/Untitled%209.png)

- at first run nmap scan on [localhost](http://localhost) to check which ports are used
- then start listening on a port other than those being used
- run the suconnect script and pass the password of current level as argument and it sends the password of next level
- `gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`

### bandit21

```bash
bandit21@bandit:/etc/cron.d$ ls -lah
total 36K
drwxr-xr-x  2 root root 4.0K Jul 11  2020 .
drwxr-xr-x 87 root root 4.0K May 14  2020 ..
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit15_root
-rw-r--r--  1 root root   62 Jul 11  2020 cronjob_bandit17_root
-rw-r--r--  1 root root  120 May  7  2020 cronjob_bandit22
-rw-r--r--  1 root root  122 May  7  2020 cronjob_bandit23
-rw-r--r--  1 root root  120 May 14  2020 cronjob_bandit24
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit25_root
-rw-r--r--  1 root root  102 Oct  7  2017 .placeholder
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit20@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

- list the contents of cronjob_bandit22
- we find that the password is being written in a file inside tmp
- we get the password of the next level by viewing the contents of the file in tmp
- `Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI`

### bandit22

```bash
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

- whoami gives the current username and it is stored in myname variable
- mytarget variable is set to the md5sum of `I am user bandit22` and cut is used to remove spaces and get only the md5sum

```bash
# what I did wrong
# bandit22@bandit:/usr/bin$ ./cronjob_bandit23.sh
# Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
# bandit22@bandit:/usr/bin$ cat /tmp/8169b67bd894ddbb4412f91573b38db3
# Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
bandit22@bandit:/usr/bin$ echo 'I am user bandit23' | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/usr/bin$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

- `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

### bandit23

```bash
bandit23@bandit:~$ cd /etc/cron.d
bandit23@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

```bash
bandit23@bandit:/etc/cron.d$ cd /tmp/
bandit23@bandit:/tmp$ mkdir pass24
bandit23@bandit:/tmp$ cd pass24
bandit23@bandit:/tmp/pass24$ touch getpass.sh
bandit23@bandit:/tmp/pass24$ touch pass
bandit23@bandit:/tmp/pass24$ vim getpass.sh
```

```bash
#!/bin/bash                                                                   

cat /etc/bandit_pass/bandit24 > /tmp/pass24/pass
```

```bash
bandit23@bandit:/tmp/pass24$ chmod a+rwx pass
bandit23@bandit:/tmp/pass24$ ls -lah
total 1.1M
drwxr-sr-x    2 bandit23 root 4.0K Jun  5 18:27 .
drwxrws-wt 5118 root     root 1.1M Jun  5 18:44 ..
-rw-r--r--    1 bandit23 root   62 Jun  5 18:24 getpass.sh
-rwxrwxrwx    1 bandit23 root    0 Jun  5 18:23 pass
bandit23@bandit:/tmp/pass24$ chmod a+rwx getpass.sh
bandit23@bandit:/tmp/pass24$ ls -lah
total 1.1M
drwxr-sr-x    2 bandit23 root 4.0K Jun  5 18:27 .
drwxrws-wt 5118 root     root 1.1M Jun  5 18:45 ..
-rwxrwxrwx    1 bandit23 root   62 Jun  5 18:24 getpass.sh
-rwxrwxrwx    1 bandit23 root    0 Jun  5 18:23 pass
```

```bash
bandit23@bandit:/tmp/pass24$ cp getpass.sh /var/spool/bandit24/
```

- The password is obtained in the specified file after 1min
- `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`

### bandit24

```bash
bandit24@bandit:/tmp/pswdcomb$ touch pc
bandit24@bandit:/tmp/pswdcomb$ for i in {0000..9999}; do echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i >> /tmp/pswdcomb/pc; done;
```

- pc file stores the password `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ` and numbers from 0 to 9999 separated by space.

```bash
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0000
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0001
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0002
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0003
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0004
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0005
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0006
```

```bash
bandit24@bandit:/tmp/pswdcomb$ nc localhost 30002 < /tmp/pswdcomb/pc
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
...
...
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.
```

- `uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG`

### bandit25, bandit 26

```bash
bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$ ssh bandit26@localhost -i bandit26.sshkey
```

```bash
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

```bash
# tricky one
# you have to minimze the terminal so that you see more option
```

![assets/Screenshot_2021-06-06_00_40_10_(2).png](assets/Screenshot_2021-06-06_00_40_10_(2).png)

- then press v in vim

```bash
:set shell=/bin/bash
:shell
```

```bash
bandit26@bandit:~$ cat /etc/bandit_pass/bandit26
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

bandit26@bandit:~$ ls -lah
-rwsr-x---  1 bandit27 bandit26 7.2K May  7  2020 bandit27-do

bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```

- `3ba3118a22e93127a4ed485be72ef5ea`

### bandit27

```bash
bandit27@bandit:~$ cd /tmp/
bandit27@bandit:/tmp$ mkdir gitwrk
bandit27@bandit:/tmp$ cd gitwrk
bandit27@bandit:/tmp/gitwrk$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit27/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit27-git@localhost's password:
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.

# readme file has the password for next level
bandit27@bandit:/tmp/gitwrk$ ls -lah
total 1.1M
drwxr-sr-x    3 bandit27 root 4.0K Jun  6 06:49 .
drwxrws-wt 5045 root     root 1.1M Jun  6 06:51 ..
drwxr-sr-x    3 bandit27 root 4.0K Jun  6 06:49 repo
bandit27@bandit:/tmp/gitwrk$ cd repo/
bandit27@bandit:/tmp/gitwrk/repo$ ls
README
bandit27@bandit:/tmp/gitwrk/repo$ cat README
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2
```

- `0ef186ac70e04ea33b4c1853d2526fa2`

### bandit28

```bash
bandit28@bandit:~$ cd /tmp/
bandit28@bandit:/tmp$ mkdir git28
bandit28@bandit:/tmp$ cd git28
bandit28@bandit:/tmp/git28$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit28/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit28-git@localhost's password:
remote: Counting objects: 9, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.

bandit28@bandit:/tmp/git28$ ls
repo
bandit28@bandit:/tmp/git28$ cd repo
bandit28@bandit:/tmp/git28/repo$ ls
README.md
bandit28@bandit:/tmp/git28/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

```bash
bandit28@bandit:/tmp/git28/repo$ git checkout c086d11a00c0648d095d04c089786
Previous HEAD position was edd935d... fix info leak
HEAD is now at c086d11... add missing data
bandit28@bandit:/tmp/git28/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: bbc96594b4e001778eee9975372716b2
```

`bbc96594b4e001778eee9975372716b2`

### bandit29

```bash
bandit29@bandit:/tmp/git29$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password:
remote: Counting objects: 16, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
bandit29@bandit:/tmp/git29$ cd repo/
bandit29@bandit:/tmp/git29/repo$ ls
README.md
bandit29@bandit:/tmp/git29/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

```bash
bandit29@bandit:/tmp/git29/repo$ git log
commit 208f463b5b3992906eabf23c562eda3277fea912
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:51 2020 +0200

    fix username

commit 18a6fd6d5ef7f0874bbdda2fa0d77b3b81fd63f7
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:51 2020 +0200

    initial commit of README.md
bandit29@bandit:/tmp/git29/repo$ git branch --v
* master 208f463 fix username
bandit29@bandit:/tmp/git29/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

```bash
bandit29@bandit:/tmp/git29/repo$ ls
code  README.md
bandit29@bandit:/tmp/git29/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```

- `5b90576bedb2cc04c86a9e924ce42faf`

### bandit30

```bash
bandit30@bandit:/tmp/git30/repo$ cat README.md
just an epmty file... muahaha
bandit30@bandit:/tmp/git30/repo$ ls -a
.  ..  .git  README.md
bandit30@bandit:/tmp/git30/repo$ git log
commit 3aefa229469b7ba1cc08203e5d8fa299354c496b
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:54 2020 +0200

    initial commit of README.md
bandit30@bandit:/tmp/git30/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
bandit30@bandit:/tmp/git30/repo$ git checkout master
Already on 'master'
Your branch is up-to-date with 'origin/master'.
bandit30@bandit:/tmp/git30/repo$
bandit30@bandit:/tmp/git30/repo$ git tag
secret
```

```bash
bandit30@bandit:/tmp/git30/repo$ git cat-file -p secret
47e603bb428404d265f59c42920d81e5
```

- `47e603bb428404d265f59c42920d81e5`

### bandit31

```bash
bandit31@bandit:/tmp/git31/repo$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master

bandit31@bandit:/tmp/git31/repo$ echo 'May I come in?' > key.txt

```

```bash
bandit31@bandit:/tmp/git31/repo$ git add key.txt
The following paths are ignored by one of your .gitignore files:
key.txt
Use -f if you really want to add them.
```

```bash
bandit31@bandit:/tmp/git31/repo$ rm .gitignore
bandit31@bandit:/tmp/git31/repo$ git add key.txt
bandit31@bandit:/tmp/git31/repo$ git commit -m "add key.txt"
[master ffda7d7] add key.txt
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
bandit31@bandit:/tmp/git31/repo$ git push origin master
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 321 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'
```

- `56a9bf19c63d650ce78e6ec0354ee45e`

### bandit32

```bash
WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: not found
```

```bash
>> $0
$ ls
uppershell
```

- Thus, $0 returns a subshell within the uppercase shell where we can type in the normal commands without them being converted to uppercase

```bash
$ whoami
bandit33
$ cat /etc/bandit_pass/bandit33
c9c3199ddf4121b10cf581a98d51caee
```

- `c9c3199ddf4121b10cf581a98d51caee`

### bandit33

```bash
bandit33@bandit:~$ ls
README.txt
bandit33@bandit:~$ cat README.txt
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
```