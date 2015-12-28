# Introduction #

Since I, the developer, don't have much time available, it would help me much if all info of accurateRip is organized in a small overview. The thread of [issue 112](https://code.google.com/p/rubyripper/issues/detail?id=112) is actually getting quite large. If I am ever to implement the standard, a single point of information would be nice. I see a lot of questions popping up, so I've added a few sections. If you know some answers please contribute :)

# What is accurateRip #
accurateRip is a secure ripping scheme developed by the coders behind DBpoweramp.  In short it compares the sums of tracks ripped with a database of rips from other users, to verify an accurate rip.  To calculate the drive offset a key disc is needed, of which there are over 20,000.  accurateRip is also available to other ripping programs.  EAC is able to use a DLL to provide the functionality.

# License questions #

> Access to the AccurateRip database, using 3rd party applications (such as adopting open source access routines) requires prior agreement.
> Commercial usage of AccurateRip requires an AccurateRip commercial license, please email for details: http://www.dbpoweramp.com/email.htm

# Which features must Rubyripper support first #
Determination of drive offset semi-automatically

# Communication protocol with accurateRip server #

# How accurateRip handles gaps #
My understanding of gaps and accuraterip is that when calculating the disk ID it happens from the first sectors of the disk (therefore including pregaps/hidden tracks) and the final sectors of the disk (or last track). Then from there the gaps are appended to the tracks and calculated from there. However this is only from reading the other implementations, and these other implementations occasionally fail to calculate correctly. The best option would be to contact the accurateRip developer and request a use license and retrieve the relevant gap info from him/her.


# Other implementations (sample code) #

  * ARCue (Perl script or Visual C) http://www.hydrogenaudio.org/forums/lofiversion/index.php/t60440.html
  * ARFlac ([Perl](http://www.hydrogenaudio.org/forums/index.php?showtopic=62522) or [C](http://www.hydrogenaudio.org/forums/index.php?showtopic=61574))

# How to contact accurateRip developer(s) #

![http://www.dbpoweramp.com/images/misc/email.gif](http://www.dbpoweramp.com/images/misc/email.gif)

# Relevant Links #
[AccurateRip homepage](http://www.accuraterip.com)
[AccurateRip forum](http://forum.dbpoweramp.com/forumdisplay.php?f=54)
[3rd Party Access info](http://www.accuraterip.com/3rdparty-access.htm)