jailskype
=========

Start skypeforlinux in a customized firejail.

Rationale
---------

I was never keen on Skype, but especially when Microsoft bought
it I avoided it at all costs and used SIP (& GTalk for the SIP-illiterate).
Unfortunately there are always the few people who refuse to consider
anything other than Skype (often they are the same people who will
only network with Facebook). When some of those people are ones
you *must* interact with for work-reasons, it gets a bit tricky.
Lately I noticed that Skype has started (about 10 years too late) to
support Linux in a way that is not so ridiculous, so I decided to
set it up in as sandboxed/crippled/blinded/impotent form as possible
for those moments when it is the only option left to me. I found [this
blogpost](https://spwhitton.name/blog/entry/firejailskype/) and built
on that, to have a user-friendly wrapper for running skypeforlinux in
a customized firejail.

Installation
------------

* Ensure `firejail` is installed with a profile for `skypeforlinux` (the
  latest Debian packages include the profile by default).

* You *must* hack the skypeforlinux shellscript wrapper (as distributed
  as part of skypeforlinux) so that it doesn't background the invocation
  of the executable (e.g. "nohup XX &" -> "XX"). If you prefer not to
  edit the upstream wrapper and to work around it by using pgrep/wait in
  `jailscript` instead, then feel free (but then it's a lot of extra
  work instead of a 1-line micro-edit). Either way you *must* prevent
  the skype invocation from backgrounding or this wrapper will then kill
  it and exit.

* Copy or symlink `jailskype` into your $PATH.

* To change the window-size of the launched Xephyr screen edit the
  `xephyr-screen` value in the firejail config (which is
  `/etc/firejail/firejail.config` for me in Debian).

Quick Start
-----------

* `jailskype -h` for details.

License
-------

Copyright © 2017 Rowan Thorpe <rowan@rowanthorpe.com>

`jailskype` uses the GPLv3 license, check the `COPYING` file.

Any additional contributions are noted in the `AUTHORS.md` file.
