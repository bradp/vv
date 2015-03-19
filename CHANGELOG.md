## Change Log

#### 1.7.1 - *2015-3-17* ####
 * Fixed deployment creation bug where push.dir was not defined
 * Created new blueprint structure
 * Added new blueprint installation methods

#### 1.7.1 - *2015-3-17* ####
 * Fixed bug where default themes and plugins were sometimes removed when they shouldn't be.

#### 1.7.0 - *2015-3-15* ####
 * Allow vv list to work with sites in subfolders
 * Cleaned up and fix licensing terms and information
 * Added experimental support for non vvv-providers, with the combination of -fp and -fsf
 * Added the option to create a blank VVV site with a DB.
 * Added ability to remove default themes and plugins when creating a new site.
 * Added xip.io support to all created sites
 * Clarified bluepring usage when setting up a site.
 * Clarified deployment removal for site
 * Sanitization & shellcheck fixes

#### 1.6.0 - *2015-2-2* ####
 * Fix issue with passing in custom admin user/pass
 * Adds ability to import a local database export.
 * Add ability to set up a WordPress Skeleton style installation
 * Add --blank paramater to create blank VVV site, with no WordPress
 * Add --defaults command to accept all default options in site creation
 * Fix placeholder import process
 * Replace old method of image proxying
 * Fix color output to look a bit better
 * Fix deployment creation
 * Add check for curl
 * Add check for tput

#### 1.5.0 - *2015-1-5* ####
 * Tons of cleanup, bug fixes, and standardization. Tons of props to @creativecoder.

#### 1.4.6 - *2014-12-15* ####
 * Fix git repo setup
 Fix brew update procedure

#### 1.4.5 - *2014-12-15* ####
 * Fixes deployment setup

#### 1.4.4 - *2014-12-15* ####
 * Exclude wp-config.php when doing a deployment
 * update readme to clarify git repo usage
 * Fix order of output in vvv-init.sh
 * Add note about auto-update disabling to vv-config section of readme
 * Make headings consistent, & represent proper hierarchy, & update outdated info.
 * Doc Tweaks. Make headings consistent, and represent proper hierarchy, and update outdated info.

#### 1.5.0 - *2015-1-5* ####
 * Tons of cleanup, bug fixes, and standardization. Tons of props to @creativecoder.

#### 1.4.3 - *2014-12-14* ####
 * Fix blueprint breaking site creation.

#### 1.4.2 - *2014-12-14* ####
 * Fix extra info being output on all commands.

#### 1.4.1 - *2014-12-14* ####
 * Fix issue with update procedure when installed with brew.
 * Added flag to force update.

#### 1.4.0 - *2014-12-14* ####
 * Adds blueprints for site creation.

#### 1.3.1 - *2014-12-13* ####
 * Fixes bug in site creation.

#### 1.3.0 - *2014-12-13* ####
 Adds sample content import to new site.
 Fixes bugs in site database creation.

#### 1.2.0 - *2014-12-13* ####
 Adds auto-update functionality.

#### 1.1.0 - *2014-12-13* ####
 Add deployment configuration using Vagrant push.

#### 1.0.1 - *2014-12-12* ####
 Removed version checking, as it was throwing errors.

#### 1.0.0 - *2014-12-12* ####
 Initial documented, stable release.

#### 0.1.0 - *2014-12-11* ####
 Initial release.
