This is manifest repository for raspberry pi yocto compilation
It will allow repo tool to download all projects required to build the bsp.

To install Repo
===============

Make sure you have a bin/ directory in your home directory and that it is
included in your path:

	$ mkdir ~/bin
	$ PATH=~/bin:$PATH

Download the Repo tool and ensure that it is executable:

	$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	$ chmod a+x ~/bin/repo

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

	$ repo init -u [url to this repository] -b [some branch] [build_dir_name]
Example :

	$ repo init -u https://github.com/aurelihein/yocto-rpi-manifest -b master

Downloading The raspberry pi yocto Source Tree
=====================================

	$ repo sync

Building raspberry pi yocto
==================

	$ source rpi-bouin-init-build-env  [build_dir_name]

The above command will place you in the build directory

	$ bitbake rpi-basic-image

Misc
====

More information about repo tool can be found here:
https://source.android.com/source/using-repo.html
