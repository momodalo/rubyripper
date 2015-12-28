# Introduction #

Subversion lets one or multiple developers organize a central repository where changes are managed. With each 'commit' (change) a diff will be created against the previous revision. When hunting down some bugs, it can be usefull to get the latest revision to see if it fixes your particular problem. Due to the scripting characteristic of ruby you do not have to install it on your system just to run rubyripper!

Here follows the commands you have to run in a terminal/konsole. The chosen directories are just an example. And of course you **need to install subversion** before doing this!

# Initial checkout #

  * cd $HOME
  * svn checkout http://rubyripper.googlecode.com/svn/trunk/ rubyripper-svn

# Update existing repository #

  * cd $HOME/rubyripper-svn
  * svn update

# Create / update language files (optional) #

Make sure you've installed the dependency list in the README file

  * cd $HOME/rubyripper-svn
  * ./configure --update-lang

# Run rubyripper #

Make sure you've installed the dependency list in the README file

  * cd $HOME/rubyripper-svn
  * ./rubyripper\_gtk2.rb
or
  * ./rubyripper\_cli.rb