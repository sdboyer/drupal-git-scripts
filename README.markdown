# drupal-git-scripts #

This set of scripts allows Drupal developers full interoperation between an 
all-git local environment and Drupal's CVS repositories. "All-git environment"
means that you can create a full drupal instance by cloning off of the git 
repositories created by this script. Core, contrib, everything.
"Interoperation" means that your local repositories can chase very closely
after CVS commits made in contrib, and seamlessly integrate those into the
environment you've created using standard git fetch/merge type operations.

While these scripts can handle core, the repo generated will differ from the
semi-canonical git mirror of core (http://github.com/drupal/drupal); these 
scripts strip CVS keywords in order to make CVS interoperation cleaner, but
that mirror does not. This results in differing commit IDs. So you may want
to use that mirror for core, instead.

## Initial Setup ##

First step is configuring the drupal_sync.conf file, which will need to be
placed at /etc/drupal_sync.conf. If you already have a local rsync'd copy
of Drupal CVS on your system, make sure to set CVSSRV to the base of that
CVS repository (i.e., to the parent directory containing the CVSROOT dir).
Details on setting up an rsync'd local CVS mirror, can be found at
http://drupal.org/node/277268, if needed.

Once your drupal_sync.conf file is appropriately placed, simply run the
included drupal_sync script with the argument 'all':

    $ drupal_sync all

This will update your local mirror, then build all the local git repositories.
Bare repositories will be built and placed at:

    # Contrib
    $GITSRV/contrib/<modulename>.git
    # Core
    $GITSRV/drupal/drupal.git

## Requirements ##

These scripts require rsync, cvs, cvsps, git, find, grep, sed. Nothin fancy.
