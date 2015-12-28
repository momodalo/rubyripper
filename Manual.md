# Introduction #

With each new release some new options appear in Rubyripper. All options are set to reasonable defaults. The aim of this wiki page is to document all options and to provide some arguments for which to choose. The config options are explained according to the tabs they're displayed. Note that for the actual ripping cdparanoia is used.

# Secure ripping #

**Cdrom device**
This is the device that is passed to cdparanoia for ripping. Normally this is configured to the default cdrom device. If your device is not auto detected, please file a bug report. When you have multiple cdrom drives you can change this setting to use the other drive. Look for your OS documentation where the other drive might be located.

**Cdrom offset**
In an ideal world, cdrom devices would be very accurate. So when you tell them to rip sector 4 and 5 you will exactly get the right results. However, often drives will have a slight inaccuracy. This can be corrected by providing the offset to cdparanoia. There is a link provided where you can find the offsets for different drives. The drivename of your drive is always provided in the logfile. It can also be found with -> cdparanoia -vQ.

**Match all chunks**
The amount of times that all sectors (aka chunks) will be matched. This is the minimum amount of the times each track is ripped. All sectors will be compared to the other rips. It can't be set lower than 2. If you don't want to use the test & copy feature, use another ripper.

**Match erronous chunks**
In the matching of all sectors there may be some sectors that have differences between the different rips. Rubyripper rips the track for a new trial until the track is matches at least the same amount of times as the rest of the sectors. You can optionally set it higher.

**Maximum trials**
Setting the maximum trials means the amount of times before Rubyripper gives up correcting. In some cases there can be no plausible match. To prevent endless looping it is advised to set this about 3 times higher than the previous setting. Also note that the more trials are used, the more likely Rubyripper will have a false succes. If there are two matches to be found in 12 trials, this doesn't necessarily mean it is truly repaired succesfully.

**Pass cdparanoia options**
You can provide all the options to cdparanoia that are available in cdparanoia -h. Notice that the cdrom drive and the offset are already passed. If your cdrom drive is very slow you might wanna add the -Z switch. You thereby turn off cdparanoia's extra protection, but you increase the speed quite nicely. By matching the different rips you have some protection anyway.

**Eject cd when finished**
After ripping your drive will spit out the disc. This is a nice feature, since you'll know that your rip is finished.

**Only keep logfile if correction is needed**
Some people thought it was usefull that a logfile should only be there when there were problems.

# TOC analysis #

**Create cuesheet**
A cuesheet is especially beneficial for single file rips. It provides the information needed to burn the file exactly like the original audio disc. It also accounts for pregaps, which may be nice for multiple file ripping as well. Notice that not all burning programs support cuesheets.

**Rip cd to single file**
Instead of a file for each track, you can get one file for the whole album. Depending on your audio player and your encoding format, this may be preferred. You are sure that there are no audible gaps between the tracks when playing. Especially mp3 seems to have problems with this. Other codecs work gapless, but your audio player needs to support it as well. The gaps can be especially frustrating with recordings of live concerts or discs which are meant to flow seamlessly from one track to the next.

**Rip hidden audio sectors before track 1**
Several discs have audio sectors that actually start before track 1. In a traditional cd-player you can rewind the first track until it starts counting negative. In most cases the audio is very short and only consists of garbage. In some rare discs there are complete hidden tracks of say 3 minutes.

By default the audio sectors are ripped if they are detected. This ensures making an exact copy of the original. However, certain drives do not support reading this section of the CD. Therefore cdparanoia might crash with specific drives when attempting to read these sectors. There are also known cases where the ripping is extremely slow and the output is total silence. So if your drive has problems please uncheck this option! All sectors will then be handled in the cue as a pregap instead.

**Mark as a hidden track when bigger than <??> seconds**
This option is only relevant for multiple file ripping and when ripping the hidden audio sectors before track 1. When marked a pregap it will be prepended to the first track. Otherwise the audio will be saved to an imaginary track 0.

**Append or preprend "pregaps" to a track (other than track 1)**
This option is only relevant for multiple file ripping. When appending pregaps to a previous track you have the advantage that when you open up a file it starts playing at the right position. Prepending to current track does not have this advantage, but it does allow for cuesheets conform official specification, where appending does not. Some burning applications might not support cuesheets where the gaps are appended to previous tracks.

**Pre-emphasis**
Pre-emphasis is a flag that tells the better cd-player to de-emphasise the audio to correct the recording. When pre-emphasis is detected on a track, you can correct the track. This is useful if you want to listen to it from your computer. When making an exact copy is preferred instead, saving the tag in the cuesheet should be your way to go.

# Codecs #
**Codec selection**
You can select as may codecs as you may like. This may be usefull as you use flac for archiving and mp3 for your mp3-player. Notice that tags are automatically passed to the supported codecs. If you select wav the output file of cdparanoia is just renamed to the filescheme.

**Flac settings**
You can pass the settings to flac as shown in flac -h. Defaults should be fine.

**Vorbis settings**
You can pass the settings to oggenc as shown in oggenc -h. Defaults should be fine.

**Lame mp3 settings**
You can pass the settings to lame as shown in lame --longhelp. Defaults should be fine.

**Other settings**
You can set the full command (including tags) here. The wildcards for artist, album, etcetera are shown when you click on the option: Show options for "Other". You don't need quotes around the variables as they're added automatically. An example command is: faac --artist %a --album %b --title %t --genre %g --track %n --year %y -o %o.aac %i

The '% letter' part is rubyripper, the switches will depend on the specific codec. You probably want to enter the right extension too after %o. You can find the needed switches for a specific encoder in a terminal with: "encoder -h" or "encoder --help" in most cases.

**Number of extra encoding threads**
The amount of extra processes that are started up for simultaneously encoding while ripping. You should normally set this to the amount of cores your cpu has. Notice that will take full use of your cpu. Depending on your OS this may hurt performance of other programs. The encoding commands are set with lowest priority though.

**Create m3u playlist**
Create a simple textfile with all the filenames in it. Most music players support this to load the whole album at once. M3u seems to suggest it's only for mp3, but other formats work just as well.

**Replace spaces with underscores in filenames**
This makes sure the filenames have no spaces in them. The tags are preserved. Some `*`nix users seem to advocate that spaces are an evil thing in filesystems.

**Downsize all capital letters in filenames**
This makes sure the filenames won't have capitals in them. The tags are preserved. Some `*`nix users seem to advocate that capitals are an evil thing in filesystems.

# Freedb #
**Enable freedb metadata fetching**
Get the metadata from the internet. Note that you probably need a helping utility like discid or cd-discid installed to have succes on identifying all discs. And then the disc needs to have a record in the freedb database as well.

**Always use first hit**
Often you find the same disc twice in the database. This option automatically chooses the first one. Most of the time this is the right one.

**Freedb server**
The freedb server that is used. You can also set this to the musicbrainz freedb emulation (http://freedb.musicbrainz.org:80/~cddb/cddb.cgi).

**Username**
Your username as required in the freedb protocol. I personally don't see the relevance for freedb to have this, so it's set to anonymous by default. You can change it if you like.

**Hostname**
Your hostname as required in the freedb protocol.

# Other #
**Base directory**
The output dir which is the basis for all output. It doesn't contain any wildcards. Together with the one of the other three schemes the output name is determined. Notice that if you select "freeze disc info" in the main window, a subdir CD## will be prepended to the file.

**Standard**
The standard filenaming schemes for the output files. You can find all wildcards explained at Show options for "Filenaming scheme".

**Various artists**
The filenaming scheme for various artists discs. You might want to add the artist to the filename where you wouldn't do so for normal discs. Also you can use the various artist %va wildcard to describe the collection of artists. For most discs this will be something like "Various Artists".

**Single file image**
The filenaming scheme for single file images. You might not want to include the track number, where you otherwise would. Besides, you probably want some extra disc info included in the filename.

**Log file viewer**
The log file viewer is automatically detected in most cases. If not you can set it here.

**File manager**
The filemanager is automatically detected in most cases. If not, you can set it here.

**Verbose mode**
Verbose mode prints extra info on the console window. You don't need to enable this.

**Debug mode**
Debug mode prints debug related info in the console window. Enable this when you encounter problems. The output in a console window might be very valuable to solve the problem.