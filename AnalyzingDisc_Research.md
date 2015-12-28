# Introduction #

Currently much of the logic of analyzing a disc, including pregaps comes from
the overview that cdparanoia -Q provides. However, as some have noticed, the TOC
(Table of Contents) cdparanoia (or the disc?) reports isn't always that
reliable. I ask for help of those who know some information about reading the
real TOC. I know for example that Exact Audio Copy has a feature to detect the
real TOC (instead of the reported TOC). Special attention has to be there for
discs with a data track.

# Gap Handling techniques of EAC #
There are two options for handling gaps. Option one is append the gap to the previous track and option two is to prepend it to the next track. Each option is commonly used in certain situations. Option one, appending to the previous gap, is commonly used when the music file is stored on a computer, for example, in the form of a flac or aac file. Option two, prepending the gap to the next track, is commonly used when the track is on a CD, for example in the cue sheet it appears as INDEX 00.

I am proposing that all three methods be made available to rippers using rubyripper as each person has their own personal preference. Additionally please note these are only to do with multiple files, with single files it's different as there are no appending and prepending issues with local storage.

## Multiple files with gaps (Noncompliant) ##
http://wiki.hydrogenaudio.org/index.php?title=Cuesheet#Multiple_files_with_gaps_.28Noncompliant.29
Fortunately, there is a very tricky work around for cue sheets to convert between the two when burning a CD. This takes advantage of the fact that a cue sheet is simply a linear file, the burner simply burns what it's told, in the order it's told. Therefore it is very simple to create a cue sheet that moves the pregap from the end of the previous track over to the front INDEX 00 section of the next track, to do this before detailing the next file an INDEX 00 occurs, which the burner knows is the gap for the next track, but uses the end of the previous track (begining at the position detailed in INDEX 00) an example of this is on the wiki link.

Note that before file two is referenced track 2 is referenced and defined then INDEX 00 then the file then INDEX 01 at the beginning of file 2.

This method is the most common of the selected methods of EAC users, but unfortunately does not comply with cue sheet standards, therefore only burning programs that support this method (such as EAC and Burrrn) can burn these disks.

This method, being the most common method employed by rippers means that when verifying files ripped with AR the files will pass.

This method additionally requires every sector to be read from the CD, including the very first sectors (even if they are silence) this maintains a 1:1 copy of the CD.

## Multiple files with corrected gaps (Compliant) ##
http://wiki.hydrogenaudio.org/index.php?title=Cuesheet#Multiple_files_with_corrected_gaps
This method very simply involves the gap being prepended to the file stored on the computer and the CD. This, I believe, is the current method employed by rubyripper. This however is unsatisfactory because this will cause playback of songs to begin with a section of silence.

## Multiple files with gaps left out (Compliant) ##
http://wiki.hydrogenaudio.org/index.php?title=Cuesheet#Multiple_files_with_gaps_left_out
This method involves the gap not being stored on the computer files, and when burning occurs the PREGAP command is used to fill up these sections of time. Unfortunatly this causes poor rips due to the fact that a 1:1 copy of the CD is not maintained and these gaps are simply artificiality created by the ripping program.

# Reading the TOC with cdrdao #
Cdparanoia reads the basic TOC, but does in most cases not detect the pregaps
reliable. As reported in [issue 207](https://code.google.com/p/rubyripper/issues/detail?id=207) cdrdao can be used to detect the pregaps. It
is quite simple to parse the output of cdrdao. In my opinion the detection
should be made optional and be done just before the start of the actual ripping.
The reason is that it takes about 30 seconds to run the analysis of cdrdao.

The actual command is cdrdao read-toc --device /dev/cdrom output.toc. The device
should be read from the settings. The output location should be set to the
temporary dir + output.toc.

## Parsing the output of cdrdao ##
The output.toc file starts with the type of disc:
  1. **CD\_DA**, **CD\_ROM**, **CD\_ROM\_XA** Which stands for audio-only, audio+data, or a multi-session disc with audio+data.
  1. **CD\_TEXT** Metadata info about the artist. Not all drives can read this. It is mostly used on burned discs. See also [issue 316](https://code.google.com/p/rubyripper/issues/detail?id=316).
  1. **TITLE** Artist + Album name, seperated by multiple spaces.

For each track there is a line in the output like: "// Track 1". The lines
following give info about the track. Important for Rubyripper is to save the
following info:
  1. **TRACK AUDIO**, **TRACK DATA** This tells whether this is a audio or a data track
  1. **PRE\_EMPHASIS**, **NO PRE\_EMPHASIS** This tells whether this track has PRE\_EMPHASIS.
  1. **START** The amount of time the pregap takes (format mm:ss:##, where ## is the sector). Cdparanoia appends the pregap to the previous track.
  1. **SILENCE** This was reported in [issue 230](https://code.google.com/p/rubyripper/issues/detail?id=230). Cdparanoia doesn't allow to rip these sectors. Here we have a problem, because hidden tracks are also reported as SILENCE. Perhaps rubyripper should try and if failed skip this. In theory cdparanoia can read these sectors by simply using the argument `"[.0]-[.<sector before track 1's sector>]"`. **Assumption**: This only happens at the start of the disc.
  1. **TITLE** CD-text with the title of the track

# Technical info about pregaps and sortalike #
**Assumption**: Hidden tracks only occur at the start of the disc.

> The pregap on a Red Book audio CD is the portion of the audio track that precedes "index 01" for a given track in the table of contents (TOC). The pregap
("index 00") is typically two seconds long and usually, but not always, contains
silence. Popular uses for having the pregap contain audio are live CDs, track
interludes, and hidden songs in the pregap of the first track
http://en.wikipedia.org/wiki/Pregap

## PRE\_EMPHASIS ##
What is it? And how should it be handled?

> In processing electronic audio signals, preemphasis refers to a system process designed to increase, within a band of frequencies, the magnitude of some (usually higher) frequencies with respect to the magnitude of other (usually lower) frequencies in order to improve the overall signal-to-noise ratio by minimizing the adverse effects of such phenomena as attenuation distortion or saturation of recording media in subsequent parts of the system.

TL;DR: Preemphasis is a process where the amplitude of a selected band of frequencies (often higher) is increased in order to improve the signal-to-noise ratio by minimising the effects of attenuation distortion or saturation. The original signal is recreated by applying Deemphasis.
http://en.wikipedia.org/wiki/Preemphasis and http://cnyack.homestead.com/files/modulation/pre_emp.htm

# Pro's and cons for different ways to handle pregaps #
**Assumption**: Hidden tracks only occur at the start of the disc.
## Prepending pregaps to track ##
  * In rubyripper version 0.5.7 the hidden audio part was prepended to the first track. If I understand it well, cdparanoia doesn't show any pregaps after the first one. So in fact there the support for pregaps ended.

## Appending pregaps to previous track ##
  * In rubyripper version 0.5.7 all other gaps are appended to the previous track, since this is what cdparanoia shows. For cdparanoia the startsector of a track is "start previous track + length previous track + pregap current track". For track 1 this means after the hidden audio part / pregap.

## Use seperate files ##
  * This only seems to be needed when a hidden audio part exist at the start of the disc.

## Hidden tracks ##
  * Current method used in CD's. Most CD players will begin playing at the begining sector of track 1, to access the pregap, or hidden track you must rewind beyond track 1
  * Often the preferred way by most rippers (ie rip to track 00)
  * As noted in [issue 230](https://code.google.com/p/rubyripper/issues/detail?id=230) some drives fail to rip the pregap and instead use 100% CPU power in an endless loop. This seems to suggest that a hidden track shouldn't be ripped by default. Some suggested displaying track 0 at the interface. However since it depends on the drive and not on the disc, I like to propose it to be a configuration checkbox to rip sectors before track 1. It should be off by default. The option is only activated when using a cue sheet. When it is off, a correct cuesheet can still be build with the PREGAP option. When burned the burning application will add silence here.

## Hidden audio before first track <2 seconds ##
  * When there are sectors before track 1 it will depend on the length of the audio part to decide it's actions. If the audio part is smaller than 2 seconds, the audio is handled as pregap. If it's bigger then it is handled as a hidden track. As a result most discs with a hidden audio part will be handled as a pregap.
  * However a pregap of track 1 has to be handled a little different than other pregaps. Rubyripper needs to do three things (see also [issue 207](https://code.google.com/p/rubyripper/issues/detail?id=207)):
    1. the pregap sectors of track 1 never have to be ripped
    1. instead it should be added as PREGAP length in the cue file.
    1. all tracks should then determine their start position as if track 1 started at 00:00:00.

# Pregaps and image rips #

# Relevant links #
[Wikipedia Article on Pregaps](http://en.wikipedia.org/wiki/Pregap)

[Hydrogenaudio knowledge base on cuesheets](http://wiki.hydrogenaudio.org/index.php?title=Cuesheet)

# Tasks / Milestones #
  * Parse the cdrdao output < done >
  * Save the hidden audio sectors internally as track 0. Refactor the arrays to hashes to make this possible. < done >
  * Make single file rip work and build a correct cuesheet < done >
  * Make a new page for the gtk2 client where advanced toc options are shown < done >
  * Add an option to rip / not rip the audio part before track 1 < done >
  * Add an option how to handle pre-emphasis < done >
  * Documented all options in the gui < done >
  * Actually implement all TOC options < done >
  * Testing all new functionality < 0% >