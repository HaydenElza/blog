---
date: 2016-04-20
layout: post
title: "Arch Linux: Find Disk Space by Cleaning Filesystem"
categories:
- linux
tag:
- Arch Linux
- HD space
- filesystem
- storage
- clean up
---

Hmm... chrome won't start:

~~~bash
$ google-chrome-stable
yada yada Invalid url pattern: chrome://print/*
~~~

I wonder if my disk is full?

~~~bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G   29G     0 100% /
tmpfs           2.8G  8.0K  2.8G   1% /tmp
/dev/sda4       421G  346G   54G  87% /home
~~~

Oh. My root is full, that'll do it. Better do some tidying to free up disk space.



### Remove Unused Packages (Orphans)

To *recursively* remove orphans and their configuration files use:

~~~
# pacman -Rns $(pacman -Qtdq)
~~~

This removes all packages which are no longer used as a dependency as well as their config files. As with anything that's recursive, proceed with caution, though you should be fine.


### Cleaning the package cache

~~~
# pacman -Sc
~~~

Once in a while you will need to run this to clean out old or uninstalled packages that where downloaded by pacman during installation. Pacman doesn't clean this automatically so it can grow indefinitely, which in my case is what took up the majority of the space.

The disadvantage of using this is that you cannot [downgrade](https://wiki.archlinux.org/index.php/Downgrade) later, so only use it if you are certain previous package versions are not required.


### Conclusion

Let's see if that helped:

~~~bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G   11G   17G  40% /
tmpfs           2.8G  8.0K  2.8G   1% /tmp
/dev/sda4       421G  346G   54G  87% /home
~~~

I gained *18GB*, impressive.

Hopefully this helps someone else out. If you have any questions or just want to say hey, you can find my social doots at the bottom of the page.

<br>
Resources:

 - [Arch Linux Wiki: System Maintenance - Clean Filesystem](https://wiki.archlinux.org/index.php/System_maintenance#Clean_the_filesystem)
 - [Arch Linux Wiki: Remove Unused Packages (Orphans)](https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29)
 - [Arch Linux Wiki: Cleaning the Package Cache](https://wiki.archlinux.org/index.php/Pacman#Cleaning_the_package_cache)