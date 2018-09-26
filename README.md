jailrun
=======

Wrapper to run a firejailed graphical application, inside an optional
firejailed desktop environment (window manager, panel, systray) inside a
firejailed per-environment Xephyr Xserver instance.

Rationale
---------

I was never keen on Skype, but especially when Microsoft bought
it I avoided it at all costs and used SIP (& GTalk for the SIP-illiterate).
Unfortunately there are always the few people who refuse to consider
anything other than Skype (often they are the same people who will
only network with Facebook). When some of those people are ones
you *must* interact with for work-reasons, it gets a bit tricky.
When I noticed that Skype had started (about 10 years too late) to
support Linux in a way that is not so ridiculous, I decided to set it up in
as sandboxed/crippled/blinded/impotent form as possible for those moments
when it is the only option left to me. I found
[this blogpost](https://spwhitton.name/blog/entry/firejailskype/) and built
on that, to have a user-friendly wrapper for running skypeforlinux in
a customized firejail. Later I realized the better way to customize
the firejail profile is via /etc/firejail/XXX.local file which each
standard profile includes if present. Therefore I renamed this from
jailskype to jailrun and made it purely a wrapper for running a firejailed
application inside its own firejailed desktop-environment (with optional
window-manager, panel, and systray) running inside its own Xephyr Xserver.

Installation
------------

* Ensure `firejail` is installed with a profile for the app (Debian
  includes profiles in `/etc/firejail/[XXX].profile`), and modify it via
  its `.local` file if desired (usually in the same directory as the
  `[XXX].profile` file, named `[XXX].local`). For any options you want
  applied globally put them in `/etc/firejail/firejail.conf`. It is not
  necessary to configure `x11 xephyr` and `xephyr-screen YYxYY` here
  as the wrapper script will pass those as optflags, but note that
  some options can be included in config files but can't be passed by
  flag, e.g. `xephyr-extra-params -resizable`.

* Ensure `openbox` (or whatever compatible window-manager you specify
  with the `--window-manager` flag) is installed.

* Copy or symlink `jailrun` into your $PATH.

Quick Start
-----------

* `jailrun --help` for details.

License
-------

Copyright © 2017,2018 Rowan Thorpe <rowan@rowanthorpe.com>

`jailrun` uses the GPLv3 license, check the `COPYING` file.

Any additional contributions are noted in the `AUTHORS.md` file.
