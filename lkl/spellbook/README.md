# Spellbook

A magic book which lets you cast spells.

## Authorship

- [Two Lemons (legokidlogan)](https://github.com/legokidlogan):
    - Scripting, design
- [Shrooblooms](https://github.com/shroobloom):
    - Assorted design decisions
    - Saw Blast icon

## Notice

This library was intended to come with a few base spells to serve as examples and give some bare-minimum combat capabilities. However, part of the goal of this library is to give people a framework to make their own special, creative, unique spells; and GMod players take mountains when you give them inches. As such, the only public spells are now bare-bones examples incapable of dealing damage. If you were looking for easy, abuseable spells, this is not the place for you; you must design your own spells, and try to make them fun and balanced.

If, however, you are well-versed in writing starfall code, and you would like to make some fun and fair spells, then welcome on in, fellow wizard! Go forth, craft thine spells!

## Usage

Simply place the [custom_spellbook.txt](/lkl/spellbook/custom_spellbook.txt) script and use its Global Radial Menu (GRM) to navigate through spells.
- The script is a template, intended for you to make a copy elsewhere and edit it to your liking.
- By default, GRM's are opened by holding the COMMA key. However, [custom_spellbook.txt](/lkl/spellbook/custom_spellbook.txt) changes it to R for your convencience.
- Spells are displayed in the spellbook's radial menu, click on one to select it.
    - Cooldowns and active statuses are also displayed here, and in the book itself.
- Press `spellbook.SUMMON_KEY` (middle mouse by default) while the radial menu is open to (de)summon the spellbook.
- While summoned, the spellbook will only open while holding the `spellbook.WEAPON_CLASS` swep.
    - By default, this is `none`, from the [Empty Hands Swep](https://steamcommunity.com/sharedfiles/filedetails/?id=245482078) addon.

Spells, and how to cast them:
- Spells are primarily casted/activated by left clicking while the spellbook is open.
- There are four main types of spell: **Instant**, **Charged**, **Channeled**, and **Passive**.
    - **Instant** are self-explanatory. They cast instantly upon clicking.
    - **Charged** spells cast when you left go.
        - The charge progress can be seen at the top of the spellbook's right page.
        - The longer a spell is charged for, the stronger it will be and the more mana it will consume.
        - Some charged spells have a minimum charge requirement, shown as a darkened part of the charge bar.
    - **Channeled** spells have a continuous effect and mana drain for as long as you hold left click.
    - **Passive** spells are toggled upon clicking, and remain active even when you select another spell.
        - Passive spells can also be toggled by right clicking them in the radial menu.
- Some spells use additional key inputs, detailed in their left-page description.
- Each spell has its own separate cooldown upon being casted, along with a (usually short) global cooldown to all spells.

How to read your spellbook:
- The left page shows your currently selected spell, its type, and description.
- The right page shows your current status:
    - The outermost circle (blue) shows your current mana, and previews mana consumption.
    - The middle circle (gray) shows the global cooldown status.
    - The innermost circle (spell color) shows the selected spell's cooldown status.
    - The top left circle indicates if a spell is active or not, primarily used by channeled and passive spells.
    - Charged spells will show the charge status at the top of the page.
        - If the spell has a minimum charge requirement, it will be shown with a darker gray color.

The [wizard_zone_example.txt](/lkl/spellbook/wizard_zone_example.txt) script can be used to define a wizard zone.
- A wizard zone is an easy way to mark an area for wizard combat.
- Place the chip. It will automatically use [boxSelector](/lkl/box_selector.txt) to let you determine the bounds.
- Aim at the first corner and press E to lock it in.
- Aim up and doin to choose the first corner's height, then press E.
- Repeat for the second corner.

## Customization

Many aspects of the spellbook and its spells can be adjusted to your liking.
To simplify the process, and not break your edits when updating this repo, it is recommended to make your own custom spellbook by copying the [custom_spellbook.txt](/lkl/spellbook/custom_spellbook.txt) template into your own folder and make edits to it from there.

Note that the `spellbook.SPELL_FOLDER` and `spellbook.SPELL_FOLDER_EXTRA` options can be changed to select your own spell folders. \
The custom spellbook template also changes the GRM open key to `R` and `spellbook.SUMMON_KEY` to `MOUSE_MIDDLE` by default for easier use in combat.

## Visual Aids and Examples

![Left and right pages](https://i.imgur.com/Rx2HfFg.png)
![Active spell](https://i.imgur.com/vYanGh1.png)
![Uncharged spell](https://i.imgur.com/7MqEJMI.png)
![Charging spell](https://i.imgur.com/5MF7Xyv.png)
![Mana-gaining spell](https://i.imgur.com/FLlMJ5d.png)
![Radial menu](https://i.imgur.com/ib40Cp9.png)

## Documentation

This project is split into three main realms: server, owner client, and non-owner client. \
The owner client handles spell selection, mana, cooldowns, etc, though the server can also add/remove mana and adjust cooldowns, among other things. \
For realm-specific functions, see [spellbook_sv.txt](/lkl/spellbook/spellbook_sv.txt), [spellbook_cl_owner.txt](/lkl/spellbook/spellbook_cl_owner.txt), and [spellbook_cl.txt](/lkl/spellbook/spellbook_cl.txt). \
See the [spells/](/lkl/spellbook/spells) folder for existing spells to make your own from. \
Further details about the four amin spell classes can be found in their respective files.

Hooks:

- `LKL_Spellbook_LibraryLoaded()`
    - All realms.
    - Called when the base spellbook library has finished loading.
    - After this, global spellbook functions exist.
    - Spells are not yet loaded.
- `LKL_Spellbook_AllSpellsLoaded()`
    - All realms.
    - Called when all spells have been loaded.
    - After this, spells have their IDs.
- `LKL_Spellbook_LoadingComplete()`
    - All realms.
    - Called when everything is fully loaded and ready to go.
- `LKL_Spellbook_PlayerLoaded( ply )`
    - Server realm.
    - Called when a player finishes loading the spellbook.
- `LKL_Spellbook_Spell_IconLoaded( spellID )`
    - CLIENT realm.
    - Called when the icon of a spell has finished loading.
- `LKL_Spellbook_OnSpellSelected( prevSpell, curSpell )`
    - All realms.
    - Called when a spell is selected.
- `LKL_Spellbook_OnSetSummoned( state )`
    - All realms.
    - Called when the spellbook is (de)summoned.
- `LKL_Spellbook_OnOpenChanged( open )`
    - All realms.
    - Called when the spellbook is opened/closed.
    - Desummoning the book also closes it.
- `LKL_Spellbook_AnimateSpellbook( bookPos, bookAng, frac )`
    - CLIENT realm.
    - Called from within `renderoffscreen`, for if you need to attach something to the spellbook clientside.
- `LKL_Spellbook_SpellbookHolosCreated( info, bookHolos )`
    - CLIENT realm.
    - Called when the spellbook's holos have been created.
    - `info` contains the base holos by name, and some additional variables. See `spellbook.getSpellbookHoloInfo()` for more details.
    - `bookHolos` is a list of all book holos. Insert into this if you are adding more holos to the book.
- `newPos, newAng, newFrac = LKL_Spellbook_OverrideBookPosAng( pos, eyeAng, frac, openCloseEndTime, isFirstPerson )`
    - All realms.
    - Called whenever `spellbook.calcBookPosAng()` is called, allowing you to override the values.
    - Note that `openCloseEndTime` and `isFirstPerson` may be nil, and usually are on the server.
- `LKL_Spellbook_Spell_NameChanged( spellID, oldName, newName )`
    - All realms.
    - Called when `spell:setName()` is used.
- `LKL_Spellbook_Spell_DescriptionChanged( spellID, description, descriptionLines )`
    - All realms.
    - Called when `spell:setDescription()` is used.
    - `descriptionLines` is passed by reference, do not modify it.
- `LKL_Spellbook_Spell_ColorChanged( spellID, color, colorRGB )`
    - All realms.
    - Called when `spell:setColor()` is used.
    - `color` is in HSV.
    - `color` and `colorRGB` are passed by reference, be sure to `:clone()` them if you need to locally edit their values.
- `LKL_Spellbook_Spell_NameColorUnhoveredChanged( spellID, nameColorUnhovered )`
    - All realms.
    - Called when `spell:setNameColorUnhovered()` is used.
    - `nameColorUnhovered` is in HSV, and returns the effective color (as setting a hue of -1 will make it auto-use the spell's hue).
- `LKL_Spellbook_Spell_NameColorHoveredChanged( spellID, nameColorHovered )`
    - All realms.
    - Called when `spell:setNameColorHovered()` is used.
    - `nameColorHovered` is in HSV, and returns the effective color (as setting a hue of -1 will make it auto-use the spell's hue).
- `LKL_Spellbook_OwnerRespawned( respawnTime )`
    - All realms.
    - Called when the owner respawns.
- `LKL_Spellbook_OwnerDeath( deathTime )`
    - All realms.
    - Called when the owner dies.
- `LKL_Spellbook_Spell_AssociateModel( spellID, niceName, model, provider )`
    - All realms.
    - Called when a spell is associated with a model and niceName from some kind of prop buffer.
- `count = LKL_Spellbook_Spell_GetAssociatedModelCount( spellID, niceName, model, provider )`
    - SERVER realm.
    - For prop buffer providers to return the amount of available props they have for the given model.
- `LKL_Spellbook_Spell_AssociatedModelCountChanged( spellID, niceName, oldCount, count )`
    - All realms.
    - Called when the available count for a niceName changes for a spell.
- `LKL_Spellbook_OnSetVisibility( oldVis, newVis )`
    - All realms.
    - Called when spellbook visibility changes.
    - See `spellbook.setVisibility()` for details.
- `LKL_Spellbook_Spell_OnCast( spell, strength, castTime )`
    - All realms.
    - Called when a spell is casted.
- `LKL_Spellbook_Spell_OnSetActive( spell, state, toggleTime )`
    - All realms.
    - Called when a spell's active state is changed.
- `LKL_Spellbook_Spell_OnFumble( spell, reason, fumbleTime )`
    - All realms.
    - Called when a spell is fumbled.
