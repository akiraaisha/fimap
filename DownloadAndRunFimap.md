# Introduction #

Ways to get fimap running.
You will need Python 2.6.

# Details #

## Downloading official release ##
Goto the [Download page](http://code.google.com/p/fimap/downloads/list).

## Downloading SVN snapshot ##
Follow this steps:
  1. If you haven't installed subversion yet, do it now:
> > `sudo apt-get install subversion # debian\ubuntu way`
  1. Goto your directory you want to download it.
> > `cd ~`
  1. Checkout the code:
> > `svn checkout http://fimap.googlecode.com/svn/trunk/ fimap`
  1. Change to the fimap directory and make it executable.
```
cd fimap/src
chmod +x fimap.py
```
  1. Run fimap.
> > `./fimap.py -h`

## Configuring (optional) ##
fimap is configured not bad at the moment.
However - You can add additional pathes and payloads without messing around with the code.
Another reason to configure fimap is if you want to detect and exploit RFI exploits much better.
