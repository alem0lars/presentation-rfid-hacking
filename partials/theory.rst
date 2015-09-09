theory
======

let's understand how the RFID stuff works..

.. code-block:: text

   RFID
   ┃┃┃┃
   ┃┃┗┗━ ID = identification
   ┗┗━━━ radio-frequency ⇒ wireless communication

----

frequencies
===========

+---------------------------+-----------------------+-------------------------+
| Name                      | Distance              | Frequency               |
+===========================+=======================+=========================+
| **LF** (low frequency)    | ``< 1m`` (``~ 0.5m``) | ``120KHz`` - ``140KHz`` |
+------------+--------------+-----------------------+-------------------------+
| **HF** (high frequency)   | ``1m`` - ``3m``       | ``13.56MHz``            |
+------------+--------------+-----------------------+-------------------------+
| **UHF** (ultra-high freq) | ``~ 9m``              | ``860MHz`` - ``960MHz`` |
+---------------------------+-----------------------+-------------------------+

we will focus on low frequency badges (they are the most vulnerable)

legacy ``125KHz`` is still in place at around ``80%`` of devices!

----

cards technologies
==================

+-------------+-------------+-------------------------------------------------+
| technology  | years       | notes                                           |
+=============+=============+=================================================+
| magstripe   | late 1960s  | - strip would prematurely wear out              |
| cards       |             | - not really used nowadays                      |
+-------------+-------------+-------------------------------------------------+
| wiegand     | late 1970s  | - used quite frequently nowadays                |
| cards       |             |                                                 |
+-------------+-------------+-------------------------------------------------+
| proximity   |             | - there is a built-in antenna ⇒ two-side        |
| cards       |             |   communication                                 |
|             |             | - but still no memory is available              |
+-------------+-------------+-------------------------------------------------+
| smart cards | early 2000s | - they have a micro-controller (intelligence)   |
|             |             | - and some memory (storage)                     |
+-------------+-------------+-------------------------------------------------+

----

cards technologies
==================

regardless of the card technology, usually the **wiegand protocol** is used

http://blog.opensecurityresearch.com/2012/12/hacking-wiegand-serial-protocol.html
https://www.supremainc.com/en/node/754
http://www.locksmithledger.com/article/12067684/access-card-migration-magstripe-to-smart-card

----

wiegand-*
=========
1.
A specific reader-to-card interface
2.
A specific binary reader-to-controller interface
3.
An electronic signal carrying data
4.
The standard 26-bit binary card data format
5.
An electromagnetic effect
6.
A card technology

- **wiegand effect**: the core principle used by badges to store informations
- **wiegand wire**: "special" wire that has the **wiegand effect**
- **wiegand interface**: physical layer standard for those readers using the
  *wiegand effect*; used for connecting the card swiping mechanism to the rest
  of the system
- **wiegand protocol**: protocol used on *wiegand interfaces*

all of this stuff takes the name of the effect's discoverer: **John Wiegand**

----

wiegand effect
==============

**wiegand effect** is a linear magnetic effect

.. note::

  - Preambolo:

    - Il discorso che fara' sara' approssimativo in quanto qualitativo:
      non ci sono formule fisiche, quindi qualcuno potra' reputare il discorso
      totalmente inutile ma secondo me e' utile per dare una visione high-level
      su come funzioni il tutto

  - Spiegazione del principio fisico:

    - Inizialmente, il filo e' completamente ricotto.
    - In questo stato la lega e' "soft" nel senso magnetico, ovvero ha una
      elevata permeabilita' magnetica
    - ⇒ il metallo conserva solo una piccola campo residua quando il campo
      esterno viene rimosso

    - Durante la fabbricazione, per dare il filo sue uniche proprieta'
      magnetiche, e' sottoposto ad una serie di operazioni
    - Il risultato e' che la permeabilita' magnetica del guscio esterno e' molto
      piu' piccola di quella del nucleo interno
    - Questo guscio esterno bassa permeabilita' manterra' un campo magnetico
      esterno anche quando il fonte del campo viene rimosso

    - Il filo ora presenta un grande isteresi magnetica: se un magnete viene
      avvicinato al filo, il guscio esterno a bassa permeabilita' esclude il
      campo magnetico dal nucleo "soft" interno fino al raggiungimento della
      soglia magnetica.
    - Quando si raggiunge tale soglia, l'intero filo (sia il guscio esterno che
      quello interno) inverte la propria polarita'
    - Una volta che il filo ha invertito la propria polarita', la manterra'
      fino a quando non viene invertita nuovamente la polarizzazione

----

wiegand wire
============

- **wiegand wire** *has an intrinsic magnetic field*
  (thanks to the **wiegand effect**)

where can we use it?
--------------------

in magnetic cards ofc ``( ͡~ ͜ʖ ͡°)``

----

magnetic card
=============

- to build a **wiegand card**, place short pieces of **wiegand wires** disposed
  parallel to each other transversely of the card

.. image:: resources/wiegand-card-inside.png

------

tracks
======

.. image:: resources/wiegand-card-tracks.png

this series of embedded wires encodes:

- the "key" track
- the "clock" track

------

conventions
===========

+----------+----------------+-------+
| wire     | magnetic field | value |
+----------+----------------+-------+
| presence | presence       | ``1`` |
| absence  | absence        | ``0`` |
+----------+----------------+-------+

.. note::

   - La carta magnetica ha una serie di brevi pezzi di filo wiegand
     incorporati in essa
   - Una seconda traccia di fili fornisce una traccia di clock

   - La scheda viene letta passando attraverso una fessura del card reader
     di lettura, il cui campo magnetico fisso e una bobina sensore.
   - Poiché ogni pezzo di filo passa attraverso il campo magnetico,
     il suo stato magnetico ribalta, che indica un 1, e questo viene rilevato
     dalla bobina
   - L'assenza di un filo indica uno 0

   - Il risultante codice digitale protocollo Wiegand viene poi inviato ad un
     controllore host per determinare se per sbloccare elettricamente la porta

    The original Wiegand format had one parity bit, 8 bits of facility code,
    16 bits of ID code, and a trailing parity bit for a total of 26 bits.
    The first parity bit is calculated from the first 12 bits of the code and
    the trailing parity bit from the last 12 bits. However, many inconsistent
    implementations and extensions to the basic format exist.

    Many access control system manufacturers adopted Wiegand technology, but
    were unhappy with the limitations of only 8 bits for site codes (0-255) and
    16 bits for card numbers (0-65535), so they designed their own formats with
    varying complexity of field numbers and lengths and parity checking.

    The physical size limitations of the card dictated that a maximum of 37
    Wiegand wire filaments could be placed in a standard credit card, as
    dictated by CR80 or ISO/IEC 7810 standards, before misreads would
    affect reliability. Therefore, most Wiegand formats used in physical access
    control are less than 37 bits in length.

----

How a card is read
==================

.. image:: resources/how-card-is-read.png

Badge basics - Card elements
----------------------------

What's written in the badge?

It depends on the badge type.

Typically (almost everyone):

- **Card ID number**: 26-37 bit number
- **Facility code**: has nothing to do with authentication
- **Site code** (occasionally)

44 bits are stored in the card but only the card ID number is sent to the
reader. Typically other bits are padding or useless numbers. You have to see the
manual / datasheet to check which is the correct format, i.e. which bits of
44 stored are actually the card ID number and which ones are padding.

----

What to hack?
=============

typical RFID hacking tools are readers **which act as ``controllers``**, thus
**also performing the decoding operation**

this is how in general sniffers work: they decode the badges informations
