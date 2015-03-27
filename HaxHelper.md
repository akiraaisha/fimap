# Introduction #

An Overview about the HaxHelper class for plugin developers.

# Details #

As you have seen, your callback method will get the HaxHelper as parameter.
This class unions all important functions for plugin developers and wraps them into an easy to use class.
The following functions are available in the HaxHelper.

# Functions #

## HaxHelper.executeSystemCommand(command) ##
Execute a system command on the vulnerable system.
### Input ###
  * command: The system command you want to execute.
### Output ###
  * Returns a String which contains it's result if all OK.
  * False if we can't inject system commands.
  * None if something went wrong.

## HaxHelper.executeCode(code) ##
Execute interpreted language code. This function allows you to inject code.
### Input ###
  * code: The code you want to execute. This is not for system commands - it's for php\asp\perl...
### Output ###
  * Returns the (filtered) result-text as string.

## HaxHelper.isUnix() ##
### Input ###
_None_
### Output ###
  * Returns True if the vulnerable machine is a unix box. Otherwise False.


## HaxHelper.isWindows() ##
### Input ###
_None_
### Output ###
  * Returns True if the vulnerable machine is a windows box. Otherwise False.

## HaxHelper.getLangName() ##
### Input ###
_None_
### Output ###
  * Returns the language name of the vulnerable script as lowercased String.

## HaxHelper.canExecuteSystemCommands() ##
### Input ###
_None_
### Output ###
  * Returns True if we are able to execute system commands. Otherwise False.

## HaxHelper.concatCommands(commands) ##
### Input ###
  * commands: A array of system commands you want to concat. fimap will concat them exactly how the OS needs it. (In unix with ; in windows with &  -- Editable in the generic.xml)
### Output ###
  * Returns a ready to go system command as String.

## HaxHelper.getPWDCommand() ##
### Input ###
_None_
### Output ###
  * Returns a `pwd` command for the vulnerable server.

## HaxHelper.getPWD() ##
### Input ###
_None_
### Output ###
  * Returns the actual result of `pwd` on the remote machine.


## HaxHelper.getUsernameCommand() ##
### Input ###
_None_
### Output ###
  * Returns a `whoami` command for the vulnerable server.

## HaxHelper.getConcatSymbol() ##
### Input ###
_None_
### Output ###
  * Returns the concat symbol which is correct for the server.

## HaxHelper.generateChangeDirectoryCommand(newdir) ##
### Input ###
  * newdir: The new directory you want to change to.
### Output ###
  * Returns a system-code to change the directory.


## HaxHelper.getUNAMECommand() ##
### Input ###
_None_
### Output ###
  * Returns a system-command which tells us the kernel version.

## HaxHelper.uploadfile(localfile, remotefile, chunksize=1024) ##
### Input ###
  * localfile: The absolute path of the file you want to send.
  * remotefile: The absolute path where the file should be copied to.
  * chunksize: The bytes to send per request. Set it to -1 to send the whole file in one request.
### Output ###
  * Returns 0 if an error occured. Else you will receive the bytes which have been written.

# Some Examples #
#### Execute a System Command ####
```
if (haxhelper.isUnix()):
    haxhelper.executeSystemCommand("echo 'We are in unix!'")
elif (haxhelper.isWindows()):
    haxhelper.executeSystemCommand("echo We are in windows!")
else:
    pass # This should never happen.
```
#### Concat Unix Commands ####
```
print haxhelper.concatCommands(("uname -a", "whoiam"))
> uname -a ; whoiam
```

#### Concat Windows Commands ####
```
print haxhelper.concatCommands(("ver", "echo %USERNAME%"))
> ver & echo %USERNAME%
```

#### Same as above just OS-Independent ####
```
uname_cmd = haxhelper.getUNAMECommand()
whoami_cmd = haxhelper.getUsernameCommand()
print haxhelper.concatCommands((uname_cmd, whoami_cmd))
```

#### Execute PHP code ####
```
if (haxhelper.getLangName() == "php"):
    phpinfo = haxhelper.executeCode("<?php phpinfo(); ?>")
else:
    print "This is not PHP!"
```

#### Write a file ####
```
bytes = haxhelper.uploadfile("/tmp/supercode.txt", "/tmp/supercode.sh", -1)
print "%d bytes written!" %(bytes)
```