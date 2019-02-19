This is manifest repository for raspberry pi yocto compilation
It will allow repo tool to download all projects required to build the bsp.

To install Repo
===============

Download the Repo tool and ensure that it is executable:

	$ curl https://storage.googleapis.com/git-repo-downloads/repo > /tmp/repo
	$ chmod a+x /tmp/repo
	$ sudo mv /tmp/repo /usr/bin

Initializing a Repo client
==========================

Create an empty directory to hold your working files. Give it any name you like:

	$ WORKING_DIRECTORY="yocto-rpi-$(date +%Y%m%d)"
	$ mkdir $WORKING_DIRECTORY
	$ cd $WORKING_DIRECTORY

Set up Git if not already done:

	$ git config --global user.name "Your Name"
	$ git config --global user.email "you@example.com"

Run repo init as the following:

	$ repo init -u https://github.com/aurelihein/yocto-rpi-manifest [build_dir_name]

To check out a branch other than "master", specify it with -b.

	$ repo init -u [url to this repository] -b [some branch] -m [manifest name.xml] [build_dir_name]

Example :

	$ repo init -u https://github.com/aurelihein/yocto-rpi-manifest -b master -m default.xml

Example for testing browser branch implementing WPE :

	$ repo init -u https://github.com/aurelihein/yocto-rpi-manifest -b master -m wpe.xml

Downloading The raspberry pi yocto Source Tree
==============================================

	$ repo sync

Building raspberry pi yocto
===========================

	$ source rpi-bouin-init-build-env  [build_dir_name]

The above command will place you in the build directory

	$ bitbake rpi-basic-image

Misc
====

More information about repo tool can be found here:
https://source.android.com/source/using-repo.html

Test The raspberry pi yocto Compilation For Browser / Kiosk / Web Browsing Usage
=================================================================

	$ WORKING_DIRECTORY="yocto-rpi-browser-$(date +%Y%m%d)"
	$ mkdir $WORKING_DIRECTORY
	$ cd $WORKING_DIRECTORY
	$ repo init -u https://github.com/aurelihein/yocto-rpi-manifest -b master -m wpe.xml
	$ repo sync
	$ source rpi-bouin-init-build-env build
	$ bitbake rpi-browser-image
