---
layout: post
title: Storage Upgrade and Backup
date: 2009-03-30
comments: true
categories: Ruby
---

Hard drive upgrade
-------
I needed to upgrade from my 80GB MacBook hard drive, and also wanted to improve my personal data backup plan.  I decided to use Time Machine on OS X because it is really easy to use. For my *really* critical files (a subset of the Time Machine backup), I'm storing an additional copy on S3. This way critical files could be restored from Time Machine or S3.

The physical hard drive upgrade went as follows. For complete details, see Macinstruct tutorial: [How to Upgrade Your MacBook's Hard Drive](http://www.macinstruct.com/node/130).

 1. Remove battery
 2. Unscrew three screws to remove "L-bracket"
 3. Pull "paper" tab to slide hard drive caddy out, note position of hard drive
 4. Remove 4 torx screws around hard drive caddy (I did this with a needle-nose pliers and my Stanley small screwdriver set since I don't have a torx screwdriver)
 5. Replace 4 screws with new hard drive in caddy

Slide the caddy back in, screw the L-bracket back in, replace the battery.

Time Machine backups
---
My new internal and external backup hard drives are as follows.

 1. (internal) Seagate 2.5" 320GB 5400rpm
 2. (external) Seagate "Go" 2.5" 500GB external USB drive

Using Disk Utility, I created two partitions for the new internal drive, one for Time Machine backups, the second for general data storage. I used the default `Mac OS Extended (Journaled)` partition type for both. 

I decided to reinstall Leopard. Interestingly I reduced the installation size by removing things I won't use (foreign language translations, Office 2004 Trial) from 15GB to 9GB. I could have backed-up my previous installation to the new external first, then restored from a Time Machine backup, however I wanted a clean installation at the cost of being being more time consuming.

When the drive was partitioned, OS X asked me whether I wanted to use either of the partitions for Time Machine backups, I chose the first one. Time Machine has run a few times since writing this article.  It runs when I connect the backup drive, since I normally leave it unplugged.

S3 backups
---
I created a new S3 account after reviewing the costs and terms. I have read reports of monthly bills in the "cents," so I am not too worried about the costs. There are no upfront costs.

I did a `gem install s3sync` to use the ruby library `s3sync` to interact with my new S3 account. I will also show the free Cyberduck FTP/SFTP/S3 client. To supply my credentials to s3sync, I created a .yml file (per the README): `$HOME/.s3conf/s3config.yml` with the following contents.

``` bash
    AWS_ACCESS_KEY_ID:
      access_key
    AWS_SECRET_ACCESS_KEY:
      secret_key
```

`s3cmd` is a shell command that comes with s3sync. Since I am new to this, I'll just demonstrate uploading one file and verifying the upload. My plan is to eventually develop a script that does a complete backup of my critical files and runs automatically. The Cyberduck client is nice, but a command line scripted backup would give me a lot of flexibility.

Here is some terminal output demonstrating bucket creation, uploading a picture PC070009.JPG to that bucket, then listing the contents of that bucket to verify the upload. Note I'm using the filename as the "key" for this example, but you would probably use a key that mirrors a folder hierarchy. I also had `openssl` installed already via MacPorts, I used the `--ssl` option when uploading the file.

``` bash
s3cmd createbucket andyatkinson-backup
s3cmd listbuckets
andyatkinson-backup
s3cmd put andyatkinson-backup:PC070009.JPG PC070009.JPG --ssl
warning: peer certificate won't be verified in this SSL session
s3cmd list andyatkinson-backup:PC070009.JPG
--------------------
PC070009.JPG
```
In order to connect to your S3 account with Cyberduck, supply the required credentials. If you used the .yml file as I mentioned above, display the contents of the file `cat $HOME/.s3conf/s3config.yml` and copy and paste.

I hope this gave you some useful information on backing up data to S3 and more.
