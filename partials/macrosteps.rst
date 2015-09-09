macro steps
===========

1. steal badge informations
2. make a copy of the badge
3. use the cloned badge

typically the main problem is ``step 1``

----

step 3: use it
==============

**easiest step**

*nothing to say*

----

step 2: clone
=============

**very easy step**

..pick data collected from step 1 and:

1. find the hex version of the badge ID number
   (information stolen from step 1)
2. take a programmable card, put it near the proxmark tool (programmer)
   and type:

   .. code-block:: console

      $ lf hid clone <hex_version_of_the_badge>

   the card is now a perfect duplicate (i.e. clone) of the sniffed badge

----

step 1: steal
=============

**the most difficult step**

we need to *use a tool* to steal the badge ID number

----

wtf?
====

*atm RFID hacking seems really easy, isn't it?*

.. note::

   - Poca sensibilita' sull'argomento security
       - Le compagnie se ne fregano
       - E' un po come i primi giorni in cui uscivano i XSS
       - Solo quando sono usciti i primi CVE e hanno iniziato ad utilizzarli
         le societa' hanno iniziato a preoccuparsene
   - Fine prima parte, ora iniziano i dettagli
