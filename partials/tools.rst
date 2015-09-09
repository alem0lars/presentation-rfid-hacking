Tools available
===============

- Proxmark3
- Tastic RFID Thief

----

Proxmark3 - Intro
=================

RFID hacking swiss army knife: *read / simulate / clone RFID cards*

- Solution for step 1 (steal badge informations).
- There is also a *companion software*, that can be used with other tools too.
- Both tool and software are *the de-facto standards in RFID hacking*.

----

Proxmark3 tool - How it works
=============================

When you put the badge close to it, he will steal the badge informations.

.. image:: resources/proxmark3-standalone-mode-operation.png

----

Proxmark3 software - How it works
=================================

Available both as command-line tool and GUI application.

Some examples:

.. code-block:: text

   proxmark3> lf hid fskdemod
   #db# TAG ID: 98139d7c32 (5432)
   #db# TAG ID: 98139d7c32 (5432)
   #db# TAG ID: 98139d7c32 (5432)
   #db# Stopped

----

Proxmark3 - Links
=================

- `Proxmark official website`_
- `Proxmark forum`_
- `Proxmark commands reference manual`_
- `Buy Proxmark3v2`_

----

Proxmark3 - Problems
====================

- Short distance
- You can get caught

In real world, sometimes we need long distance tools.

----

Tastic RFID Thief
=================

- Device from BishopFox_.
- Solution for step 1 (steal badge informations).
- Captured informations can be used with proxmark software.

- 3 feet distance (more than proxmark tool!)
- You can put in your bag and pick info from near badges


.. _BishopFox: http://www.bishopfox.com/resources/tools/rfid-hacking
.. _`Tastic RFID Thief`: http://www.bishopfox.com/resources/tools/rfid-hacking/attack-tools
.. _`Proxmark official website`: http://www.proxmark.org
.. _`Proxmark forum`: http://www.proxmark.org/forum/index.php
.. _`Buy Proxmark3v2`: http://www.elechouse.com/elechouse/index.php?main_page=prod%20uct_info&cPath=90_93&products_id=2264
.. _`Proxmark commands reference manual`: https://github.com/Proxmark/proxmark3/wiki/commands
