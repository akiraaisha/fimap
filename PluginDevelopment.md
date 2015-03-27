# Introduction #
If adding a payload is not enough, you can write a exploit-mode plugin
which can do advanced stuff on the vulnerable server.

This pages here will show you how to write a plugin for fimap.

Goal of the plugin is:
  * Adding our own handler for the exploit-mode.
  * Intercepting the callback and do whatever we want.

This howto will only work with the SVN version or the (future) release version 0.8.

# Let's go! #

## Creating the folder structure ##
If you take a look at the fimap directory, you will see a plugin folder.
This folder contains all the plugins.
Since we want to write a new one, we simply going to create a new folder.
In this example we are going to write a "Hello Shell!" plugin so let's create a folder named "hello\_shell". In this folder simply create your main class with the same name as the folder and a empty file called 'plugin.xml'.
Due technical reasons the plugin filename should be a valid python variable name which means no space or special characters.

So basicly we go to the plugin folder and ...
  * ... create a folder named `hello_shell`
  * ... create a file inside the folder named `hello_shell.py`
  * ... create a file inside the folder named `plugin.xml`
  * ... create an empty file inside the folder named `__init__.py`

```
  fimap
   |
   |-> plugins
        |
        |-> hello_shell
             |
             |-- __init__.py
             |-- hello_shell.py
             |-- plugin.xml
```


That's it! Your folder structure is ready!


## Filling the code with the basics ##
At first open your "plugin.xml" and paste this into it:
```
<?xml version="1.0" encoding="UTF-8"?>
<plugin 
		name="Hello Shell"
		startup="hello_shell" 
		version="1"
		autor="Iman Karim"
		email="fimap.dev@gmail.com"
		url="http://fimap.googlecode.com"
/>
```
The only non trivial value in this xml file is the `startup` value. This should be the the same like your directory name (and your main class name without .py).
That's it!

Now open your "hello\_shell.py" in your favorite editor and paste this:
```
from plugininterface import basePlugin

class hello_shell(basePlugin):
        
    def plugin_init(self):
        # This function is your `__init__` function.
        print "Plugin Init!"
        
    def plugin_loaded(self):
        # This function will be called if all plugins are loaded.
        pass
        
       
    def plugin_exploit_modes_requested(self, langClass, isSystem, isUnix):
        # This method will be called just befor the user gets the 'available attack' screen.
        # You can see that we get the 
        #     * langClass (which represents the current language of the script)
        #     * A boolean value 'isSystem' which tells us if we can inject system commands.
        #     * And another boolean 'isUnix' which will be true if it's a unix-like system and false if it's Windows.
        # We should return a array which contains tuples with a label and a unique callback string.
        ret = []

        # ADD YOUR PAYLOADS HERE.

        return(ret)
        
    def plugin_callback_handler(self, callbackstring, haxhelper):
        # This function will be launched if the user selected one of your attacks.
        # The two params you receive here are:
        #    * callbackstring - The string you have defined in plugin_exploit_modes_requested.
        #    * haxhelper - A little class which makes it very easy to send an injected command.
        pass
        
            
```


Well as you see it's easy to understand.
So let's go on and register our payload.

```
def plugin_exploit_modes_requested(self, langClass, isSystem, isUnix):
        ret = []

        if (isSystem): # Do we have shell access?
            # attack should be a tuple (Label, Callbackstring)
            attack = ("Hello Shell!", "hello_shell.sayhello")
            ret.append(attack)

        return(ret)
```

Here we go.
We have just added a new payload into the exploit menu.

When the user selects your payload, the _Callbackstring_ will be broadcasted to all plugins.

Let's go on and intercept the callback string.

```
def plugin_callback_handler(self, callbackstring, haxhelper):
    if (callbackstring == "hello_shell.sayhello"): # Is it our callback string?
        if (haxhelper.isUnix()):
            # We are in unix
            print haxhelper.executeSystemCommand("echo 'Hello Shell!'")
        else:
            # We are in windows
            print haxhelper.executeSystemCommand("echo Hello Shell!")
```

As you can see its really easy!




# Complete code #
## File: plugin.xml ##
```
<?xml version="1.0" encoding="UTF-8"?>
<plugin 
		name="Hello Shell"
		startup="hello_shell" 
		version="1"
		autor="Iman Karim"
		email="fimap.dev@gmail.com"
		url="http://fimap.googlecode.com"
/>
```

## File: hello\_shell.py ##
```
from plugininterface import basePlugin

class hello_shell(basePlugin):
        
    def plugin_init(self):
        # The Constructor of the plugin
        pass
    
    def plugin_loaded(self):
        # We dont need it for this example.
        pass

    def plugin_exploit_modes_requested(self, langClass, isSystem, isUnix):
        ret = []

        if (isSystem): # Do we have shell access?
            # attack will be a tuple (Label, Callbackstring)
            attack = ("Hello Shell!", "hello_shell.sayhello")
            ret.append(attack)

        return(ret)

    def plugin_callback_handler(self, callbackstring, haxhelper):
        if (callbackstring == "hello_shell.sayhello"): # Is it our callback string?
            if (haxhelper.isUnix()):
                # We are in unix
                print haxhelper.executeSystemCommand("echo 'Hello Shell!'")
            else:
                # We are in windows
                print haxhelper.executeSystemCommand("echo Hello Shell!")   

```

# Final words #
Check out the HaxHelper object for more information what you can do.