# New in v07 #
  * All commands will now be send base64 encoded. So you can use quotes as much as you want.
  * php://input detection is now 100% reliable. (it produced some false positives befor)
  * You can now define a POST string for relative and absolute files in the config.py.
  * Two placeholders can be used for the POST- and the find-string.
    * `__PHP_QUIZ__` which will generate a little random PHP testing code.
    * `__PHP_ANSWER__` which is the answer of the PHP testing code.
  * Experimental blindmode implemented. It will try to get the path with
    * "/.."
    * "/../.."
    * "/../../.."
    * ...
> Also known as monkey mode. It will only try blindly if the default mode failed and you have enabled it with `--enable-blind`. This mode will cause a lots of request!
  * TTL implemented. You can define it with `--ttl <seconds>`. Default is 30 seconds.
  * Experimental HTTP Proxy support. You can define a HTTP(s) proxy with `--http-proxy localhost:8080`.
  * Show-my-ip added. Use `--show-my-ip` if you want to see your current Internet-IP, country and User-Agent. Useful to test your proxy or VPN!
  * Googlescanner can now skip the first X pages. Use `--skip-pages X`.
  * Exploit mode will now extract the first time you connect to a server the kernel version and store it.
> Next time you start the exploit mode, the kernel version will be printed right after the domain name.
  * Lot's of bugfixes and additional regular expressions.