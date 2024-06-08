# DeckCustomer

DeckCustomer allows you to composite deck images using Hearthstone's Copy Deck clipboard format or DeckCustomer's supported format **without** any deck restrictions.
* Version: 1.0

# How to use
* Write a ``<deckname>.txt`` file and put into ``inputs`` folder. Each ``.txt`` file will represent a deck. More details in section **Deck format**.
* Additionally, you can create a folder named ``inputs/custom_<deckname>`` and put in any images as references to support your deck images' info.
* Modify ``config.ini`` to customize how you place the images. More details in section **Modifying config.ini**.
* Run ``deckCustomer.exe`` and wait for results. This will take a bit.

# Disclaimers and legal notes
* DeckCustomer gets only additional data directly from these sites:
  * https://hearthstone.wiki.gg/
  * https://hearthstonejson.com/
* ``data`` contains Hearthstone assets, which shouldn't be used for any purposes besides promoting Hearthstone content. All Hearthstone assets are under Blizzard Entertainment's copyright.
* Most of deckbuilding processings are courtesy of https://github.com/hearthSim/python-hearthstone.
* Images in ``inputs`` folder are courtesy of https://hearthcards.net.
* There are already example files in ``inputs``. You may run ``deckCustomer.exe`` to see the results directly first.
* Instructions in the documentation may require **non-case-sensitive** inputs (either ``Standard`` or ``standard`` for example).
* DeckCustomer may also produce **illegal deck codes**. While they may be techincally usable in game client in unintended scenarios, **it is not recommended to use them in client**, as it violates Blizzard Entertainment's Terms of Uses and EULA, which may result your Blizzard account in suspension.

# Deck format
DeckCustomer supports two formats to help you write your ``.txt`` file(s).
## Hearthstone's Copy Deck format
When you use Copy Deck feature from Hearthstone client, it should result in a clipboard like this:
```
### Custom Priest2
# Class: Priest
# Format: Standard
# Year of the Pegasus
#
# 1x (1) Anduin's Gift
```
DeckCustomer will recognize these line patterns:
* Line that starts with ``### `` represents **Deck name**.
* Line that starts with ``# Format: <format>`` represents **Deck format**.
  * You can modify ``<format>`` into either ``Standard``, ``Wild``, ``Classic``, ``Twist``.
* Line that starts with ``# <number>x `` represents a **deck card** with ``<number>`` as total count.
  * If there is a ``(<cardcost>)`` pattern right after, it is ignored.
  * These similar patterns are also recognizeable as **deck cards**:
    * ``<number>x  <cardname>``
    * ``# <number>x <cardname>``
   * If the mentioned patterns also have space characters at the start (excluding the one right next to ``#``), it is considered **sideboard cards** instead:
     * ``  <number>x  <cardname>``
     * ``# <number>x <cardname>``
    * ``<cardname>`` can also be modified to target the desired card more precisely into the following values:
      * **dbfId** of the card. Example: ``110441``
      * **String id** of the card. Example: ``TOY_330t6``
      * **Hearthstone Wiki's page name** of the card. Example: [``Zilliax Deluxe 3000 (Virus art)``](https://hearthstone.wiki.gg/wiki/Zilliax_Deluxe_3000_\(Virus_art\))
## DeckCustomer's unique format
DeckCustomer also comes up with a unique format you can write, like this:
```
[BASIC]
HERO = Archmage Khadgar
FORMAT = Twist
DECKNAME = Khadgar

[DECK]
1x Arcane Intellect

[E.T.C., Band Manager]
1x Fireball
```
DeckCustomer will recognize these line patterns:
* Line with ``HERO = <cardname>`` represents **Hero portrait**.
* Line with ``FORMAT = <format>`` represents **Deck format**.
  * You can modify ``<format>`` into either ``Standard``, ``Wild``, ``Classic``, ``Twist``.
* Line with ``DECKNAME = <deckname>`` represents **Deck name**.
* Line ``[DECK]`` informs DeckCustomer that they are going to read lines that represent **deck cards**.
* Line that starts with ``# <number>x `` represents a **deck card** with ``<number>`` as total count.
  * If there is a ``(<cardcost>)`` pattern right after, it is ignored.
  * These similar patterns are also recognizeable as **deck cards**:
    * ``<number>x  <cardname>``
    * ``# <number>x <cardname>``
  * If the mentioned patterns also have space characters at the start (excluding the one right next to ``#``), it is considered **sideboard cards** instead:
    * ``  <number>x  <cardname>``
    * ``# <number>x <cardname>``
  * ``<cardname>`` can also be modified to target the desired card more precisely into the following values:
    * **dbfId** of the card. Example: ``110441``
    * **String id** of the card. Example: ``TOY_330t6``
    * **Hearthstone Wiki's page name** of the card. Example: [``Zilliax Deluxe 3000 (Virus art)``](https://hearthstone.wiki.gg/wiki/Zilliax_Deluxe_3000_\(Virus_art\))
* Line ``[<cardname>]`` informs DeckCustomer that they are going to read lines that represent **sideboard cards** inside ``<cardname>``.
  * The lines below this will also add into ``<cardname>``'s existing sideboard if it already contains cards from ``[DECK]`` patterns.
 # Modifying config.ini
 * ``[TILE_VIEW]``
   * ``MAX_UNIQUE_DECK_CARDS_PER_COLUMN``: Number of unique card tiles per column (including sideboard cards). When a column's total reaches this number, a new column is created to the right.
   * `` MAX_CUSTOM_CARDS_PER_COLUMN``: Number of images from ``inputs/custom_<deckname>`` folders per column in the final image. When a column's total reaches this number, a new column is created to the right.
   * ``CUSTOM_CARDS_MIN_HEIGHT``: Minimum pixels of custom images. DeckCustomer won't shrink those images below that height threshold.
   * ``OUTPUT``:
      * = ``PNG``: Save deck composition as ``.png`` file (with Hearthstone-like visual, deck hero portrait, total number of cards, total dust to craft)
      * = ``JPG``: Same as ``PNG`` but as ``.jpg`` file
      * = ``RAW_PNG``: Save deck composition as ``.png`` file but with only card tiles and custom images behind a transparent background.

# Changelogs
* 1.0: Initial commit.