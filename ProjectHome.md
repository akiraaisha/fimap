# Welcome to the fimap project! #
<img src='http://tha-imax.de/~imax/fimap_bigger.jpg' width='400' height='200'>

fimap is a little python tool which can find, prepare, audit, exploit and even google automaticly for local and remote file inclusion bugs in webapps. fimap should be something like <a href='http://sqlmap.sourceforge.net'>sqlmap</a> just for LFI/RFI bugs instead of sql injection.<br>
It's currently under heavy development but it's usable.<br>
<br>
The goal of fimap is to improve the quality and security of <b>your</b> website.<br>
<br>
<b>Do not use this tool on servers where you don't have permission to pentest!</b>

I am dead serious.<br>
<br>
<br>
<br>
<hr />

I'm trying twitter right now to announce cool SVN updates.<br>
<br>
Feel free to follow: <a href='http://twitter.com/fimap'>http://twitter.com/fimap</a>

If you don't like twitter like me then keep watching the Quick News below :)<br>
<br>
<h2>Quick News for SVN and upcoming versions</h2>
<ul><li><del>Bing searching module implemented in SVN!</del> Currently broken :-O<br>
</li><li>SSH-Logfiles can now be scanned and exploited through SSH username!<br>
</li><li>You can now define which target to exploit and execute shell commands without the interactive exploit interface! (FimapNonInteractiveExec)<br>
</li><li>New experimental fallback plugin which you can try when just /etc/passwd (or any other only-readable file was found. (FimapPhpInfoExploit)<br>
</li><li>New fallback plugin for windows victims! (FimapFindFirstFileExploit)</li></ul>

<h2>What works currently?</h2>
<ul><li>Check a Single URL, List of URLs, or Google results fully automaticly.<br>
</li><li>Can identify and exploit file inclusion bugs.<br>
<ul><li>Relative\Absolute Path Handling.<br>
</li><li>Tries automaticly to eleminate suffixes with Nullbyte and other methods like Dot-Truncation.<br>
</li><li>Remotefile Injection.<br>
</li><li>Logfile Injection. (FimapLogInjection)<br>
</li></ul></li><li>Test and exploit multiple bugs:<br>
<ul><li>include()<br>
</li><li>include_once()<br>
</li><li>require()<br>
</li><li>require_once()<br>
</li></ul></li><li>You always define absolute pathnames in the configs. No monkey like redundant pathes like:<br>
<ul><li>../etc/passwd<br>
</li><li>../../etc/passwd<br>
</li><li>../../../etc/passwd<br>
</li></ul></li><li>Has a Blind Mode (--enable-blind) for cases when the server has disabled error messages. BlindMode<br>
</li><li>Has an interactive exploit mode which...<br>
<ul><li>...can spawn a shell on vulnerable systems.<br>
</li><li>...can spawn a reverse shell on vulnerable systems.<br>
</li><li>...can do everything you have added in your <i>payload-dict</i> inside the <i>config.py</i>
</li></ul></li><li>Add your own payloads and pathes to the config.py file.<br>
</li><li>Has a Harvest mode which can collect URLs from a given domain for later pentesting.<br>
</li><li>Goto FimapHelpPage for all features.<br>
</li><li>Works also on windows.<br>
</li><li>Can handle directories in RFI mode like:<br>
<ul><li><code>&lt;? include ($_GET["inc"] . "/content/index.html"); ?&gt;</code>
</li><li><code>&lt;? include ($_GET["inc"] . "_lang/index.html"); ?&gt;</code>
</li><li>where Null-Byte is not possible.<br>
</li></ul></li><li>Can use proxys.<br>
</li><li>Scans and exploits GET, POST and Cookies.<br>
</li><li>Has a very small footprint. (No senseless bruteforcing of pathes - unless you need it.)<br>
</li><li>Can attack also windows servers! (WindowsAttack)<br>
</li><li>Has a tiny plugin interface for writing exploitmode plugins (PluginDevelopment)<br>
<ul><li>Check out the PHPInfo() Exploit plugin: FimapPhpInfoExploit<br>
</li></ul></li><li>Non Interactive Exploiting (FimapNonInteractiveExec)</li></ul>

<h2>What doesn't work yet?</h2>
<ul><li>Other languages than PHP (even if engine is ready for others as well.)</li></ul>

<h2>Where can I see some examples?</h2>
<ul><li>Goto FimapExampleRuns</li></ul>

<h2>Whats the quickest way to get fimap running on my machine?</h2>
<ul><li>Goto <a href='http://code.google.com/p/fimap/downloads/list'>Download Page</a>
</li><li>Click <a href='DownloadAndRunFimap.md'>here</a> if you prefer an SVN Snapshot.<br>
</li><li>If you have <a href='http://www.backtrack-linux.org/'>BackTrack</a> you have it already! (/pentest/web/fimap)</li></ul>

<h2>Where is the FAQ?</h2>
<ul><li>Goto FrequentlyAskedQuestions</li></ul>

<h2>What's coming next?</h2>
<ul><li>Goto WorkInProgress</li></ul>

<h2>Is there a How To?</h2>
<ul><li>Check out <a href='http://kaoticcreations.blogspot.com/2011/08/automated-lfirfi-scanning-exploiting.html'>this</a> post by HR from <a href='http://kaoticcreations.blogspot.com'>Kaotic Creations</a> which explains fimap really good :) It's a tutorial for windows but I think unix heads should understand it as well.</li></ul>

<h2>Other Stuff</h2>
<wiki:gadget url="http://www.ohloh.net/p/427707/widgets/project_languages.xml" border="0" width=450 height=250/><br>
<br>
<h2>Credits</h2>
<ul><li>Main Developer: <a href='mailto:fimap.dev@gmail.com'>Iman Karim</a></li></ul>

<ul><li>Trusted Plugins:<br>
<ul><li>Metasploit binding by <a href='mailto:xavi.garcia(atom)gmail(dot)com'>Xavier Garcia</a>
</li><li>Weevily Injector by <a href='mailto:infodox(atom)insecurety(dot)net'>Darren "Infodox" Martyn</a> from <a href='http://insecurety.net/'>http://insecurety.net/</a>
</li><li>AES Reverse Shell by <a href='mailto:infodox(atom)insecurety(dot)net'>Darren "Infodox" Martyn</a> from <a href='http://insecurety.net/'>http://insecurety.net/</a>
</li></ul></li><li>Additional thanks goes out to:<br>
<ul><li>Peteris Krumins for <a href='http://www.catonmat.net/blog/python-library-for-google-search/'>xgoogle</a> python module.<br>
</li><li>Pentestmonkey for <a href='http://pentestmonkey.net/tools/php-reverse-shell/'>php-reverse-shell</a>.<br>
</li><li>Crummy for <a href='http://www.crummy.com/software/BeautifulSoup/'>BeautifulSoup</a>.<br>
</li><li>Zeth0 from <a href='http://commandline.org.uk/'>commandline.org.uk</a> for ssh.py.<br>
</li></ul></li><li>Also thanks to:<br>
<ul><li>The <a href='http://python.org'>Python</a> Project<br>
</li><li>The <a href='http://eclipse.org'>Eclipse</a> Project<br>
</li><li>The <a href='http://netbeans.org'>Netbeans</a> Project</li></ul></li></ul>

<hr />

<h2>Tools and Sites I really like</h2>
<ul><li><a href='http://aluigi.org'>http://aluigi.org</a> Luigi Auriemma<br>
</li><li><a href='http://debian.org'>http://debian.org</a> Debian<br>
</li><li><a href='http://sikuli.org'>http://sikuli.org</a> Sikuli<br>
</li><li><a href='http://eu.battle.net/sc2/en'>http://eu.battle.net/sc2/en</a> Starcraft 2 - I really like Starcraft :)<br>
</li><li><a href='http://sqlmap.sourceforge.net'>http://sqlmap.sourceforge.net</a> sqlmap<br>
</li><li><a href='http://yakuake.kde.org'>http://yakuake.kde.org</a> Yakuake<br>
</li><li><a href='http://virtualbox.org'>http://virtualbox.org</a> Virtual Box</li></ul>


<h2>Links to Friends</h2>
<ul><li>Very good music by Dextrous aka. Duckstrous! Check it out and give him love! <a href='http://www.duckstrous.com'>http://www.duckstrous.com</a>