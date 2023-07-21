--[[ comment block so this doesn't break your Starfall chips


# SGUI
An entire GUI library built from the ground up inside of Starfall, using [middleclass](https://github.com/kikito/middleclass). \
Most of the big features/classes are complete, though I'm currently working on adding more, such as TextEntry. \
SGUI makes heavy use of [color_scheme.txt](/lkl/color_scheme.txt) to standardize its colors and make it easy to use custom themes.

**This README is a WIP**, expect to see some documentation and example code here in the future. \
In the meantime, [sgui_tester.txt](/lkl/sgui_tester.txt) has an assortment of code snippets to toy around with. It will be removed once this README is complete.

## Upcoming Features
A small list of features coming soon to SGUI. \
The library is quite robust currently, but I'd recommend waiting for these features to be completed if any look useful to you.
- `TextEntry`: a Panel for the user to type inside of.
    - Ideally, this will include selection highlighting, copy and paste (can't access computer clipboard though), ctrl + a, undo and redo, shift + arrow selection, and view scrolling/clipping. All of which has to be made from scratch, as pulling from the chat window would be clunky and risk accidental message sending.
    - For the sake of my sanity, I currently plan on not allowing TextEntry to be multi-lined.
- `FancyLabel`: a Label which will rip code from [htext.txt](/lkl/htext.txt) to allow for multi-line Labels with line wrapping and multiple simultaneous colors and fonts.
- `FancyRevealingLabel`: the same as above, but for [rhtext.txt](/lkl/rhtext.txt), which reveals text character-by-character and plays sound accordingly.
- A cross-session config system similar to client convars, editable both by code and by specialized Panels.
- A dedicated, configurable button to bring up the mouse cursor.
    - Currently, the only decent options for this in-game is opening chat or using F3, the latter of which instantly closes when you left click.
    - This will use the afforementioned convar-style system to determine the button, with `RALT` being the default.
 \
 \
--]]
