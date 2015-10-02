## Change Log

#### 1.9.0 - *DATE* ####

 * Add Hooks system for extensibility and modifications
 * Add SITENAME / SITEDOMAIN instructions to Blueprints
 * Add tab-completions in both Bash and ZSH
 * Allow installing trunk version of WordPress
 * Add folder creation to blank site set up
 * Remove database backups when removing a site with vv
 * Confirm VVV path when auto-grabbing it
 * Switch from '~' to $HOME for portablility
 * Add automatic Travis testing
 * General shell script clean up / security / sanity checks added.
 * Added --debug-vv flag for easier bug reporting.
 * Clean up multiple url handling code for vv-list
 * Allow for sourcing vv and leveraging code that way
 * README spelling fixings
 * Fix vv list breaking for more than 3 domains for a site
 * Allow overriding the error of site not existing for vv remove
 * Add ability to define the language to install WP with the --locale / --language flag
 * Load settings from vv-config just in bash, removing the need for python to be installed
 * When proxying images from a live site don't proxy uploaded images
 * If running creation for only files, don't halt vagrant before creating the files
 * Allow passing in site name directly to `vv remove`
 * Add `vv_internal_debug` to see exactly what code is running when.
 * Remove 2016 when removing defaults


#### 1.8.0 - *2015-7-25* ####
 * Adds flag to download a search/replace db tool
 * Add documentation around db prefix
 * Add db prefix option / flag
 * fix typo in unknown errorDate:
 * Pull from upstream / fix merge conflict
 * Formatting fixes
 * Add beginnings for tab-complete functionality
 * Add subdomain multisite installation instructions
 * Creates Roots.io Bedrock install
 * Adds bedrock to readme create commands
 * Adds installation of bedrock
 * Adds composer bedrock text to create_site_files
 * Adds help and arg case
 * Add windows install instuctions to readme
 * Adding *.domain support to subdomain networks
 * Making VV handle wildcard subdomains as VVV does per #94.
 * README Update - Custom Demo Content
 * Akismet typo
 * Output better version update debugging, and only run when github returns a real string
 * Update README to have correct version number


#### 1.7.2 - *2015-3-17* ####
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
