---
title: "picoCTF 2022 - Forensic"
excerpt: "Writeup for the picoCTF 2022 - Forensic category"
last_modified_at: 2022-04-04
stickies: true
stickies_path: "/assets/stickies/picoctf.png"
toc: true
toc_label: "Challenges"
toc_sticky: true
categories:
  - Writeups
tags:
  - CTF
---

## Forensic
### Enhance!
`100 points` `5214 solves`

> `svg`<br>
> Download this image file and find the flag.<br>
> - [Download image file](https://artifacts.picoctf.net/c/138/drawing.flag.svg)

Opened the svg image with browser, used ctrl-A to select all and ctrl-F to search, the flag was selected and revealed in the search box. The whitespace in the flag was removed using [CyberChef](https://gchq.github.io/CyberChef/#recipe=Remove_whitespace(true,true,true,true,true,false)&input=cCBpIGMgbyBDIFQgRiB7IDMgbiBoIDQgbiBjIDMgZCBfIGQgMCBhIDcgNSA3IGIgZiB9).

![picoctf-2022-drawing.png]({{ site.url }}{{ site.baseurl }}/assets/posts/picoctf-2022-drawing.png)

Flag: `picoCTF{3nh4nc3d_d0a757bf}`

<br>

### Lookey here
`100 points` `5362 solves`

> `grep`<br>
> Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it.<br>
> Download the data [here](https://artifacts.picoctf.net/c/296/anthem.flag.txt).

`grep` the known flag pattern `picoCTF{` reveals the flag within the txt file.

```bash
└─$ cat anthem.flag.txt | grep picoCTF{
      we think that the men of picoCTF{gr3p_15_@w3s0m3_2116b979}
```

Flag: `picoCTF{gr3p_15_@w3s0m3_2116b979}`

<br>

### Packets Primer
`100 points` `4268 solves`

> `pcap`<br>
> Download the packet capture file and use packet analysis software to find the flag.<br>
> - [Download packet capture](https://artifacts.picoctf.net/c/201/network-dump.flag.pcap)

Opened the pcap file with WireShark and found the flag in one of the TCP packet data section.

Flag: `picoCTF{p4ck37_5h4rk_01b0a0d6}`

<br>

### Redaction gone wrong
`100 points` `4546 solves`

> Now you DON’T see me.<br>
> This [report](https://artifacts.picoctf.net/c/264/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?

The pdf has phrases highlighted with black colour, making it invisible by eye. Selected all with ctrl-A and copied and pasted it to a text document to reveal all text, which revealed the flag.

![picoctf-2022-redaction.png]({{ site.url }}{{ site.baseurl }}/assets/posts/picoctf-2022-redaction.png)

```text
Financial Report for ABC Labs, Kigali, Rwanda for the year 2021.
Breakdown - Just painted over in MS word.
Cost Benefit Analysis
Credit Debit
This is not the flag, keep looking
Expenses from the
picoCTF{C4n_Y0u_S33_m3_fully}
Redacted document.
```

Flag: `picoCTF{C4n_Y0u_S33_m3_fully}`

<br>

### Sleuthkit Intro
`100 points` `3116 solves`

> `sleuthkit`<br>
> Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.<br>
> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.<br>
> - [Download disk image](https://artifacts.picoctf.net/c/114/disk.img.gz)<br>
> - Access checker program: `nc saturn.picoctf.net 52279`

Unzipped the file and used `mmls` to get the Linux partition size as `202752`. Provided it to the checker program and the flag is returned.

```bash
└─$ gzip -d disk.img.gz

└─$ mmls disk.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)

└─$ nc saturn.picoctf.net 52279
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
picoCTF{mm15_f7w!}
```

Flag: `picoCTF{mm15_f7w!}`

<br>

### Sleuthkit Apprentice
`200 points` `1922 solves`

> `disk`<br>
> Download this disk image and find the flag.<br>
> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.<br>
> - [Download compressed disk image](https://artifacts.picoctf.net/c/332/disk.flag.img.gz)

Unzipped the file and used `fdisk` to check the partitions. With the first partition as boot and the second as swap, the third Linux partition should be the one in interest.

```bash
└─$ gzip -d disk.flag.img.gz

└─$ fdisk -lu disk.flag.img
Disk disk.flag.img: 300 MiB, 314572800 bytes, 614400 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x7389e82d

Device         Boot  Start    End Sectors  Size Id Type
disk.flag.img1 *      2048 206847  204800  100M 83 Linux
disk.flag.img2      206848 360447  153600   75M 82 Linux swap / Solaris
disk.flag.img3      360448 614399  253952  124M 83 Linux
```

To mount the partition, the offset was calculated by multiplying the sector size `360448 * 512 = 184549376`. The flag was found at `/root/my_folder/flag.uni.txt.`

```bash
└─$ sudo mount -o loop,offset=184549376 disk.flag.img /mnt

└─$ ll /mnt
total 39
drwxr-xr-x  2 root root  3072 Sep 29 14:06 bin
drwxr-xr-x  2 root root  1024 Sep 29 11:57 boot
drwxr-xr-x  2 root root  1024 Sep 29 11:57 dev
drwxr-xr-x 27 root root  3072 Sep 29 14:06 etc
drwxr-xr-x  2 root root  1024 Sep 29 11:57 home
drwxr-xr-x  9 root root  1024 Sep 29 11:57 lib
drwx------  2 root root 12288 Sep 29 11:57 lost+found
drwxr-xr-x  5 root root  1024 Sep 29 11:57 media
drwxr-xr-x  2 root root  1024 Sep 29 11:57 mnt
drwxr-xr-x  2 root root  1024 Sep 29 11:57 opt
drwxr-xr-x  2 root root  1024 Sep 29 11:57 proc
drwx------  3 root root  1024 Sep 29 14:07 root
drwxr-xr-x  2 root root  1024 Sep 29 11:57 run
drwxr-xr-x  2 root root  5120 Sep 29 11:57 sbin
drwxr-xr-x  2 root root  1024 Sep 29 11:57 srv
drwxr-xr-x  2 root root  1024 Sep 29 14:06 swap
drwxr-xr-x  2 root root  1024 Sep 29 11:57 sys
drwxrwxrwt  4 root root  1024 Sep 29 14:06 tmp
drwxr-xr-x  8 root root  1024 Sep 29 11:57 usr
drwxr-xr-x 11 root root  1024 Sep 29 14:06 var

└─$ sudo chmod 777 /mnt/root

└─$ ll /mnt/root
total 1
drwxr-xr-x 2 root root 1024 Sep 29 14:09 my_folder

└─$ ll /mnt/root/my_folder 
total 1
-rw-r--r-- 1 root root 60 Sep 29 14:08 flag.uni.txt

└─$ cat /mnt/root/my_folder/flag.uni.txt
picoCTF{by73_5urf3r_2f22df38}
```

Flag: `picoCTF{by73_5urf3r_2f22df38}`

<br>

### Operation Oni
`300 points` `1451 solves`

> `disk`<br>
> Download this disk image, find the key and log into the remote machine.<br>
> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.<br>
> - [Download disk image](https://artifacts.picoctf.net/c/378/disk.img.gz)<br>
> - Remote machine: `ssh -i key_file -p 53924 ctf-player@saturn.picoctf.net`

Unzipped the file and used `fdisk` to check the partitions. Mounted the Linux with the offset `206848 * 512 = 105906176`.

```bash
└─$ gzip -d disk.img.gz

└─$ fdisk -lu disk.img
Disk disk.img: 230 MiB, 241172480 bytes, 471040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0b0051d0

Device     Boot  Start    End Sectors  Size Id Type
disk.img1  *      2048 206847  204800  100M 83 Linux
disk.img2       206848 471039  264192  129M 83 Linux

└─$ sudo mount -o loop,offset=105906176 disk.img /mnt
```

SSH keys are usually stored in public and private key pairs under the user home directory `~/.ssh`, with the public key having the file extension of `.pub`. Searched for `.pub` files and the directory `/root/.ssh` was revealed.

```bash

└─$ sudo chmod 777 /mnt/root

└─$ find /mnt -name *.pub   
find: ‘/mnt/var/log/chrony’: Permission denied
find: ‘/mnt/root/.ssh’: Permission denied
...
```

Granted permission to access the folder and use the key, which was used to connect to the SSH server and obtained the flag.

```bash
└─$ ll /mnt/root/.ssh
total 2
-rw------- 1 root root 411 Oct  6 10:30 id_ed25519
-rw-r--r-- 1 root root  96 Oct  6 10:30 id_ed25519.pub

└─$ sudo chmod 777 /mnt/root/.ssh/id_ed25519

└─$ ssh -i /mnt/root/.ssh/id_ed25519 -p 53924 ctf-player@saturn.picoctf.net
...
ctf-player@challenge:~$ ls -a
.  ..  .cache  .ssh  flag.txt

ctf-player@challenge:~$ cat flag.txt
picoCTF{k3y_5l3u7h_75b85d71}
```

Flag: `picoCTF{k3y_5l3u7h_75b85d71}`

<br>

### Operation Orchid
`300 points` `1340 solves`

> `disk`<br>
> Download this disk image and find the flag.<br>
> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.<br>
> - [Download compressed disk image](https://artifacts.picoctf.net/c/238/disk.flag.img.gz)

Unzipped the file and used `fdisk` to check the partitions. Mounted the Linux with the offset `411648 * 512 = 210763776`. The encoded flag was found at `/root/flag.txt.enc`.

```bash
└─$ gzip -d disk.flag.img.gz

└─$ fdisk -lu disk.flag.img 
Disk disk.flag.img: 400 MiB, 419430400 bytes, 819200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xb11a86e3

Device         Boot  Start    End Sectors  Size Id Type
disk.flag.img1 *      2048 206847  204800  100M 83 Linux
disk.flag.img2      206848 411647  204800  100M 82 Linux swap / Solaris
disk.flag.img3      411648 819199  407552  199M 83 Linux

└─$ sudo mount -o loop,offset=210763776 disk.flag.img /mnt

└─$ sudo chmod 777 /mnt/root

└─$ ll /mnt/root
total 1
-rw-r--r-- 1 root root 64 Oct  6 14:32 flag.txt.enc

└─$ cat /mnt/root/flag.txt.enc 
Salted__�����ݔ?�(�
                  ��$   E�i��Zx�W�^�7ߴzUȤ7� ���؎$�'%

└─$ file /mnt/root/flag.txt.enc 
/mnt/root/flag.txt.enc: openssl enc'd data with salted password
```

The flag was encoded with `openssl` with salted password, where a key is needed to decrypt the flag. It is likely that the key will exist in `.bash_history` if the encrypted was done locally, yet the file was not found. A search revealed that the history file was renamed to `.ash_history`.

```bash
└─$ cat /mnt/root/.bash_history         
cat: /mnt/root/.bash_history: No such file or directory

└─$ find . -name *history*
/mnt/root/.ash_history
```

Granted permission to read the history, and indeed the encryption was done locally with the key revealed as `unbreakablepassword1234567`. The flag was then decrypted with the information found.

```bash
└─$ sudo chmod 777 /mnt/root/.ash_history

└─$ cat /mnt/root/.ash_history 
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt

└─$ openssl enc -aes-256-cbc -d -salt -in /mnt/root/flag.txt.enc -k unbreakablepassword1234567
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
bad decrypt
281472862390880:error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:../crypto/evp/evp_enc.c:610:
picoCTF{h4un71ng_p457_1d02081e}
```

Flag: `picoCTF{h4un71ng_p457_1d02081e}`

<br>
