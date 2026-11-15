<p align="center"><img src="media/banner.jpg" alt="Paladin header art" width="100%"></p>

<img src="media/crest.png" alt="Paladin crest" width="96" align="left">

# ForeverPaladinHUD2

A paladin HUD for **World of Warcraft: Forever** (Interface 16001). This is the "2" build: everything in [ForeverPaladinHUD](../../../ForeverPaladinHUD) plus text fonts and formats, player / target / target-of-target frames and minimap options.

<br clear="left">

> **Status: version 2.0.0, not yet verified in the game client.** It passes a mocked-client test
> suite and boots cleanly in a simulated UI, but nobody has confirmed it in the real game. Expect
> rough edges and please report them.

## Install

1. Download this repository (Code -> Download ZIP) or clone it.
2. Put the folder in `World of Warcraft/_forever_/Interface/AddOns/` and make sure it is named exactly `ForeverPaladinHUD2`.
3. Restart the game or `/reload`. Type `/fpa2` to open the menu.

**It only starts on a paladin.** On a character of any other class it stays completely off: nothing
on screen, no events, nothing saved, and `/fpa2` just says which class it is for. So you can
leave every class's HUD enabled and only the right one runs.

Optional companions (the HUD works without them):
- **ForeverArt** - menu artwork: a painted backdrop, a header picture and a class crest.
- **ForeverFonts** - extra typefaces for the Text options.

Do not enable `ForeverPaladinHUD` at the same time: you would get two HUDs.

## How you use it

Open the menu with `/fpa2`. **While the menu is open** (and Lock is off), point at any bar or icon:

| Do this | Result |
|---|---|
| Hold **CTRL**, then hold the **left** mouse button | The item sticks to the cursor until you let go |
| Hold **CTRL** and roll the **mouse wheel** | Bigger or smaller |
| Hold **CTRL**, then hold the **right** mouse button and drag | Turns the item; it stays as you leave it |
| **Double-click the right** mouse button | Back to its original orientation |

Icons turn to any angle. Bars and the recent-actions row turn in quarter turns, because the
client cannot draw a status bar at an angle. With the menu closed nothing can be clicked or moved.
Because the mouse does all of this, the menu has no position, scale or orientation controls.
The **Help** tab in the menu explains all of it in game.

## What it shows

- **Mana bar** - mana. Its number has its own on/off switch.
- **Regeneration bar** - what is actually arriving per second.
- **Swing timer** - with its own Show switch, colour, spark, text mode, ticks and ready flash.
- **Combo points** - present but off by default; this class has none.
- **Recent actions** - the last four spells you cast, newest first.
- **Ability icons** - 38 abilities, switched on one by one. On cooldown an icon goes dark and
  grey, a clock sweep runs round it, and the time left counts down to the hundredth of a second in
  its bottom-right corner, drawn above everything else. It also flashes when ready, glows while its
  effect is on you, and dims or turns red when you cannot use it. Every one of these has a switch.
- **Unit frames** - player, target and target-of-target, with cast bar, buffs and debuffs. Opening
  the menu puts all three on screen (switched-off ones dimmed) so each can be moved and sized.
- **Text** - typeface, size, place and number format for each text, beside the thing it labels.
- **Map** - minimap shape, size and clutter.

On by default: Hammer of Justice, Judgement, Divine Shield, Divine Protection, Lay on Hands, Blessing of Protection.

## Look

- **40 colour skins**, plus **custom colours**: on the Skins tab click any colour in the strip for a
  colour wheel (with an Opacity slider for the see-through parts), then save your set under a name.
- **Menu artwork** (needs ForeverArt): High resolution, Low resolution or Off, and a choice of header picture.
- **Named profiles**: save, load and delete whole setups. Reset to default keeps them.

## Commands

| Command | What it does |
|---|---|
| `/fpa2` | Open or close the menu |
| `/fpa2 help` | Open the Help tab |
| `/fpa2 abilities`, `skins`, `profiles`, `text`, `frames`, `map` | Open that tab |
| `/fpa2 show` / `hide` | Whole HUD on or off |
| `/fpa2 energy|regen|swing|combo|trail on|off` | One element on or off ("energy" is the resource bar) |
| `/fpa2 cooldown on|off` | Countdown numbers |
| `/fpa2 lock` / `unlock`, `sticky`, `grid` | Editing aids |
| `/fpa2 skin <name>`, `save <name>`, `load <name>`, `reset` | Skins and profiles |

## Abilities

IDs are rank 1 and only a fallback: at login the addon asks the client for the ID behind each
spellbook name, so an icon follows the rank you actually know.

| Ability | Fallback ID | Default |
|---|---|---|
| Hammer of Justice | 853 | on |
| Judgement | 20271 | on |
| Divine Shield | 642 | on |
| Divine Protection | 498 | on |
| Exorcism | 879 | off |
| Lay on Hands | 633 | on |
| Blessing of Protection | 1022 | on |
| Blessing of Freedom | 1044 | off |
| Blessing of Sacrifice | 6940 | off |
| Holy Wrath | 2812 | off |
| Turn Undead | 2878 | off |
| Hammer of Wrath | 24275 | off |
| Cleanse | 4987 | off |
| Righteous Fury | 25780 | off |
| Divine Intervention | 19752 | off |
| Holy Light | 635 | off |
| Flash of Light | 19750 | off |
| Holy Strike | 678 | off |
| Consecration | 26573 | off |
| Holy Shock | 20473 | off |
| Holy Shield | 20925 | off |
| Repentance | 20066 | off |
| Divine Favor | 20216 | off |
| Seal of Righteousness | 20154 | off |
| Seal of Command | 20375 | off |
| Seal of the Crusader | 21082 | off |
| Seal of Light | 20165 | off |
| Seal of Wisdom | 20166 | off |
| Seal of Justice | 20164 | off |
| Blessing of Might | 19740 | off |
| Blessing of Wisdom | 19742 | off |
| Blessing of Kings | 20217 | off |
| Blessing of Salvation | 1038 | off |
| Blessing of Light | 19977 | off |
| Light's Vigil | 1310911 | off |
| Voice of Truth | 1310897 | off |
| Templar's Bulwark | 1311015 | off |
| Swift Judgement | 1310994 | off |

## How it stays within the client's rules

Public API only. No protected calls, no combat automation, no combat log, nothing written outside
its own SavedVariables. Values the client marks secret are handed to widgets and never compared or
calculated with; a cooldown the addon may not read simply shows no number.

## Known limits

- Not verified in game (see Status).
- Bars turn in quarter turns only; a turned icon's border, sweep and number stay upright. Unit frames move and size but do not turn.
- Glow, dim and red tint depend on what the client will tell an addon; in combat it may withhold
  those answers and the icon then stays plain.
- A few fallback spell IDs are unconfirmed on this client; the name lookup normally corrects them.

## How it is built

This file and the addon are generated: one generator produces all nine class HUDs from a single
reference, so they stay identical in behaviour. A mocked-client suite (722 assertions for this
class), a Lua 5.1 limits check and a simulated UI run are part of every build.
