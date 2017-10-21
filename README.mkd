Color schemes for Gnome Terminal
========================================

Scripts for setting solarized, base-16 and zenburn color schemes in gnome
terminal

Installation and usage
----------------------

To be able to uninstall, we highly recommend that you create a new Gnome
Terminal profile, using the menus in Gnome Terminal.

You need the `dconf` command (if you run a recent Gnome version). With Ubuntu,
this can be installed by running

    $ sudo apt-get install dconf-cli

Then clone the repository and you can run the installation script:

    $ git clone https://github.com/gnumoksha/gnome-terminal-colors.git
    $ cd gnome-terminal-colors
    $ ./install.sh

And just follow the instructions.

To run this script remotely or via cron (or from any shell where
`DBUS_SESSION_BUS_ADDRESS` is not set), you need to start a dbus connection:

    $ dbus-launch ./install.sh

Uninstall
---------

Change to another profile in Gnome Terminal, then remove the Solarized profile
by running:

### Gnome 3.6 or lower

    $ rm -r ~/.gconf/apps/gnome-terminal/profiles/Solarized/
    $ gconftool-2 --recursive-unset /apps/gnome-terminal

### Gnome 3.8 or higher

Be sure to have the dconf-cli package installed and do:

    $ dconf reset -f /org/gnome/terminal/legacy/profiles:/PROFILE_ID"

Replace PROFILE_ID by your profile ID (you can get it in your profile
configuration in gnome-terminal).

Themes
------

Each theme has is own folder in the `colors` dir. It contains the following
files:

  * bd_color: bold color
  * bg_color: background color
  * fg_color: foreground color
  * palette: list of colors for all standard color codes.

No additional configuration is needed to add a theme, the installation script
just list at launch the children folders in the `colors` dir.

Dircolors
---------

The installation script will ask if a solarized dircolors is wanted. It will be
downloaded and installed as `~/.dir_colors/dircolors`. On CentOS, it can be an
issue (see issue #62), as the default setup use `~/.dir_colors` as dircolors.
In that case, you should manually move `~/.dir_colors` as
`~/.dir_colors/dircolors` before starting the installation script.

If the dircolors is not applied, please check that your shell actually source
your dircolors:
```
if [ -f ~/.dir_colors/dircolors ]
    then eval `dircolors ~/.dir_colors/dircolors`
fi
```

This should not be necessary on major distributions (such as Ubuntu, Fedora,
etc.) but could be on ArchLinux, Gentoo and others.

Contributors
------------

* Sigurd Gartmann <sigurdga@sigurdga.no>
* Anthony Ruhier <anthony.ruhier@gmail.com>
* Paul Thomson <captbunzo@gmail.com>
* Techlive Zheng <techlivezheng@gmail.com>
* Daniel Graña <dangra@gmail.com>

FAQ
===

Conflicting background colors in VIM
------------------------------------

Use the 16 colors terminal option to get VIM to look like GVIM with solarized
colors.

    set t_Co=16

