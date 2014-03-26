OS X Management
===============

A collection of little scripts used to manage Macs in our studios.


enrolme.sh
----------

Really simple bash script to fetch and install Trust and Enrolment profiles from a server, in the correct order.


powerman.pl
-----------

Power management script that ensures our Energy settings are maintained, but also dynamically shuts down systems depending upon how long they've been idle, whether there's still a user that seems to be present, and with variations for different studios.

The fairly insistent resetting of the Energy preferences is mainly a hangover from Mac OS X Tiger, when Energy settings seemed to be altered randomly. However, having this script running occasionally always keeps every system in perfect check, so I'm not changing my game plan.


Resources.app
-------------

Very straightforward AppleScript app which checks for the presence of a share, mounts it as Guest if it's missing, then opens a specific directory.


Store.app
---------

Slightly less straightforward AppleScript app which checks for the presence of a share, attempts to mount it (Finder will prompt for a password unless cached or in the user's Keychain) and then checks for the presence of the user's own storage directory.

If the storage directory is missing, a request is made via HTTP to the server, which will create one from a template with appropriate permissions. This directory is then opened as a new Finder window. If the directory already exists, it's just opened.


storefor
--------

This Bash script, PHP file and LaunchDaemon .plist make up the 'storefor' generator called by Store.app. The script is called every 10 seconds to check for new Store directory requests, whose need is indicated by a temp file generated by the HTTP call to the PHP file.

To install:

1. The com.studios.storefor.plist goes into /Library/LaunchDaemons - check the permissions are correct, then fire up with launchctl.
2. The storefor.php file goes into a suitable location to be served out by your webserver.
3. The storefor.sh script goes into /usr/local/bin.

Simple, but effective, and probably not massively secure. ;)

