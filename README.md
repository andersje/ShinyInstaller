ShinyInstaller
==============

Licensed under the GPLv3.
Copyright 2014 Andersand Corporation

a pair of shell scripts to install/remove zip'd R applications
to a shiny server.  Works equally well with open-source or 
payware version of shiny server.  
(details on shiny server at http://shiny.rstudio.com/articles/shiny-server.html)

You can find docs on how to use this tool, complete with screenshots,
in the docs/ directory

The docs in that directory were all polished by Matthew Sparby, from an 
ugly prototype I developed 

QUICKSTART
==========

== On Your Linux Server ==
 * create a group called "rinstallers"
 * Add everyone who will need to install R apps to that group
 * copy the file shiny.sudoers to /etc/sudoers.d
 * copy the files from scripts/ to /usr/local/bin/

== On your development box ==
 * Bundle your app into a zipfile (see below)
 * transfer zipfile to your shiny server
 * ssh to Linux Server
 * install:
     sudo /usr/local/bin/shinyinstall
 * load http://your.shiny.server:3838/YourApp/ in your browser
 * laugh maniacally

MORE EXPLANATION
================

R Applications need to be bundled into a zipfile of the proper format.
Create a directory with the same name as your application.  e.g. if your 
application is called RTaurusFinder (presumably an application to find
deals on classic 1980s-era Ford Taurus automobiles which are located in
close geographic proximity to some point), you want to create a folder called
RTaurusFinder.  Put all your stuff in there.

How do you actually build a Shiny app?
See: http://rstudio.github.io/shiny/tutorial/

Once you've got your files in that directory, zip it up.
Name your zipfile Appname.zip.  So, in the above example, you'd end up
with RTaurusFinder.zip

Transfer the zip file to the server.  Feel free to follow the directions
in the docs/ dir -- that'll walk you through sftp'ing things to the Linux 
box running shiny-server, assuming you're running some recent version of
MS Windows.  I currently have no docs for OSX or Linux clients, but pull
requests are welcome.

Log into the server.  You'll need a shell account on it.
Navigate to the directory with your zipfile

sudo /usr/local/bin/shinyinstall RTaurusFinder.zip

Once that's done, fire up your web browser and go to
http://your.shiny.server:3838/RTaurusFinder/

and you should see your app.

Good luck, and I hope this is useful.

Pull requests welcome

WHY
===

With a shiny-server, you've probably got developers wanting to try out new
versions of their app on something bigger than their current workstation.
Or, maybe you want them to throw their apps on the webserver so you've got
an idea of what libraries need to be installed.

This pair of scripts lets you delegate the installation and removal of those
apps.  Probably more valuably, it gives you a couple of generic documents to
hand to end users on how to sftp their data to the server, and actually run
the scripts.

I don't really recommend giving your devs admin authority on a prod box --
and that's what these scripts will give them.  This is ideal for a trusted
userbase, in a dev or QA environment.  On your prod boxes, you'll want to
restrict who can run these scripts a bit more.
