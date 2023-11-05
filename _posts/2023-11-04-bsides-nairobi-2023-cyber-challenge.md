---
layout: post
title: BSides Nairobi 2023 Cyber Challenge
date: '2023-11-04 12:46:04 +0300'
image: /assets/img/cover_images/40.png
categories: [CTF, BSides Nairobi 2023 Cyber Challenge]
---
## Mobile
### Daily blatha
Every day blatha. One part here, another there.
#### You got all my journals? (150pts) 
Use frida to get the name of the app or any other way 
```bash
b3nj4h@arch ~> frida-ps -aU
 PID  Name               Identifier               
----  -----------------  -------------------------
6010  Email              com.android.email        
6386  Google Play Store  com.android.vending      
5402  Messaging          com.android.messaging    
5975  Phone              com.android.dialer       
5632  Superuser          com.genymotion.superuser 
6254  dailyblatha        com.bsidesnrb.dailyblatha
```
we spawn the firebase activity with activity manager 
```bash
am start -n com.bsidesnrb.dailyblatha/.firebaseActivity
Starting: Intent { cmp=com.bsidesnrb.dailyblatha/.firebaseActivity }
```
The app has insecure logging

![img-description](/assets/img/bsides2023/8.png)

We try to grep for BSidesNRB using logcat inside the AVD
```bash
logcat | grep -i BSidesNRB
```
and we get the first piece of the flag
```bash
11-04 06:52:19.517  6254  6254 D BSidesNRB: Value is: BSidesNBI{4ndro1d
```
Next we open the sqlite activity to spawn the database
```bash
am start -n com.bsidesnrb.dailyblatha/.sqliteActivity  
Starting: Intent { cmp=com.bsidesnrb.dailyblatha/.sqliteActivity }
```

![img-description](/assets/img/bsides2023/10.png)

The database is initialize we pull it since we know the name
```bash
adb pull /data/data/com.bsidesnrb.dailyblatha/databases/bsidesnrb.db
```
we use sqlite 3 to get the second flag
```bash
b3nj4h@arch > sqlite3 bsidesnrb.db
SQLite version 3.43.2 2023-10-10 12:14:04
Enter ".help" for usage hints.
sqlite> .tables
android_metadata  flag            
sqlite> select * from flag
   ...> ;
1|flag2|_db_m1sc0nf1gs
sqlite> 
```
We navigate to sharedPrefsActivity and find this

![img-description](/assets/img/bsides2023/9.png)

We decode the string and get the third part of the flag
```bash
b3nj4h@arch ~> echo XzRyM19kNG5nM3IwdXNzc30= | base64 -d
_4r3_d4ng3r0usss}
```
We now have the full flag
```
BSidesNBI{4ndro1d_db_m1sc0nf1gs_4r3_d4ng3r0usss}
```

### Whatslif3
Thou shall find what made him one with the world.
#### This took us out? (75pts) 
From the source code we see that the input should be a base64 decoded string check_guess
![img-description](/assets/img/bsides2023/3.png)
We get the string from resources and base64 decode it
```bash
b3nj4h@arch ~> echo QlNpZGVzTkJJe3RoaXNfZGlkbid0X2tpbGxfdGhlbX0= | base64 -d
BSidesNBI{this_didn't_kill_them}
```
We use the output as our input string and hit the submit button. We get the activity with this encoded string

![img-description](/assets/img/bsides2023/2.png)

We take the string and slap it in cyber chef and wait for it to do the magic. Boom there we go we get the flag

![img-description](/assets/img/bsides2023/4.png)


## Forensics
### Mystique
Start by analyzing this email.

#### Who is the sender of this email?  (25pts) 
cat the file and grep for the X-Sender
```bash
cat infected.eml | grep -i X-Sender
X-Sender: 2export@ekofood.com.tr
```
#### What is the md5sum of the email attachment? (25pts) 
Download the attachment with thunderbird and check the md5sum hash
```bash
md5sum Items\ list.doc
2dae57b509d72eb69166e9d48995e530
```
#### Without opening the attachment on your host machine, use an online sandbox like AnyRun to observe what happens when the document is opened. From your analysis, what CVE is associate with the attachment? (25pts)
Open the file with virus total and navigate to community you'll get the CVE from ANY_RUN

![img-description](/assets/img/bsides2023/5.png)

#### What malware family is likely associated with the attachment? (25pts) 
From the previous image we can see the malware family 
```
agenttesla
```

#### Take a look at the malware configuration. What is the c2 Domain address? (25pts) 
Navigate to behaviour and check under DNS resolution

![img-description](/assets/img/bsides2023/6.png)

#### In your opinion, what protocol do you suspect could have been leveraged on for potential exfiltration? (25pts) 
The malware uses port 587 which is an smtp protocol port

![img-description](/assets/img/bsides2023/7.png)
