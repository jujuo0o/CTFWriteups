# Hacktober 2020
Stenography challs are not included here.
## Start 
### Rules - 0x1

> _Submit this as the flag you've read and understand the rules: flag{pl4y_by_th3_ru13s}_

Flag: **flag{pl4y_by_th3_ru13s}**
### DEADFACE  1 - 0x2

> _How many threat actors are identified on the DEADFACE intel page? Submit the flag as flag{#}_

Threat Actors were listed on "Intel" page.
Flag: **flag{7}**

### DEADFACE 2 - 0x3

> _According to the intel on DEADFACE, what is the username of the threat actor believed to be the second-in-command of DEADFACE? Submit the flag as flag{username}._

"second-in-command" can be found on "intel" page
Flag: **flag{mort1cia}**

### UNCOMN - 0x4

> _Which Hacktober sponsor has the following mission statement:_ _We analyze, design and deliver customized people, process, technology, and data solutions to solve your most complex business challenges._ _Submit the flag as flag{Company_Name}._

Flag: **flag{UNCOMN}**

### Core Values - 0x5

> _How many core values are listed on UNCOMN's website? Submit the flag as flag{#}_

Flag: **flag{5}**
### Lets Begin - 0x6

> _Now that you've answered the starter questions, let's get on with the CTF! Enter this as the flag: flag{lets_get_started}_

Flag: **flag{lets_get_started}**


## Trafic Analysis 

### Evil Corp's Child - 0x1

> _What is the MD5 hash of the Windows executable file?_

The Executable file is being transmitted over HTTP with the file name **picture4.png**, simple export the file and perform:

    md5sum picture4.png
    a95d24937acb3420ee94493db298b295  picture4.png
Flag: **flag{a95d24937acb3420ee94493db298b295}**

### Evil Corp's Child 2 - 0x2

> _The malware uses four different ip addresses and ports for communication, what IP uses the same port as https? Submit the flag
> as: flag{ip address}._
    
 
Flag **flag{213.136.94.177}**

### Evil Corp's Child 3 - 0x3

> _What is the localityName in the Certificate Issuer data for HTTPS traffic to 37.205.9.252?_

Flag **flag{Mogadishu}**


### Evil Corp's Child 4 - 0x4

> _What type of malware infection is exhibited in this traffic?_

Search for community responses for the file found on "Evil Corp's Child 1"  to find the infection type.

Flag **flag{Dridex}**

###  Remotely Administrated Evil - 0x5

> *What is the name of the executable in the malicious url?*

Filter HTTP data and you will notice that a file is being recieved with name "solut.exe"

Flag: **flag{solut.exe}**

###  Remotely Administrated Evil 2 - 0x6

> *What MYDDNS domain is used for the post-infection traffic in RATPack.pcap?*

Filter DNS protocol and then you will see that a request is being made to a suspicious looking website.

Flag **flag{`solution.myddns.me`}**


###  Remotely Administrated Evil 3 - 0x7

> *What type of malware infection is Example 1?*

Submit the file found on "Remote Administrated Evil 1" to virustotal. Looking at the community responses you can see that the virus connect to netwire. 

Flag: **flag{Netwire Rat}**


### An Evil Christmas Carol - 0x8

> _A malicious dll was downloaded over http in this traffic, what was the ip address that delivered this file?_

Filter HTTP data and look for GET requests:

Flag **flag{205.185.125.104}**


### An Evil Christmas Carol 2 - 0x9

> What is the domain used by the post-infection traffic over HTTPS?

Again Filter DNS protocol for suspicious website requests.

Flag: **flag{`vlcafxbdjtlvlcduwhga.com`}**


### An Evil Christmas Carol 3 - 0x10

> What is the domain used by the post-infection traffic over HTTPS?

Searching the sha256 of the file found on "An Evil Christmas Carol 1" along with the challenge author username will lead you to a website that will provide the activity type.

Flag: **flag{zloader}**


## SQL
### Body Count - 0x1

> *How many users exist in the Shallow Grave University database?*

Get user count from table "users"

    select count(*) from users;
outputs:

	+----------+
	| count(*) |
	+----------+
	|      900 |
	+----------+

Flag: **flag{900}**

### Past Demons - 0x2

> *We've had a hard time finding anything on spookyboi. But finally, with some search engine finessing, an analyst found an old, vulnerable server spookyboi used to run. We extracted a database, now we need your help finding the password*

    select * from users;
Outputs:

	...
	8|spookyboi|
	...
Now:

    select * from passwd;
Will return:

    8|59DEA36D05AACAA547DE42E9956678E7|8

Now google search for "59DEA36D05AACAA547DE42E9956678E7" and you will recieve its plaintext: zxcvbnm
Flag: **flag{zxcvbnm}**


### Address Book - 0x3

> *Shallow Grave University has provided us with a dump of their database. Find luciafer's email address and submit it as the flag in this format: `flag{username@email.com}`*

    select * from users where first like "%lucia%"
Output:

    +---------+------------+-------+--------+--------+-----------------------------------+--------------+------------+----------+-------+--------+------------+
	|      49 | luchav1987 | LUCIA | HAVRON | R      | luc1afer.h4vr0n@shallowgraveu.com | 2991 Y Alley | Broken Bow |       38 | 27856 | f      | 1987-12-13 |
	+---------+------------+-------+--------+--------+-----------------------------------+--------------+------------+----------+-------+--------+------------+
Flag: **flag{`luc1afer.h4vr0n@shallowgraveu.com`}**


### Calisota - 0x4

> *One of our other analysts isn't familiar with SQL and needs help
 finding out how many users live in which states. Submit the SQL
 command used to get the total number of users in the `users` table who live in California and Minnesota.*

    select * from states where state_full='California' or state_full='Minnesota'
Output:

	+----------+------------+--------------+------------+
	| state_id | state_full | state_abbrev | country_id |
	+----------+------------+--------------+------------+
	|        6 | California | CA           |        199 |
	|       28 | Minnesota  | MN           |        199 |
	+----------+------------+--------------+------------+

Now count:

    select count(*) from users where state_id=6 or state_id=28;

Output:

	+----------+
	| count(*) |
	+----------+
	|       40 |
	+----------+

Flag: **flag{SELECT COUNT(*) FROM users WHERE state_id=6 OR state_id=28;}**

### Fall Classes - 0x5

> *Without counting duplicates, how many courses are being offered in the FALL2020 term at Shallow Grave University?*

term_id for FALL2020 is 2 so

    select count(distinct(course_id)) as count from term_courses where term_id=2;

will output

	+-------+
	| count |
	+-------+
	|   401 |
	+-------+
Flag: **flag{401}**

### 90s Kids - 0x6

> *According to conversations found in Ghost Town, r34p3r despises 90s kids and tends to target them in his attacks. How many users in the Shallow Grave SQL dump were born in October in the 1990s?*

    select count(*) as total from users where year(dob)>=1990 and year(dob)<2000 and month(dob)=10;
Output:

	+-------+
	| total |
	+-------+
	|    32 |
	+-------+

Flag: **flag{32}**

### Jigsaw - 0x7

> *We've slowly been piecing together the name of one of DEADFACE's future victims. Here's the information we have:*
> 
> -   *The first two characters of the user's last name begin with K, R, or I.*
> -   *Followed by any character except newline, then three letters*
> -   *Immediately followed by the last letter E-N*
> 
> *Submit the username as the flag: `flag{username}`*

    select username from users where last RLIKE '[KRI][KRI]....[E-N]' and LENGTH(last)=7;
Output:

	+----------------+
	| username       |
	+----------------+
	| image.wa1k3624 |
	+----------------+

Flag: **flag{image.wa1k3624}**


### Student Body - 0x8

> *We believe Lucia is trying to target a student taught by her SOCI424 professor. How many students were taught by that professor in either term? Submit the number of students as well as the professor's first and last name concatenated.*

#### Step 1 - Find Who Teaches Lucia

    select t.instructor from enrollments e left join term_courses t on e.term_crs_id=t.term_crs_id left join courses c on t.course_id = c.course_id WHERE c.title='SOCI424' and e.user_id=49;
Output:

	+------------+
	| instructor |
	+------------+
	|        480 |
	+------------+
#### Step 2  - Get Professors Name

    select CONCAT(first,last) as name from users where user_id=480;
Output:

	+-----------------+
	| name            |
	+-----------------+
	| CLAUDEDARRACOTT |
	+-----------------+
#### Step 3 - Get Number Of Students Taught By Professor In FALL2020

    select count(*) as count from enrollments e left join term_courses t on e.term_crs_id=t.term_crs_id where t.instructor=480 and t.term_id=2;
Output:

	+-------+
	| count |
	+-------+
	|    57 |
	+-------+

Flag: **flag{57_CLAUDEDARRACOTT}**


## Programming 
### Message In An Array


> *Deadface has left a message in the code. Can you read the code and figure out what it says? You may also copy and paste the code in an emulator. Enter the answer as `flag{Word Word Word Word}`.*


```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace GhostTown
{
    class Program
    {
        static void Main(string[] args)
        {
           string[] str = new string[4] {"DEADFACE","Nothing", "Stop", "Will"};
           Console.WriteLine("{1} {3} {2} {0}", str);
         }
    }
}
```
Flag: **flag{Nothing Will Stop DEADFACE}**

### Trick Or Treat

> *We found a script being used by DEADFACE. It should be relatively straightforward, but no one here knows Python very well. Can you help
> us find the flag in this Python file?*
from hashlib import md5 as m5


    def show_flag():
        b = 'gginmevesogithoooedtatefadwecvhgghu' \
            'idiueewrtsadgxcnvvcxzgkjasywpojjsgq' \
            'uegtnxmzbajdu'
        c = f"{b[10:12]}{b[6:8]}{b[4:6]}{b[8:10]}" \
            f"{b[4:6]}{b[12:14]}{b[2:4]}{b[0:2]}" \
            f"{b[14:16]}{b[18:20]}{b[16:18]}{b[20:22]}"
        m = m5()
        m.update(c.encode('utf-8'))
        d = m.hexdigest()
        return f"flag{{{d}}}"
    
    
    def show_msg():
        print(f'Smell my feet.')
    
    
    show_msg()

Just call the `show_flag()` function and you will get the flag
Flag: **flag{2f3ba6b5fb8bb84c33b584f981c2d13d}**


## Linux
### Talking to the Dead 1

> *We've obtained access to a server maintained by spookyboi. There are four flag files that we need you to read and submit (flag1.txt,
> flag2.txt, etc). Submit the contents of `flag1.txt`.*
`ssh hacktober@env.hacktober.io`
Password: `hacktober-Underdog-Truth-Glimpse`

execute:

    find | grep flag

you will find 4 flag files,

> ./home/luciafer/Documents/.flag2.txt
./home/luciafer/Documents/flag1.txt
./home/spookyboi/Documents/flag3.txt
./root/flag4.txt

then show the contents of flag1.txt

	cat /home/luciafer/Documents/flag1.txt
	flag{cb07e9d6086d50ee11c0d968f1e5c4bf1c89418c}

Flag: **flag{cb07e9d6086d50ee11c0d968f1e5c4bf1c89418c}**


### Talking to the Dead 2 

> *There's a hidden flag that belongs to luciafer. Submit the contents of the hidden flag2.txt.*

`cat` the flag2.txt found in `talking to dead 1`

    cat /home/luciafer/Documents/.flag2.txt
    flag{728ec98bfaa302b2dfc2f716d3de7869f3eadcbf}

Flag: **flag{728ec98bfaa302b2dfc2f716d3de7869f3eadcbf}**


### Talking to the Dead 3

> *Submit the contents of `flag3.txt` from the remote machine.*

flag3.txt is owned by `spookyboi` so we need some kind of privilege escalation. 
We can search for some SUID binaries such as

    find -perm -u=s
we will find some binaries.

	./usr/bin/umount
	./usr/bin/passwd
	./usr/bin/mount
	./usr/bin/gpasswd
	./usr/bin/su
	./usr/bin/chsh
	./usr/bin/newgrp
	./usr/bin/chfn
	./usr/local/bin/ouija
	./usr/lib/openssh/ssh-keysign
	./usr/lib/dbus-1.0/dbus-daemon-launch-helper
now if you can see there is one suspicious looking binary `ouija`. lets execute it and find out what it do?.

    luciafer@3b887b8931d8:/$ ouija
	OUIJA 6.66 - Read files in the /root directory
	Usage: ouija [FILENAME]
	EXAMPLES:
		ouija file.txt
		ouija read.meluciafer@3b887b8931d8:/$ 
We can see that this binary can be used to read all files with root permissions.

    luciafer@3b887b8931d8:/$ ouija /home/spookyboi/Documents/flag3.txt
	/usr/bin/cat: /root//home/spookyboi/Documents		
	/flag3.txt: No such file or directory
as you can see that `ouija` adds "/root/" prefix before path so we can bypass it with adding `../`

    ouija ../home/spookyboi/Documents/flag3.txt
    flag{445b987b5b80e445c3147314dbfa71acd79c2b67}

Flag: **flag{445b987b5b80e445c3147314dbfa71acd79c2b67}**


### Talking to the Dead 4
> *We suspect spookyboi doesn't use the root account for this server. There must be some mechanism used to read the flag4.txt file without
> gaining root. Submit the contents of `flag4.txt` from the remote
> machine.*

Same method from `Talking to the Dead 3` will be used to read the flag4.txt under `root` dir.

    ouija flag4.txt
    flag{4781cbffd13df6622565d45e790b4aac2a4054dc}
Flag: **flag{4781cbffd13df6622565d45e790b4aac2a4054dc}**


## Cryptography

### Hail Caesar!
> *This image was found in Ghost Town along with the encoded message below. See if you can decipher the message. Enter the entire decoded
> message as the flag. Decode this: _TGG KUSJWV QGM_*

Looking at the ciphertext it seems some king of rotation is performed. Now we can get the plaintext by simply rotating the ciphertext 26 time.

    inp="TGG KUSJWV QGM"
	def rotate(day):
		cipher= ""
		for i in inp:
			c_ord = ord(i)+day
			if ord(i)>=65 and ord(i)<=90:
				if c_ord>90:
					c_ord = 64+(c_ord-90)
				cipher+=chr(c_ord)
			elif ord(i)>=97 and ord(i)<=122:
				if c_ord>122:
					c_ord=96+(c_ord-122)
				cipher+=chr(c_ord)
			else:
				cipher+=i
		return cipher

	for i in range(1,26):
		print(rotate(i))
Outputs:

	UHH LVTKXW RHN
	VII MWULYX SIO
	WJJ NXVMZY TJP
	XKK OYWNAZ UKQ
	YLL PZXOBA VLR
	ZMM QAYPCB WMS
	ANN RBZQDC XNT
	BOO SCARED YOU
	CPP TDBSFE ZPV
	DQQ UECTGF AQW
	ERR VFDUHG BRX
	FSS WGEVIH CSY
	GTT XHFWJI DTZ
	HUU YIGXKJ EUA
	IVV ZJHYLK FVB
	JWW AKIZML GWC
	KXX BLJANM HXD
	LYY CMKBON IYE
	MZZ DNLCPO JZF
	NAA EOMDQP KAG
	OBB FPNERQ LBH
	PCC GQOFSR MCI
	QDD HRPGTS NDJ
	REE ISQHUT OEK
	SFF JTRIVU PFL

Now search through the output and you will see a readable text:

	BOO SCARED YOU
Flag: **flag{BOO SCARED YOU}**

### Down the Wrong Path

> *One of our operatives took a photo of a notebook belonging to Donnell. We think it's a message intended for another member of
> DEADFACE. Can you decipher the message and tell us who it's intended for?*

Looking at the image provided, it looks like transposition cipher. Except here no  shuffling has been applied, so if you read the text  column by column you will get:
	

    REMEMBER TO TELL SPOOKYBOI ABOUT THE NEW TARGETS OF OUR NEXT ATTACK

Flag: **flag{REMEMBER TO TELL SPOOKYBOI ABOUT THE NEW TARGETS OF OUR NEXT ATTACK}**

### Cover your Bases

> *One of the other junior analysts stumbled upon this and isn't quite sure what to make of it. Based on the context that it was found, it
> might be a coded message. 
> Decode this: `ZmxhZ3tzaG91bGRhX21hZGVfdGhpc19vbmVfaGFyZGVyfQ==`*

This is base64 encoded so simple execute the following on your terminal

    echo ZmxhZ3tzaG91bGRhX21hZGVfdGhpc19vbmVfaGFyZGVyfQ== | base64 -d
	flag{shoulda_made_this_one_harder}

Flag: **flag{shoulda_made_this_one_harder}**

