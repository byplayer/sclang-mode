sclang-mode
===========
This is a fork of [the official SuperCollider sclang-mode for emacs](https://github.com/supercollider/supercollider/tree/master/editors/scel/el). I have not submitted a pull request and probably won't, since I am not terribly confident in my elisp-fu, nor have I really done a lot of testing on these changes to the official one. Hopefully people who use emacs to write SC will find this and find it useful, though.

If you have any problems with the changes I've made, feel free to submit an issue report. For the most part, however, this should work as a drop-in replacement for the sclang-mode that ships with SC.

I've also written other elisp to make writing SC easier in emacs, but it is separate from this repo, and is totally optional. If you are interested, check out [my supercollidexr repo](https://github.com/defaultxr/supercollidexr), where my-sclang.el is stored. Some things in it might only make sense if you also install the SuperCollider class files in that repo as well.

changes made
============
The things that I changed from the official sclang-mode:
* Remove the class regex (and thus make it possible to detect class names even when many SC quarks/classes are installed)
  * The official sclang-mode will stop highlighting classes if you have too many installed. The reason for this is that it generates a list of all the classes and then converts it into a big regex. Emacs has a maximum size for regexes, and if you have too many classes to be represented in a regex, it will fail, and no class names will be syntax highlighted.
  * My fix is to use the general regex to look for things that MIGHT be class names (i.e. any word that starts with a capital letter) and then check for that word's existence in the list of all the class names. This might be slightly slower, but I haven't noticed it being slower when I scroll the window or move the point or whatever. It also might cause some unforeseen bugs that I am not yet aware of.
  * These changes are mostly in `sclang-mode.el`, in the `sclang-update-font-lock` and `sclang-font-lock-class-keyword-matcher` functions, as well as the variable I defined (which holds the list of all the classes), `sclang-list-of-classes`.
