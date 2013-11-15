======
Ubuntu
======

-------------------------------
Changing Caps Lock into Control
-------------------------------

You could easily changing Caps Lock into Control by GUI or .Xmodmap until 13.04. 13.10 can't use this method. But no problem. We have alternate method.

Open ``/etc/default/keyboard`` and enter ``XKBOPTIONS="ctrl:nocaps"``. And reboot.

