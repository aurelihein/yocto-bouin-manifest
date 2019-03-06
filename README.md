This is manifest repository for yocto compilation support
It will allow repo tool to download all projects required to build the bsp.

To install Repo
===============

Download the Repo tool and ensure that it is executable:

    $ curl https://storage.googleapis.com/git-repo-downloads/repo > /tmp/repo
    $ chmod a+x /tmp/repo
    $ sudo mv /tmp/repo /usr/bin

Initializing a Yocto build environment common among severals builds
==========================

    $ sudo mkdir /yocto
    $ sudo chown $USER:$(id -gn) -R /yocto
    $ mkdir /yocto/{downloads,sstate-cache-rpi,sstate-cache-odroid-c2}
    $ cd /yocto

Download required packages for Yocto
====================================

    $ sudo apt-get update
    $ sudo apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm libncurses5 libncurses5-dev
    $ sudo apt-get -y install tree htop

Initializing a Repo client
==========================

Create an empty directory to hold your working files. Give it any name you like:

    $ WORKING_DIRECTORY="$(date +%Y%m%d)-yocto"
    $ mkdir $WORKING_DIRECTORY
    $ cd $WORKING_DIRECTORY

Set up Git if not already done:

    $ git config --global user.name "Your Name"
    $ git config --global user.email "you@example.com"

Run repo init as the following:

    $ repo init -u https://github.com/aurelihein/yocto-bouin-manifest [build_dir_name]

To check out a branch other than "master", specify it with -b.

    $ repo init -u [url to this repository] -b [some branch] -m [manifest name.xml] [build_dir_name]

Example :

    $ repo init -u https://github.com/aurelihein/yocto-bouin-manifest -b master -m default.xml

Example for testing browser branch implementing WPE with rpi :

    $ repo init -u https://github.com/aurelihein/yocto-bouin-manifest -b master -m wpe-rpi.xml

Example for testing browser branch implementing WPE with odroid :

    $ repo init -u https://github.com/aurelihein/yocto-bouin-manifest -b master -m wpe-odroid.xml

Downloading The yocto Source Tree
==============================================

     repo sync

Building raspberry pi yocto
===========================

    $ source rpi-bouin-init-build-env  [build_dir_name]

The above command will place you in the build directory

    $ bitbake rpi-basic-image

Misc
====

More information about repo tool can be found here:
https://source.android.com/source/using-repo.html

Test yocto Compilation For Browser / Kiosk / Web Browsing Usage
=================================================================

    $ WORKING_DIRECTORY="yocto-rpi-browser-$(date +%Y%m%d)"
    $ mkdir $WORKING_DIRECTORY
    $ cd $WORKING_DIRECTORY
    $ repo init -u https://github.com/aurelihein/yocto-bouin-manifest -b master -m wpe-rpi.xml
    $ repo sync
    $ source rpi-bouin-init-build-env build
    $ bitbake rpi-browser-image

Info : https://github.com/Igalia/meta-webkit/wiki/WPE
You can then try the image with :

    $ export WPE_BCMRPI_TOUCH=1
    $ export WPE_BCMRPI_CURSOR=1
    $ export WPE_DISPLAY_FPS=1
    $ cog https://www.primevideo.com
