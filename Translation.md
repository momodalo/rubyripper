# Introduction #
  * You can also translate Rubyripper to your language!
  * You just need to have reasonable knowledge of English

# Gettext #
  * Rubyripper is translated with help of the gettext library
  * Gettext works with a translation source template (.pot)
  * With the template you can create a specific translation source file (.po)
  * To see the translation you need to generate the binary translation files (.mo) from latest po files.
  * Some tools are included to easily update the po files. Rubyripper supports these commands via the configure script: `./configure --help`.
  * Messages that are only slightly changed are marked as "fuzzy".

# How to start? #
  * Make sure to get latest source code
  * Switch to either the stable or the master branch
  * Update the po files.

See the [Git](Git.md) wikipage for details.

## For new translations ##
Create a subdirectory with your language code in the po dir. For example in master branch: `mkdir po/nl` for Dutch translation.
  * Create the specific source file `LANG=nl_NL msginit -i rubyripper.pot -o nl/rubyripper.po`. Replace the nl\_NL/nl thing with the letters for your language.
  * Some programs like Poedit can do this for you automatically.

## Updating translations ##
  * See the [Git](Git.md) wikipage.

# Editing po files using Poedit #
It is recommended to use the program Poedit. It should be available in most distros. In the file menu, you can select new catalogue from POT-file. All files are encoded in UTF-8, so select this as well. When you need to give a name for your po file, name it rubyripper.po.

## Start translation ##
In the first column is the original listed, in the second column the translation. When clicked on a row, the message will show on the lower part of the screen. You can enter the translation in the lowest part. You go through the different sentences with Cntr-down and Ctrl-up. It may be handy to first copy the text, then translate it.

Any value like %s should stay intact. They will be replaced with some variable. Make sure not to forget spaces and newlines (\n).

# Getting it merged #
Open up a new issue, announce your translation and the branch it's for and attach your created po file.