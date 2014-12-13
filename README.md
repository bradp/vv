# Variable VVV - The Best VVV Site Wizard

	 ██    ██ ██    ██
	░██   ░██░██   ░██     Variable VVV 1.0.1
	░░██ ░██ ░░██ ░██
	 ░░████   ░░████       The easiest way to set up
	  ░░██     ░░██        WordPress sites with VVV!
	   ░░       ░░


```vv``` makes it extremely easy to create a new WordPress site using [Varying Vagrant Vagrants](https://github.com/Varying-Vagrant-Vagrants/VVV).


## Installation

If you have [Homebrew](http://brew.sh/) installed, you can do

	brew install bradp/vv/vv


Otherwise you'll want to clone and place in your $PATH somewhere.

## Updating

vv is currently under development, and you'll probably want the latest and greatest version at all time.
If installed with Homebrew, you can do `` brew upgrade vv`` to grab the latest tagged release. If you've cloned it down, a simple ``git pull origin master`` will get you rocking.

## Usage

Once installed, you can run ``vv`` anywhere you'd like. If vv can't automatically find your VVV installation, you will be prompted for the path. It will also save this into a configuration file in ```~/.vv-config```, so you won't be prompted again.

At any time, you can run ``vv`` or ``vv --help`` to see a list of all possible options and flags. For anything that requires flags, but they are not passed in, will prompt you for have the value.

Anything you do that you don't pass in required value as an argument will prompt you for it.

The main commands are ``list``, ``create``, ``delete``. These will list your sites, create a site, and delete a site. All of these have a few different aliases, so if you run ```vvv show```, vv will know you meant ```vvv list```.

To start creating a site, simply do ``vv create`` ( you can also do ```vv --create```, or simply ``vv -c``). You will then be prompted for all required options.

All options and flags are listed below.

## Site Creation

```vv create```

Creating a site does the following:

* Halts Vagrant (if running)
* Creates a web root for the site in the `www` folder containing three files: `vvv-init.sh`, `wp-cli.yml`, and `vvv-hosts`
	* `vvv-init.sh` tells Vagrant to create a database if one does not exist and install the latest version of WordPress (via WP-CLI) the next time Vagrant is provisioned
	* `wp-cli.yml` tells WP-CLI that WordPress is in the htdocs folder
	* `vvv-hosts` contains the hosts entry to give your site a nice custom domain (the domain is set in the wizard)
* Creates a file in the `nginx-config` folder to handle server settings for your site
* Restarts Vagrant with `vagrant up --provision`

Provisioning Vagrant takes a couple of minutes, but this is a crucial step as it downloads WordPress into your site's htdocs directory and runs the installation. If you want to skip provisioning and install WordPress manually, you can run the new site's `vvv-init.sh` file directly in the Vagrant shell.

## Site Deletion

```vv delete```

Deleting a site does the following:

* Halts Vagrant (if running)
* Deletes the site's web root (which deletes the `vvv-init.sh`, `wp-cli.yml`, and `vvv-hosts` files as well)
* Deletes the file in the `nginx-config` folder pertaining to the site

Note that it does not delete the site's database.

## Deployments

```vv --deployment-create```

vv supports setting up deployments that work with [Vagrant Push](https://docs.vagrantup.com/v2/push/index.html). You'll need to be on version 1.7.0 or later of Vagrant. Simply run ```vv --deployment-create``` and walk through the wizard.

To deploy a site, you can do ```vvv --vagrant push <sitename><deployment_name>```.

When removing a deployment, your current Vagrantfile will be backed up as Vagrantfile-backup.

## Advanced Usage

Anything that vv prompts you for, you can pass in as an argument. Most of this is realized in the site creation. In fact, there are a few arguments you can pass in that aren't prompted. This gives you total control over creating a new site.

To create a new site named 'mysite' that has the domain 'mysite.dev' and is a multisite with subdomains, with WP_Debug turned on would be:

```vv -c -d mysite.dev -n mysite -m subdomains -x```

Or, the more readable version with all expanded flags.

```vv --create --domain mysite.dev --name mysite --multisite subdomains --debug```

### Vagrant Proxy ###

Because vv knows where you VVV installation is, you can run it from anywhere. vv will proxy any commands passed into ``vv --vagrant <command>`` to your VVV location. So ``vv --vagrant halt`` will halt your VVV vagrant, no matter where you run it.

###Options###

|Option |Description|
|------|-----------
|``--help``, ``-h``| Show help and usage|
|``--version``|Show current vv version number.|
|``--about``|Show about screen.|
| |
|``--list``,	``-l``, ``list``|List all VVV sites|
|``--create``, ``-c``, ``create``|Create a new site|
|``--remove``, ``-r``, ``remove``|Remove a site|
|``--deployment-create``|Set up deployment for a site|
|``--deployment-remove``|Remove deployment for a site|
|``--vagrant``, ``-v``|Pass vagrant command through to VVV.|
|``--path``,	``-p``|Path to VVV installation|
|``--force_path``, ``-fp``|Override vv auto-VVV locating|


###Options for Site Creation###

|Option |Description|
|------|-----------
|``--domain, -d``|Domain of new site|
|``--live_url``, ``-u``|Live URL of site|
|``--files``, ``-f``|Do not provision Vagrant, just create the site directory and files|
|``--images``, ``-i``|Load images by proxy from the live site|
|``--name``, ``-n``|Desired name for the site directory (e.g. mysite)|
|``--wp_version``, ``-wv``|Version of WordPress to install|
|``--debug``, ``-x``|Turn on WP_DEBUG and WP_DEBUG_LOG|
|``--multisite``, ``-m``|Install as a multisite|
|``--username``|Admin username|
|``--password``|Admin password|
|``--email``|Admin email|
|``--git_repo``|Git repo to clone as wp-content|
|``--path``,	``-p``|Path to VVV installation|
|``--force_path``, ``-fp``|Override vv auto-VVV locating|


###Options for Site Removal###
|Option |Description|
|------|-----------
|``--name``, ``-n``|Desired name for the site directory (e.g. mysite)|
|``--path``,	``-p``|Path to VVV installation|
|``--force_path``, ``-fp``|Override vv auto-VVV locating|

###Options for Deployment Setup###
|Option |Description|
|------|-----------
|``--name``, ``-n``|Desired name for the site directory (e.g. mysite)|
|``--deployment-name``|Name of deployment (production, staging, other, etc)|
|``--host``|Host (if SFTP, define port as host:port) |
|``--username``|FTP Username |
|``--password``|FTP Password  |
|``--passive``|Use Passive transfer mode? (y/n)  |
|``--secure``|Use SFTP? (y/n) |
|``--destination``|Destination path ( You probably want / or ~/public_html ) |
|``--confirm-removal``|Used when removing a deployment to skip the confirmation prompt |


## .vv-config ##

The first time you run ``vv``, it will attempt to locate your VVV installation location. If it can't find it, you will be prompted for it. This will be written to a .vv-config file in your home directory. (``~/.vv-config``) You can also edit this file if you need to change your VVV path.

In the future, more settings and defaults will be stored here, but for now, it is just the path.

## Questions?

Ping me on Twitter at [@bradparbs](http://twitter.com/bradparbs).

## Thanks

Forked and based off of [vvv-site-wizard from Alison Barrett](https://github.com/aliso/vvv-site-wizard).

## Change Log

#### 1.0.1 - *2014-12-12* ####
 Removed version checking, as it was throwing errors.

#### 1.0.0 - *2014-12-12* ####
 Initial documented, stable release.

#### 0.1.0 - *2014-12-11* ####
 Initial release.
