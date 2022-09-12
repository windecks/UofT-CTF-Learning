# Week 2

Congrats on completing Week 1! By now, you should be familiar with the Linux command line, using VMs, and have gained some basic skills in Web exploitation, OSINT, etc. If you followed the "beginner" path last week, try out the "non-beginner" path before continuing on this week's exercises.

## Tools commonly used in CTFs

**Web exploitation** uses a variety of tools with various functions. When it comes to browser extensions, [cookie managers](https://chrome.google.com/webstore/detail/cookiemanager-cookie-edit/hdhngoamekjhmnpenphenpaiindoinpo) (available on Chrome and Firefox), [HTTP Request](https://chrome.google.com/webstore/detail/tamper-dev/mdemppnhjflbejfbnlddahjbpdbeejnn) editors, and [User-Agent controllers](https://chrome.google.com/webstore/detail/user-agent-switcher-for-c/djflhoibgkdhkhhcedjiklpkjnoahfmg) are great. The respective extensions for Chrome are linked.

Many of these functions are also tied into Burp Suite, an application that streamlines web exploitation and penetration testing. Burp Suite allows a lot more fine-tuned control on these functions. [Here's a link to the website.](https://portswigger.net/burp)

SQL injection tools are also commonly used in web exploitation. `sqlmap` is a commonly used tool that allows automatic SQL injection. [Here's a link.](https://sqlmap.org/)

Finally, `dirsearch` and `dirb` are tools to search directory paths on a website that may not be explicitly displayed:

http://dirb.sourceforge.net/

https://github.com/maurosoria/dirsearch

**Reverse Engineering** also features quite a few tools. Reverse engineering tools are generally split into two categories - static analysis, and dynamic analysis. In static analysis, binaries are analyzed in a static state. In dynamic analysis, binaries are executed and analyzed in a dynamic environment! Note that dynamic analysis is not necessarily better than static analysis. A lot of the time, dynamic analysis tools may introduce false positives and negatives. For challenging problems, both types of analysis may be required.

The two most popular disassemblers are IDA Pro and Ghidra. Ghidra is developed by the NSA, and is available for free on their website. IDA Pro requires a very expensive license, but for personal use, most people will obtain copies illegaly (piracy).

Debuggers are designed around either static or dynamic analysis. OllyDbg is a great debugger that does both, specifically designed around binary code analysis. WinDbg debugs Windows drivers, gdb specializes in dynamic analysis, and Vivisect combines disassembly and debugging into one package.

**Forensics** involves the forensic analysis of a variety of files. Packet analysis is a common challenge in forensics. A packet is a small segment of a message, sent over the internet. For example, "UofTCTF" may be sent in packets, featuring the individual characters. A .pcap file (The packets are captured into a file) can be interpreted by applications such as Wireshark. 

Sleuthkit (and its GUI-included counterpart, Autopsy) are tools used for disk image analysis. 

Steganography is also a common challenge in forensics. If data is hidden in an image, command-line tools such as `zsteg` can be used to efficiently retrieve the hidden data. There are also a ton of online tools that specialize in specific image types too.

Nested files are also featured in a lot of challenges. A nested file is a file hidden inside a file! `binwalk` is the most popular tool for discovering hidden files. It is also a command-line tool.

**Binary Exploitation** involves way too many tools to list here, but `pwntools` is a great framework that is used in most challenges.

Thatt's most of the tools you'll use in CTFs. Try them out on picoCTF challenges! 

## Exercises

**PicoCTF:** Try out some of the 200-300 point questions! 

**NATAS:** Try to get to level 14!

**Bandit:** Keep working on Bandit. It's okay if you don't get very far! The challenges aren't too frequent on CTFs anyways, but they help build foundational skills.
