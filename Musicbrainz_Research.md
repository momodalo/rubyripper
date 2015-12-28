# Introduction #

Musicbrainz is an alternative provider for metadata of audiodiscs. Since it's actively developed and has a more advanced design than freedb, some users prefer to let rubyripper use it. However, before implementing such a standard I need some information first. Please help to provide this.

# What info to feed freedb #
Freedb needs the freedb\_id, the amount of tracks and the startsector for each track. The freedb\_id can be calculated from the TOC (Table of contents) from an audio disc. There are some help programs who can calculate the freedb\_id, like cd-discid.

# What info to feed musicbrainz #

To identify a disc to musicbrainz you need [libdiscid](http://musicbrainz.org/doc/libdiscid) libdiscid is a C library for creating MusicBrainz DiscIDs from audio CDs. It reads a CD's table of contents (TOC) and generates an identifier which can be used to lookup the CD at MusicBrainz. Additionally, it provides a submission URL for adding the DiscID to the database. (tip recieved by Muz_on the IRC)_

# Musicbrainz communication protocol #
You can connect over http / a socket / whatever?

# Relevant links #
  * http://musicbrainz.org/ (official site)

  * http://rbrainz.rubyforge.org/ (ruby example implementation)

  * [libmusicbrainz](http://musicbrainz.org/doc/libmusicbrainz) (The libmusicbrainz (also known as mb\_client or [MusicBrainz](http://musicbrainz.org/doc/MusicBrainz) Client Library) is a development library geared towards developers who wish to add [MusicBrainz](http://musicbrainz.org/doc/MusicBrainz) lookup capabilities to their applications.)

# Contact #

[Mailing Lists](http://wiki.musicbrainz.org/Mailing_List)

Server: irc.freenode.net
Channel: #musicbrainz

There is a weekly dev chat held every Monday in the #musicbrainz-devel channel that takes about an hour. It usually starts at 8pm UK, 9pm mainland Europe, 3pm EST or noon PST. An invitation is usually sent out to the [Developers Mailing List](http://wiki.musicbrainz.org/Developers_Mailing_List) Sunday night/Monday morning.