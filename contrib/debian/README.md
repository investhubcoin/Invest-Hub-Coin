
Debian
====================
This directory contains files used to package ihcd/ihc-qt
for Debian-based Linux systems. If you compile ihcd/ihc-qt yourself, there are some useful files here.

## ihc: URI support ##


ihc-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install ihc-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your ihcqt binary to `/usr/bin`
and the `../../share/pixmaps/ihc128.png` to `/usr/share/pixmaps`

ihc-qt.protocol (KDE)

