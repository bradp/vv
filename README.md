# Variable VVV - The Best VVV Site Wizard

	 ██    ██ ██    ██
	░██   ░██░██   ░██     Variable VVV 1.12
	░░██ ░██ ░░██ ░██
	 ░░████   ░░████       The easiest way to set up
	  ░░██     ░░██        WordPress sites with VVV!
	   ░░       ░░


`vv` makes it extremely easy to create a new WordPress site using [Varying Vagrant Vagrants](https://github.com/Varying-Vagrant-Vagrants/VVV). `vv` supports site creation with many different options; site blueprints to set up all your plugins, themes, and more; deployments; and lots more features.

[![Travis](https://img.shields.io/travis/bradp/vv.svg)](https://travis-ci.org/bradp/vv)

*Tired of the time it takes to do a `vagrant provision` or create new sites?* Check out [flip](https://github.com/bradp/vvv-provision-flipper), a simple utility to solve that issue.

# Table of Contents

- [Installation](#installation)
  - [OS X Installation](#os-x-installation)
  - [Windows Installation](#windows-installation)
  - [Linux Installation](#linux-installation)
- [Adding tab-completion to vv](#adding-tab-completion-to-vv)
- [Updating](#updating)
- [Usage](#usage)
- [Site Creation](#site-creation)
  - [Subdomain Multisite Installation](#subdomain-multisite-installation)
- [Site Deletion](#site-deletion)
- [Deployments](#deployments)
- [Advanced Usage](#advanced-usage)
  - [Airplane Mode](#airplane-mode)
  - [Flags](#flags)
- [Blueprints](#blueprints)
  - [Blueprints for Multisite configurations](#blueprints-for-multisite-configurations)
  - [Blueprints for Multi-Network configurations](#blueprints-for-multi-network-configurations)
- [Vagrant Proxy](#vagrant-proxy)
- [vv Options](#vv-options)
  - [Commands](#commands)
  - [Options for Site Creation](#options-for-site-creation)
  - [Options for Site Removal](#options-for-site-removal)
  - [Options for Deployment Setup](#options-for-deployment-setup)
- [.vv-config](#vv-config)
- [vv Hooks](#vv-hooks)
- [Thanks](#thanks)

## Installation

### OS X Installation

If you have [Homebrew](http://brew.sh/) installed, you run the following in your terminal application:

	$ brew install bradp/vv/vv

Otherwise, clone this repositoy and edit your `$PATH` to include the `vv` core file:

1. Clone this repo: `git clone https://github.com/bradp/vv.git`
1. Add the `vv` core script to your shell's `$PATH`:
    * If you're using `bash`: ``touch ~/.bash_profile && echo "export PATH=\$PATH:`pwd`/vv" >> ~/.bash_profile``

### Windows Installation

* Clone `vv` to a folder somewhere.

    `$ git clone https://github.com/bradp/vv.git`

* Add that folder to your system path. See [here](http://windowsitpro.com/systems-management/how-can-i-add-new-folder-my-system-path) if you need help.

* Open an explorer window and go to My Computer (or This PC).
* Right click and choose properties
* Choose Advanced System Settings
* Choose Environmental Variables form the Advanced Tab
* Choose the "Path" variable and edit it.
* Add a semicolon to end the previous path item and then add the `vv` folder path (Example: `;C:\Users\Name\Documents\vv`)
* Open Git Bash and run `vv`

Alternately, you can use cmd.exe with `bash vv`.

Props to [Vinsanity](https://github.com/Vinsanity) for these instructions. If you're having issues, please see [this issue](https://github.com/bradp/vv/issues/33).

### Linux Installation

* Clone vv into a folder.

    `$ git clone https://github.com/bradp/vv.git`

* Access the directory that you cloned vv into.

* Copy the vv executable to /usr/local/bin

    `$ sudo cp vv /usr/local/bin`

* You should now be able to easily run vv from anywhere in your system.

## Adding tab-completion to `vv`

Currently, `vv` supports tab-completion of arguments and options in both bash and ZSH. To enable this, you'll first want to make sure you're on the most current version of `vv`. Then simply add `source $( echo $(which vv)-completions)` to the end of your .bash_profile, .bashrc or .zshrc.

## Updating

vv is currently under development, and you'll probably want the latest and greatest version at all times.

You can run `vv --update` to update to the latest version. This will update via Homebrew if you've installed it that way, otherwise vv will bootstrap an update on where ever you've installed it.

vv will automatically check for updates and update itself once a week. You can disable this by adding `"auto_update_disable": false` to the JSON config in `~/.vv-config`.

If you have trouble updating, you may want to try some of the options below:

Homebrew sometimes caches a version of Variable VV causing you to receive a message saying you are out of date with the Github version, however running `vv --update` simply downloads a version you already have installed. In cases like this, there are two safe options you can try.

First, and simplest, run `vv --force-update`. Second, if that does not work you can safely uninstall Variable VV and re-install it via homebrew, you can do this with these commands: `brew remove vv` then `brew untap bradp/vv` and finally, run the install command `brew install bradp/vv/vv`as mentioned above. You will not lose any settings or sites.

## Usage

Once installed, you can run `vv` anywhere you'd like. If vv can't automatically find your VVV installation, you will be prompted for the path. It will also save this into a configuration file in `~/.vv-config`, so you won't be prompted again.

At any time, you can run `vv` or `vv --help` to see a list of all possible options and flags.

vv will prompt you for a value for any required flags that were not specified.

The main commands are `list`, `create`, `delete`. These will list your sites, create a site, and delete a site. These each have a few aliases, so for example, if you run `vv show`, vv will know you meant `vv list`.

To start creating a site, simply do `vv create` ( you can also do `vv --create`, or simply `vv -c`). You will then be prompted for all required options.

All options and flags are [listed below](#vv-options).

## Site Creation

`vv create`

Creating a site does the following:

* Halts Vagrant (if running)
* Creates a web root for the site in the `www` folder containing three files: `vvv-init.sh`, `wp-cli.yml`, and `vvv-hosts`
	* `vvv-init.sh` tells Vagrant to create a database if one does not exist and install the latest version of WordPress (via WP-CLI) the next time Vagrant is provisioned
	* `wp-cli.yml` tells WP-CLI that WordPress is in the htdocs folder
	* `vvv-hosts` contains the hosts entry to give your site a nice custom domain (the domain is set in the wizard)
* Creates a file in the `nginx-config` folder to handle server settings for your site
* Restarts Vagrant with `vagrant up --provision`

Provisioning Vagrant takes a couple of minutes, but this is a crucial step as it downloads WordPress into your site's htdocs directory and runs the installation. If you want to skip provisioning and install WordPress manually, you can run the new site's `vvv-init.sh` file directly in the Vagrant shell.

### Subdomain Multisite Installation

If you are using a subdomain multisite, you must edit vvv-hosts file inside of that site's folder with each subdomain on a new line. For example:

 > mysite.dev

 > siteA.mysite.dev

 > siteB.mysite.dev


After this, run `vagrant reload --provision` and your subdomains should resolve. *Please note*, any sites set up prior to version 1.7.3 will need more configuration for this, either delete and re-set up the site or [ping me on Twitter](http://twitter.com/bradparbs) for help.

## Site Deletion

`vv delete site_name`

You can also leave off site_name to be prompted for it.

Deleting a site does the following:

* Halts Vagrant (if running)
* Deletes the site's web root (which deletes the `vvv-init.sh`, `wp-cli.yml`, and `vvv-hosts` files as well)
* Deletes the file in the `nginx-config` folder pertaining to the site
* Deletes the database associated with the site

## Deployments

`vv deployment-create`, `vv deployment-remove`, `vv deployment-config`

vv supports setting up deployments that work with [Vagrant Push](https://docs.vagrantup.com/v2/push/index.html). You'll need to be on version 1.7.0 or later of Vagrant. Simply run `vv --deployment-create` and walk through the wizard.

To deploy a site, you can do `vv vagrant push <sitename>-<deployment_name>`.

When removing a deployment, your current Vagrantfile will be backed up as Vagrantfile-backup.


## Advanced Usage

### Airplane Mode

Using `x` as the first argument with `vv` will force airplane mode. This will cut off update checks on usage. This is useful if you're using `vv` without an internet connection. The provision state of VVV will probably fail at some point, though.

### Flags
Anything that vv prompts you for, you can pass in as an argument. Most of this is realized in the site creation. In fact, there are a few arguments you can pass in that aren't prompted. This gives you total control over creating a new site.

To create a new site named 'mysite' that has the domain 'mysite.dev' and is a multisite with subdomains, with `WP_Debug` turned on would be:

`vv create -d mysite.dev -n mysite -m subdomains -x`

Or, the more readable version with all expanded flags.

`vv create --domain mysite.dev --name mysite --multisite subdomains --debug`

To use a custom database prefix, simply use the `vv create --prefix myprefix` when creating a new site.

## Blueprints

Blueprints allow you to set up different plugins, themes, mu-plugins, options, widgets, menus, or constants that will be installed to a new site you create. First, run `vv --blueprint-init` to have vv create a `vv-blueprints.json` file in your VVV directory. You can edit this file to create and set up different blueprints.

A simple blueprint should look like this:
```json
{
  "sample": {
    "themes": [
      {
        "location": "automattic/_s",
        "activate": true
      }
    ],
    "mu_plugins": [
      {
        "location": "https://github.com/WebDevStudios/WDS-Required-Plugins.git"
      }
    ],
    "plugins": [
      {
        "location": "https://github.com/clef/wordpress/archive/master.zip",
        "version": null,
        "force": false,
        "activate": true,
        "activate_network": false
      },
      {
        "location": "cmb2",
        "version": "2.0.5",
        "force": false,
        "activate": true,
        "activate_network": false
      }
    ],
    "options": [
      "current_theme::_s"
    ],
    "widgets": [
      {
        "name": "meta",
        "location": "sidebar-1",
        "position": 1,
        "options": {
          "title": "Site login or logout"
        }
      },
      {
        "name": "text",
        "location": "sidebar-2",
        "position": 4,
        "options": {
          "title": "Hello world.",
          "text": "I'm a new widget."
        }
      }
    ],
    "menus": [
      {
        "name": "Example Menu",
        "locations": [
          "primary",
          "social"
        ],
        "items": [
          {
            "type": "post",
            "post_id": 2,
            "options": {
              "title": "Read the 'Sample Post'"
            }
          },
          {
            "type": "custom",
            "title": "Our Partner Site",
            "link": "//example.com/",
            "options": {
              "description": "Check out our partner's awesome website."
            }
          },
          {
            "type": "term",
            "taxonomy": "category",
            "term_id": 1,
            "options": {
              "title": "Example category"
            }
          }
        ]
      }
    ],
    "demo_content": [
      "link::https://raw.githubusercontent.com/manovotny/wptest/master/wptest.xml"
    ],
    "defines": [
      "WP_CACHE::false"
    ]
  }
}

```

For themes, plugins, and mu-plugins, you can use:

* Github username/repo
* Full git url
* Url to zip file
* WordPress.org slug

The options for plugins, themes, widgets, and menus correspond to the equivalent [WP CLI](http://wp-cli.org) option.

For options, demo content, and constants, please note the `::` as a separator between the key and value.

Custom demo content can be imported through the blueprint. Be sure to use a link that points to just the xml code, like [this](https://raw.githubusercontent.com/manovotny/wptest/master/wptest.xml). You can add as many demo content files as you'd like, just separate each line with a comma as usual.

A multisite's Network Settings can be configured using a `network_options` array in the blueprint.

You can create as many named blueprints in this file as you would like, all with as many different settings as you'd like.

When creating a site, the name you've specified (in this example, "sample") is what you'll need to specify to use this blueprint.

You can use 'SITENAME' or 'SITEDOMAIN' anywhere in the blueprint, and that will be replaced with the actual site name or local domain when installing.

### Blueprints for Multisite configurations

Blueprints also let you set up individual subsites in a Multisite network. For example, you can define a blueprint for a multisite network in which certain plugins or themes are activated across the whole network, or just for specific subsites.

To add multisite support to your blueprint, add a `sites` key to a specific blueprint, like this:

```json
"sites": {
  "site2": {
    "plugins": [
      "...(same as above)..."
    ]
  }
}
```

The `sites` object holds a subsite definition, which has the same capabilities as a regular site's blueprint (so `plugins`, `themes`, etc. are all the same), and also includes keys for [WP-CLI's `wp site create` command](http://wp-cli.org/commands/site/create/). For example, to create a subsite whose slug is `subsite2`, titled "Second Subsite" with an admin email address of `subsite2admin@localhost.dev` with `robots.txt` exclusions, use:

```json
"sites": {
  "subsite2": {
    "title": "Second Subsite",
    "email": "subsite2admin@localhost.dev"
  }
}
```

If your multisite network uses subdomains, you can include a blueprint-level key named like `BLUEPRINT_NAME::subdomains` to have `vv` configure your subdomains for you. `BLUEPRINT_NAME` should match the name of your blueprint, and the value should be a space-separated list of subdomains that match your subsite slugs. A complete example for the `sample` blueprint shown above using subdomain-based multisite configurations might look like this:

```json
{
  "sample": {
    "sample::subdomains": "site2 site3",
    "sites": {
      "site2": {
        "title": "Child Site (subsite2)",
        "plugins": [
          {
            "location": "buddypress",
            "activate": true
          }
        ]
      },
      "site3": {
        "title": "Private Child Site",
        "private": true,
        "email": "site2admin@local.dev",
        "themes": [
          {
            "location": "https://github.com/glocalcoop/anp-network-main-child/archive/master.zip",
            "activate": true
          }
        ]
      }
    },
    "themes": [
      {
        "location": "automattic/_s",
        "enable_network": true
      },
      {
        "location": "glocalcoop/anp-network-main-v2",
        "activate": true
      }
    ],
    "mu_plugins": [
      {
        "location": "https://github.com/WebDevStudios/WDS-Required-Plugins.git"
      }
    ],
    "plugins": [
      {
        "location": "https://github.com/clef/wordpress/archive/master.zip",
        "version": null,
        "force": false,
        "activate": true,
        "activate_network": false
      },
      {
        "location": "cmb2",
        "version": "2.0.5",
        "force": false,
        "activate": true,
        "activate_network": false
      },
    ],
    "demo_content": [
      "link::https://raw.githubusercontent.com/manovotny/wptest/master/wptest.xml"
    ],
    "defines": [
      "WP_CACHE::false"
    ]
  }
}
```

The above installs [BuddyPress](https://buddypress.org/) but activates it only for `site2`, enables the `_s` theme for the entire network but activates `anp-network-main-v2` for the network's main site and `anp-network-main-child` for `site3`, which is also given its own site admin user.

Be sure to run `vv` with the `--multisite subdomain` option when you use a blueprint like this.

### Blueprints for Multi-Network configurations

In addition to a [multisite configuration](#blueprints-for-multisite-configurations), VV recognizes blueprints that will configure a WP Multi-Network (a network of WP Multisite networks). VV's Multi-Network blueprints work just like Multisite blueprints, but have the following required additions:

* A `BLUEPRINT_NAME::subnetwork_domains` key must be present listing the root domains for each network.
* A `networks` object must be present, whose keys match the domains listed in the `BLUEPRINT_NAME::subnetwork_domains` member.

For example, this Multi-Network configuration defines two WP Multisite subnetworks (for a total of three WP Multisites) in the blueprint called `multinet`.

```json
{
  "multinet": {
    "multinet::subdomains": "site2 site3",
    "multinet::subnetwork_domains": "wpsubnet1.dev wpsubnet2.dev",
    "networks": {
      "wpsubnet1.dev": {
        "path": "/",
        "site_name": "WP Subnetwork Example 1"
      },
      "wpsubnet2.dev": {
        "path": "/",
        "site_name": "WP Subnetwork Example 2"
      }
    }
  }
}
```

Note that empty network objects are allowed (i.e., `path` and `site_name` are optional), but not recommended.

To associate a given subsite with a network, you can either use the `network_id` key or a `network_domain` key in the subsite object. A `network_domain` is recommended. For example, this object will associate the `site2` subsite with the main network (because no `network_domain` or `network_id` key is defined), and the subsite with slug `site3` with the network created at the given domain:

```json
{
  "site2": {
  },
  "site3": {
    "network_domain": "wpsubnet1.dev"
  }
}
```

The above will ultimately place `site3` at the `site3.wpsubnet1.dev` URL while `site2` will be created as a subdomain of whatever domain you chose when you invoked `vv create`.

It is not an error for a WP network to be defined with no sites of its own.

## Vagrant Proxy

Because vv knows where you VVV installation is, you can run it from anywhere. vv will proxy any commands passed into `vv vagrant <command>` to your VVV location. So `vv vagrant halt` will halt your VVV vagrant, no matter where you run it.

## `vv` Options

|Option|Description|
|------|-----------|
|`--help`, `-h`| Show help and usage|
|`--version`|Show current vv version number.|
|`--about`|Show about screen.|
|`--update`|Updates vv to the latest stable version|
|`--debug-vv`|Outputs all debugging info needed for bug reporting.|
|`--path`,	`-p`|Path to VVV installation|
|`--force-path`, `-fp`|Override vv auto-VVV locating|
|`--force-sites-folder`,`-fsf`|Override sites folder directory locating|
|`--defaults`|Accept all default options and skip the wizard. You can also run `yes | vv create ... other flags ... -defaults` to skip the final confirmation|

### Commands

|Command|Description|
|-------|-----------|
|`list`, `--list`,  `-l`|List all VVV sites|
|`create`, `--create`, `-c`|Create a new site|
|`delete`, `--delete`, `-r`|Delete a site|
|`deployment-create`, `--deployment-create`|Set up deployment for a site|
|`deployment-remove`, `--deployment-remove`|Remove deployment for a site|
|`deployment-config`, `--deployment-config`|Manually edit deployment configuration|
|`blueprint-init`, `--blueprint-init`|Initalize blueprint file|
|`vagrant`, `v`, `--vagrant`, `-v`|Pass vagrant command through to VVV.|

### Options for Site Creation

|Option|Description|
|------|-----------|
|`--name`, `-n`|Desired name for the site directory (e.g. mysite)|
|`--domain, -d`|Domain of new site|
|`--webroot`, `-wr`|Subdirectory used for web server root|
|`--bedrock`, `-bed`|Creates Roots.io Bedrock install|
|`--blueprint`, `-b`|Name of blueprint to use|
|`--live-url`, `-u`|Live URL of site|
|`--files`, `-f`|Do not provision Vagrant, just create the site directory and files|
|`--images`, `-i`|Load images by proxy from the live site|
|`--wp-version`, `-wv`|Version of WordPress to install|
|`--debug`, `-x`|Turn on WP_DEBUG and WP_DEBUG_LOG|
|`--multisite`, `-m`|Install as a multisite. Can also pass in "subdomain" or "subdirectory"|
|`--sample-content`,`-sc`|Adds sample content to site.|
|`--username`|Admin username|
|`--password`|Admin password|
|`--email`|Admin email|
|`--prefix`|Database prefix to use|
|`--git-repo`,`-gr`|Git repo to clone as wp-content|
|`--path`,	`-p`|Path to VVV installation|
|`--force-path`, `-fp`|Override vv auto-VVV locating|
|`--blank`|Creates blank VVV site, with no WordPress|
|`--blank-with-db`|Creates a blank VVV site, with a database|
|`--wpskeleton`, `-skel`|Creates a new site with the structure of [WP Skeleton](https://github.com/markjaquith/WordPress-Skeleton)
|`--database`,`-db`|Imports a local database export|
|`--remove-defaults`,`-rd`|Removes default themes and plugins|
|`--language`,`--locale`|Install WP in another locale. Need to pass the locale afterwards, like so: `vv create --locale fr_FR`|

### Options for Site Removal
|Option|Description|
|------|-----------|
|`--name`, `-n`|Desired name for the site directory (e.g. mysite)|
|`--path`,	`-p`|Path to VVV installation|
|`--force_path`, `-fp`|Override vv auto-VVV locating|

### Options for Deployment Setup
|Option|Description|
|------|-----------|
|`--name`, `-n`|Desired name for the site directory (e.g. mysite)|
|`--deployment-name`|Name of deployment (production, staging, other, etc)|
|`--host`|Host (if SFTP, define port as host:port) |
|`--username`|FTP Username |
|`--password`|FTP Password  |
|`--passive`|Use Passive transfer mode? (y/n)  |
|`--secure`|Use SFTP? (y/n) |
|`--destination`|Destination path ( You probably want / or ~/public_html ) |
|`--confirm-removal`|Used when removing a deployment to skip the confirmation prompt |


## `.vv-config`

The first time you run `vv`, it will attempt to locate your VVV installation location. If it can't find it, you will be prompted for it. This will be written to a .vv-config file in your home directory. (`~/.vv-config`) You can also edit this file if you need to change your VVV path.

Also, if `vv` detects a `.vv-config` file in your current directory, this local file will override the one in your home directory. A use case would be to have several different `VVV` installations, that each contain their own local `.vv-config` file. Provided that you enter the appropriate directory before sending commands to `vv`, this effectively allows you to manage several different installations through one user account.

You can also add `"auto_update_disable": false` to this file to disable auto-update functionality.


## `vv` Hooks

`vv` has support for extensibility within the 'hooks' system present. This allows for quite a lot of extensibility and injection into the `vv` process. This system allows you to add your own code to run within almost any point with `vv`.

To get started with hooks, run any `vv` command with `--show-hooks` at the end. For example, `vv list --show-hooks` will run `vv list` as normal, but will also show all the hooks available.

To create the folder that your hook code should live in, simply make a 'vv' folder inside of your VVV folder.

To add code to run for a hook, make a file within your vv folder inside of VV named the hook that you want to add to. This file can be any command line runnable language, and will be executed inline.

For example, saving this file as the name of any hook will output 'Hello' when that hook gets called.

```bash
    #! /usr/bin/php
    echo 'Hello'
```

Another example would be running npm install inside of wp-content for all new sites.

Make a file named post_site_creation_finished. This file gets 4 variables passed in: the hook name, the name of the site folder, the site domain, and the VVV path.

```bash
    #!/bin/bash
    cd www/"$2"/htdocs/wp-content || exit
    npm install
```


## Thanks

Forked and based off of [vvv-site-wizard from Alison Barrett](https://github.com/aliso/vvv-site-wizard).
Also thanks to [meitar](https://github.com/meitar), [creativecoder](https://github.com/creativecoder), [jtsternberg](https://github.com/jtsternberg), [caseypatrickdriscoll](https://github.com/caseypatrickdriscoll), [gregrickaby](https://github.com/gregrickaby), [leogopal](https://github.com/leogopal), [ajdruff](https://github.com/ajdruff), [schlessera](https://github.com/schlessera), [john-g-g](https://github.com/john-g-g), [tnorthcutt](https://github.com/tnorthcutt), [wpsmith](https://github.com/wpsmith), [wesbos](https://github.com/wesbos), [protechig](https://github.com/protechig), [Ipstenu](https://github.com/Ipstenu), [justintucker](https://github.com/justintucker), [michaelbeil](https://github.com/michaelbeil), [jb510](https://github.com/jb510), [neilgee](https://github.com/neilgee), [nanomoffet](https://github.com/nanomoffet), [joehills](https://github.com/joehills), [JeffMatson](https://github.com/JeffMatson), [greatislander](https://github.com/greatislander), [pelmered](https://github.com/pelmered), [gMagicScott](https://github.com/gMagicScott), [alexschlueter](https://github.com/alexschlueter), [eriktdesign](https://github.com/eriktdesign), [WPprodigy](https://github.com/WPprodigy), [michaelryanmcneill](https://github.com/michaelryanmcneill), [boborchard](https://github.com/boborchard), [cryptelli](https://github.com/cryptelli), [lswilson](https://github.com/lswilson) for their contributions.
