---
layout: post
title:  "How to get and crack hashes."
tagline: Diskcryptor Ransomware
date: 2020-10-10 15:44
categories: [Tasks]
tags: [Med, tasks, tools]
image: diskcryptor.png
---

## Things to download
<p>&nbsp;</p>
Here is a quick list of resources that I downloaded for the tutorial:

(1.) [VMWare Workstation](https://www.vmware.com/au/products/workstation-pro/workstation-pro-evaluation.html), it'll ask you for a key but you can just used the trial version.  

(2.) [Windows 10 VM](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/), grab the one for VMWare.

(3.) [DiskCryptor v1.1](https://github.com/DavidXanatos/DiskCryptor/releases), you want to grab the stable release which is under the BETA versions.

(4.) [diskcryptor2john Python script](https://raw.githubusercontent.com/openwall/john/a02c068c245e43cdab24e412213562cd461638ba/run/diskcryptor2john.py), save this to a text file called <b>diskcryptor2john.py</b>.

(5.) [System Rescue iso](https://www.system-rescue.org/Download/), I got the i868 version.

(6.) [HashCat](https://hashcat.net/hashcat/), program for password cracking.

<p>&nbsp;</p>
## Other resources I used
<p>&nbsp;</p>
Here are the other blogs that I used.

(1.) How to enable the bios boot in a VM check it out [here](https://kb.vmware.com/s/article/1004129). The command you want to add to the VM's <b>.vmx</b> is <b>Add bios.forceSetupOnce = "TRUE"</b>.

(2.) To enable a shared file between the host and VM check this [blog](https://pureinfotech.com/setup-network-file-sharing-windows-10/).

(3.) How to use HashCat in a quick guide created by [LaconicWolf](https://laconicwolf.com/2018/09/29/hashcat-tutorial-the-basics-of-cracking-passwords-with-hashcat/).

(4.) [HashCat hash types](https://hashcat.net/wiki/doku.php?id=example_hashes), this is how I identified the <b>-m</b> option.

(5.) [Password cracking time estimation](https://www.betterbuys.com/estimating-password-cracking-times/), pretty basic but proves a point.

(6.) [ACSC mitigations for ransomware](https://www.cyber.gov.au/acsc/view-all-content/threats/ransomware), great resource for anyone to read over. 

<p>&nbsp;</p>
## Command line help
<p>&nbsp;</p> 
Within the system rescue iso to view the drives run;

<b>fsarchiver probe simple</b>

To mount the shared network drive once it's set up run;

<b>cd /mnt</b>

<b>mkdir shared</b>

<b>/usr/bin/mount -t cifs //<YOUR HOSTNAME>/Downloads /mnt/shared</b>

Then to copy the Python script across;

<b>cp shared/diskcryptor2john.py /usr/bin/</b>

Find the drive you want to run the script against from <b>fsarchiver</b> and then run;

<b>/usr/bin/diskcryptor2john.py /dev/sda1 >> shared/dcrypt-hashes.txt</b>

Then open a command line in Windows in the directory of HashCat executable and run;

<b>hashcat.exe -a 0 -m 20011 C:\<your path to the hashes>\dcrypt-hashes.txt example.dict -O</b>

If the password is cracked it will show in the console.

<p>&nbsp;</p>
## Explanation
<p>&nbsp;</p>
This task took me a while to figure out so I'm not going to explain it here. If you know enough the commands should be enoughotherwise you'll just have to watch me fumble around in the video.

[![](https://img.youtube.com/vi/Vey-ll3LM3o/maxresdefault.jpg)](https://youtu.be/Vey-ll3LM3o)
