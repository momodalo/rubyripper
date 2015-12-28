# Introduction #

Just a reminder to myself. A release will be made when there are enough changes that make it worthwile. Normally this will be about 4 times a year.

# Details #

  1. Fix any outstanding crashes or code a workaround.
  1. Set the version number.
  1. Remove any fuzzy messages from translations.
  1. Update the changelog in the README file.
  1. Make an archive with a release candidate.
  1. Send a mail to testers, translators, release-mailing-list with archive.
  1. Ask to test and report any findings.
  1. Ask to update the translations.
  1. Announce a release in 7-14 days.
  1. When ready, tag the release with git --tag v.0.X.X.

# Usefull things #

git archive --format tar --prefix rubyripper-version/ master | bzip2  > rubyripper-version.tar.bz2