# Introduction #

Git manages changes for the rubyripper project. With each 'commit' (change) a diff will be created against the previous revision.

# Usefull Git commands #
Make sure you first install git on your system!

  * Initial checkout: `git clone https://code.google.com/p/rubyripper/`. All further commands on this page assume you're in the rubyripper main dir.
  * Update rubyripper repository: `git pull`
  * Status rubyripper repository (including active branch): `git status`
  * Switch to master branch: `git checkout master`
  * Switch to stable branch: `git checkout stable`
  * See a graphical view of commits: `gitk`

Notice there also is a nice webview on the rubyripper site: http://code.google.com/p/rubyripper/source/list

# Running rubyripper without installing #
You should install needed dependencies first, see the README file.

## Master branch ##
  * First checkout master branch (git checkout master)
  * `./bin/rubyripper_cli` for the command line interface
  * `./bin/rubyripper_gtk2` for the graphical client.

### Update language files ###
  * All language input files are saved in "po" dir
  * Update the po files for latest code with `./configure --update-po`
  * Manually edit the po files or use a po editor
  * Update the mo files to see your translations with `./configure --update-mo`
  * Rerun the program to see the changes (you can also set a different lang with LANG="nl\_NL" for example).

## Stable branch ##
  * All language files are in the "locale/po" dir
  * First checkout stable branche (`git checkout stable`)
  * `./rubyripper_cli.rb` for the command line interface
  * `./rubyripper_gtk2.rb` for the graphical client.

### Update language files ###
  * To update po + mo files use `./configure --update-lang`
  * Manually edit the po files or use a po editor
  * To update po + mo files use `./configure --update-lang`

# Automatic tests (master branch only) #
One of the new features of rubyripper that it is restructured to have automatic testing as part of its design.

## Rspec unit tests ##
  * Unit tests are used for testing a single class in isolation.
  * All tests can be found in the "spec" dir
  * You can install rspec with rgem: `rgem install rspec`
  * You can run rspec with `rspec`

## Cucumber feature tests ##
  * Tests the program by simulating real users.
  * All feature tests can be found in the "features" dir
  * You can install cucumber with rgem: `rgem install cucumber`
  * You can run cucumber with `cucumber`

# Read more about git #

  * Official guide : http://www.kernel.org/pub/software/scm/git/docs/user-manual.html
  * Readable guide : http://www-cs-students.stanford.edu/~blynn/gitmagic/
  * Git community book: http://book.git-scm.com/