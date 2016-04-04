---
date: 2016-04-04
layout: post
title: "error: failed to prepare transaction (could not satisfy dependencies) 
:: package-query: requires pacman<4.3"
categories:
- linux
tag:
- Arch Linux
- package-query
- pacman
---

Oops, forgot to update Arch linux for a while and was met by the following message after trying to run ```pacman -Syu```:

~~~bash
error: failed to prepare transaction (could not satisfy dependencies)
:: package-query: requires pacman<4.3
~~~

This is because there was a change in the library that bridged between yaourt and pacman.

To fix, remove package-query and manually install the snapshot from AUR:

~~~bash
pacman -Rdd package-query
git clone https://aur.archlinux.org/package-query.git
cd package-query
makepkg -si
~~~

You should now be clear to run ```pacman -Syu```.

<br>

---

<br>

Resources:

- [Reddit: Problem with pacman -Syu, could not satisfy dependencies?](https://www.reddit.com/r/archlinux/comments/43ofo1/problem_with_pacman_syu_could_not_satisfy/)
- [Reddit: How do I install package-query and yaourt with pacman 5.0?](https://www.reddit.com/r/archlinux/comments/43nnb4/how_do_i_install_packagequery_and_yaourt_with/)
