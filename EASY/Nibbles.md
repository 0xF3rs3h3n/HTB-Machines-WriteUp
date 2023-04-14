# Write Up - Nibbles

**Disclaimer: This article is for educational purposes only, do not attempt to hack system without prior consent from the person you are hacking, and only use this information for ethical purposes.**

## Basic Information
### URL
> https://app.hackthebox.com/machines/Nibbles

<img src=./img/Nibbles/Nibbles.png width=500px>

<br>

## Attack Flow
| NO. | TID | Tactics | Techniques |
| ---- | ---- | ---- | ---- |
| [001](#001) | T1594 | Reconnaissance | Search Victim-Owned Websites  |
| [002](#002) | T1589.002 | Reconnaissance | Gather Victim Identity Information / Email Addresses |
| [003](#003) | T1110.001 | Credential Access | Brute Force / Password Guessing |
| [004](#004) | T1588.006 | Resource Development | Obtain Capabilities / Vulnerabilities |
| [005](#005) | T1587.001 | Resource Development | Develop Capabilities / Malware |
| [006](#006) | T1190 | Initial Access | Exploit Public-Facing Application |
| [007](#007) | T1587.001 | Resource Development | Develop Capabilities / Malware #2 |
| [008](#008) | T1190 | Initial Access | Exploit Public-Facing Application #2 |
| [009](#009) | T1082 | Discovery | System information discovery |
| [010](#010) | T1083 | Discovery | File and Directory Discovery
| [011](#011) | T1548.003 | Privilege Escalation | Abuse Elevation control Mechanism / Sudo and Sudo Caching
| [012](#012) | T1552.001 | Credential Access | Unsecured Credentials / Credentials in Files 


<br>

## 001 : T1594 : Reconnaissance / Search Victim-Owned Websites <a id="001"></a>
### Access to the target server

*Hello world!*

<img src=./img/Nibbles/1_website.png width=500px>

<br>

*Check HTTP source code*

<img src=./img/Nibbles/2_website_source.png width=500px>

<br>

*Access /nibbleblog/*

<img src=./img/Nibbles/3_website_nibbles.png width=700px>

<br>

*Run a web content scanner*

<img src=./img/Nibbles/4_dirb.png width=1200px>

<br>

## 002 : T1589.002 : Reconnaissance / Gather Victim Identity Information / Email Addresses <a id="002"></a>

*Access /admin/ \
It has directory listing*

<img src=./img/Nibbles/5_directory_listing.png width=500px>

<br>

*Access /content/private/config.xml \
Username is possibly "admin"*

<img src=./img/Nibbles/6_configxml.png width=700px>

<br>

## 003 : T1110.001 : Credential Access / Brute Force / Password Guessing <a id="003"></a>

*Access admin.php \
Log in as admin:nibbles \
#I learned should check a machine name and easy passwords \
Note: This website has feature of access block using IP address* :(

<img src=./img/Nibbles/7_loginform.png width=500px>

<br>

*Admin dashboard*

<img src=./img/Nibbles/8_adminpage.png width=700px>

<br>

## 004 : T1588.006 : Resource Development / Obtain Capabilities / Vulnerabilities <a id="004"></a>

*Searchsploit*

<img src=./img/Nibbles/9_searchsploit.png width=1200px>

<br>


*Version is 4.0.3 \
from /nibbleblog/README*

<img src=./img/Nibbles/9a_readme.png width=500px>


<br>

*exploitdb*

<img src=./img/Nibbles/10_exploitdb.png width=700px>

<br>

*Plugin "my_image" has the vulnerability of arbitrary file upload (CVE-2015-6967)*

<img src=./img/Nibbles/12_exploiotdb3.png width=1200px>

<br>

## 005 : T1587.001 : Resource Development / Develop Capabilities / Malware <a id="005"></a>

*Payload for PoC of CVE-2015-6967*

<img src=./img/Nibbles/13_webshell.png width=300px>

<br>

## 006 : T1190 : Initial Access / Exploit Public-Facing Application <a id="006"></a>

*Attempt to upload the payload using "my_image" plugin*

<img src=./img/Nibbles/14_plugin.png width=1000px>

<br>

*Upload the payload*

<img src=./img/Nibbles/16_uploding_webshell.png width=550px>

<br>

*Upload succeeded*

<img src=./img/Nibbles/17_uploaded.png width=800px>

<br>

*Payload has information of upload directory \
Directory is /content/private/plugins/my_image/image.php*

<img src=./img/Nibbles/18_directory.png width=800px>

<br>

*Access image.php*

<img src=./img/Nibbles/24_image.png width=600px>

<br>

*Exploit is successed*

<img src=./img/Nibbles/19_id.png width=800px>

<br>

## 007 : T1587.001 : Resource Development / Develop Capabilities / Malware #2 <a id="007"></a>

*Preparing a reverseshell*

<img src=./img/Nibbles/20_reverseshell.png width=1300px>

<br>

## 008 : T1190 : Initial Access / Exploit Public-Facing Application #2 <a id="008"></a>

*Run nc on a local machine to catch reverseshll*

<img src=./img/Nibbles/21_nc.png width=300px>

<br>

*Upload the reverseshell and run same way*

<img src=./img/Nibbles/22_uploading_reverseshell.png width=600px>

<br>

<img src=./img/Nibbles/23_uploaded.png width=600px>

<br>

*Obtaining the shell after accessing image.php*

<img src=./img/Nibbles/24_image.png width=600px>

<br>

<img src=./img/Nibbles/25_get_shell.png width=600px>

<br>

## 009 : T1082 : Discovery / System information discovery <a id="009"></a>

*login user*

<img src=./img/Nibbles/26_whoami.png width=180px>

<br>

*Upgrade login shell*

<img src=./img/Nibbles/27_upgradeshell.png width=700px>

<br>

*Check system information*

<img src=./img/Nibbles/28_uname.png width=1300px>

<br>

## 010 : T1083 : Discovery / File and Directory Discovery <a id="010"></a>

*Find a user flag at /home/nibbler/*

<img src=./img/Nibbles/29_userflag.png width=400px>

<br>

## 011 : T1548.003 : Privilege Escalation / Abuse Elevation control Mechanism / Sudo and Sudo Caching <a id="011"></a>

*Check "sudo -l"*

<img src=./img/Nibbles/30_sudo-l.png width=1300px>

<br>

*Unzip personal.zip at /home/nibbler \
Can execute this file as a root without password*

<img src=./img/Nibbles/32_monitorsh.png width=600px>

<br>

*Check file permissions \
This shell script can be modified*

<img src=./img/Nibbles/33_monitorsh_rwx.png width=600px>


<br>

*Modify monitor.sh for privilege escalation \
It aims to spawn bash of root user*

<img src=./img/Nibbles/34_bash.png width=700px>

<br>

*Run monitor.sh with sudo \
#Needs full path*

<img src=./img/Nibbles/35_privesc.png width=1000px>


<br>

## 012 : T1552.001 : Credential Access / Unsecured Credentials / Credentials in Files <a id="012"></a>

*Find a root flag at /root*

<img src=./img/Nibbles/36_rootflg.png width=500px>


