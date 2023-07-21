# starfall_scripts
This is a collection of [Starfall](https:/github.com/thegrb93/StarfallEx) scripts I've made for use in GarrysMod. \
You're welcome to use or edit these for making projects of your own, just don't claim them as your own, sell them, etc.

## DISCLAIMER
Since these are a bunch of small tools and not full-scale addons, don't be surprised if a few things break here and there. \
Most should be quite robust and have documentation for known issues and what not to do, but there'll always be stragglers, especially with my older work. \
Typically the libraries have lots of documentation, while full tools like dial_button usually have little more than config details. Some may improve over time.

Feel free to submit an issue request if there's a significant problem with anything, though I can't make any guarantees.

Take caution when using any scripts which have `----- VERY OLD -----` at the top, these are especially old and/or clunky. These will be rarely updated, if ever.

## Navigation
- The contents of this repository should go into `.../GarrysMod/garrysmod/data/starfall/`
    - Note that everything is inside the `lkl/` folder, so in effect all files here will start with `.../starfall/lkl/`
    - This is to ensure the scripts don't conflict with any of your personal files and are easier to update.
- Many of these scripts use each other as dependencies, so be sure to check the `--@include` details if you aren't downloading the entire repo.
- **Do NOT rename the starfall files!** Doing so will break the includes.
- Some subfolders, such as [lkl/utlity_chips_dir/](/lkl/utlity_chips_dir) will have their own README for additional info.
    - Said README files will be wrapped in a lua comment block to ensure they don't cause any havoc if you download the entire repo directly.
- *Most* scripts will put their configs at the top of their respecive SERVER/CLIENT blocks, and will specify the number of config areas it has.

## Best of the Bunch
Most of this repo is just small libraries, fringe tools, or repurposed projects, but here's the extra-special ones that I'd recommend looking at first:

### Libraries
- [SGUI](/lkl/sgui)
    - An entire GUI library made from within Starfall using [middleclass](https://github.com/kikito/middleclass).
    - There's currently a pr to [add vgui into Starfall itself](https://github.com/thegrb93/StarfallEx/pull/1413), though it may be a long time before it's merged. As such, I've been working on this in the meantime.
    - While most of it is complete, I'm still working on SGUI to add more classes, so expect updates and new features from time to time.
- [cl_check_permissions.txt](/lkl/cl_check_permissions.txt)
    - A dead-simple client permission checker to make your life easier and your code faster.
    - Apart from the initial setup, all you need to do is check the global `permissionSatisfied` boolean before performing a required action.
    - Handles all sorts of boilerplate to do the following for you:
        - Auto-check permission status when a player interacts with the chip's permission popup.
        - Bring up permission popup if needed when a player connects to the chip's HUD.
        - Safely handle non-base-addon permissions like how [CFC Servers]() adds `print.chat`, `print.console`, and `print.color` that normally don't exist.
        - Automatically prevent the chip from erroring when calling `sendPermissionRequest()` twice or not HUD-connected.
    - Behaves nicely with multi-file projects, using `addPermissions( tbl )` and `checkPermissions()` to build onto the current list.
    - Simple example usage can be found in [cl_check_permissions_example.txt](/lkl/cl_check_permissions_example.txt)
- [easy_bass.txt](/lkl/easy_bass.txt)
    - Drastically simplifies creation of Starfall [bass sounds](http://thegrb93.github.io/StarfallEx/#Libraries.bass) and fixes some issues they have.
    - Provides two functions: `easyBass.loadFile()` and `easyBass.loadURL()`
        - They have the same arguments as the built-in bass functions by the same names, though `flags` is replaced with a table of settings.
        - The settings auto-handle volume, pitch, and more, including some extra features that don't exist normally.
        - Full details can be found at the bottom of [easy_bass.txt](/lkl/easy_bass.txt), and example usage in [easy_bass_example.txt](/lkl/easy_bass_example.txt)
    - Any bass objects created by this will automatically have the GMod fade bug fixed, and will no longer be heard globally across the map.
- [middleclass_extras.txt](/lkl/middleclass_extras.txt)
    - Adds some global functions for use with the ever-wonderful [middleclass](https://github.com/kikito/middleclass) library, which [Starfall has built-in](http://thegrb93.github.io/StarfallEx/#Libraries.builtins.class).
    - Most notably, it extends the `obj:isInstanceOf( class )` function to work as `isInstanceOf( obj, class )` without knowing if `obj` is a middleclass object or not.
        - The idea is similar to how `obj:isValid()` and `isValid( obj )` works in glua/Starfall.
        - This has been done for a few other functions as well, check the script for details.
    - A must-have for any in-depth middleclass projects.
- [queue.txt](/lkl/queue.txt)
    - Creates the Queue class, for spacing out hefty and unreliable operations.
    - Each Queue is given a list of entries and a callback to perform on each entry.
        - Entries can be of any data type, allowing for a wide assortment of applications while still being much easier to set up and use than a coroutine.
    - Automaticaly stops processing once you get close to your CPU quota, and continues once safe again.
    - Has a multitude of ways to fine-tune your Queue for any use-case. Further documentation can be found in the script.
- [gcolors.txt](/lkl/gcolors.txt)
    - Globalizes a bunch of commonly-used colors for easy and efficcient access.
    - Gone are the days of having to define white, invisible, red, and so on over and over and over again.
        - Now it's as simple as `c_white`, `c_empty`, `c_red`, and so on. See the file for the full list.
        - Can easily be edited to add even more colors to your liking.
    - Has some utility functions as well, mostly just for special integration with other libraries and shortening net messages that use global colors.
- [color_scheme.txt](/lkl/color_scheme.txt)
    - A class for standardizing colors and managing custom themes.
    - Has an assortment of tools for getting colors, whether they be statically-defined, dynamic with functions and custom params, or automatically finding a color from an arbitrary object.
    - ColorSchemes can set each other as a baseline, letting them add or override colors while still having the base theme.
    - ColorSchemes have fallback colors for if something couldn't be found, which you can also override on a per-function-call basis.
- [easy_print.txt](/lkl/easy_print.txt)
    - Greatly simplifies and enhances the process of printing colored text.
    - Uses [color_scheme.txt](/lkl/color_scheme.txt) to standardize colors across projects and easily tweak things to your liking.
    - Provides functions for handling lists, key-value lists, bullet lists, [ulx](https://github.com/TeamUlysses/ulx)-style command targeting, and more.
    - Able to automatically get colorzied strings from *any* type, including custom middleclass objects and multi-colored strings for Vector and Angle.
    - Allows for quick printing of messages from server to specific clients without having to do the networking yourself.
- [chat_cmds.txt](/lkl/chat_cmds.txt)
    - A feature-rich library to simplify chat command creation.
    - Utilizes [easy_print.txt](/lkl/easy_print.txt) to colorize the commands, standardizing the appearance and improving readability.
    - Allows for aliasing commands, such as `/prefix reallylongcommand` and `/prefix rlc`
    - Automatically creates a command to list other commands and their aliases.
    - Arguments can be given names, marked as required/optional, and will automatically be enforced.
    - Fail cases can be handled separately from the execution function to keep things tidy and provide colored prints on what went wrong.
    - Has a built-in help command to list argument info and any custom details you provide for your commands.
- [sv_dosound.txt](/lkl/sv_dosound.txt) and [cl_dosound.txt](/lkl/cl_dosound.txt)
    - **Disclaimer**: `cl_dosound` will soon be refactored to use [easy_bass.txt](/lkl/easy_bass.txt), though it shouldn't change anything front-facing.
    - Lets you create special event-based sounds, consolidating the params into one place and reducing the playback function to a simple one-liner.
    - Sounds are given names, properties (which can also be functions), and can be placed into categories.
    - Sounds are set up once in a config table, but you can also override properties on a per-call basis.
    - A great and easy way to spice up a project with some sounds. Not ideal for a radio or music player, though.
    - `cl_dosound` is best for client-only projects and supports both game sounds and urls.
    - `sv_dosound` is for playing sounds serverside, removing the need for client perms and playing for all to hear.
        - If `cl_dosound` is included, the server version will automatically pass url sounds along to the client to handle, and can also use `doSoundOnClient()` to simplify networking for server-driven events.
- [hook_remote_fix.txt](/lkl/hook_remote_fix.txt)
    - Fixes a lot of bugs and general jankiness with [hook.runRemote()](http://thegrb93.github.io/StarfallEx/#Libraries.hook.runRemote).
    - Adds a bunch of extra tools for setting up groups and sending remote hooks to said groups individually for easy orginisation.
    - A small example of its main features can be found in [hook_remote_fix_tester.txt](/lkl/hook_remote_fix_tester.txt)
- [joint_manager.txt](/lkl/joint_manager.txt)
    - **Disclaimer**: While feature-rich, this project is old and not well documented.
    - Creates an angle-based bone system for groups of props.
    - Great for mechs, hydraulic arms, inverse-kinematics (IK) legs, and so on.
    - Bones are given names, heirarchy data, angle limits, IK info, and can be given custom orientation definitions (e.g. the 'forward' of a prop is now it's 'right' direction, etc. for easier alignment).
    - Special "holdable objects" can be specified for stuff like equipping and holstering a gun or sword.
    - You can create poses (list of bone manipulations) and animations (keyframes with poses, manips, holdable params., and functions).
    - Has built-in IK functions for up to four-segment limbs!
- [table_tracker.txt](/lkl/table_tracker.txt)
    - A streamlined tool for tracking, blocking, or otherwise modifying table read/write calls.
    - Great for debugging tables when they're getting modified in ways that don't seem possible.
- [targeted_input.txt](/lkl/targeted_input.txt)
    - Easily allows the server realm to listen for raw keyboard inputs of clients, turning a whole bunch of networking nonsense into just a hook and a few functions.
    - Lets you listen to only specific button inputs and specific players as needed.
    - Has additional functionality for key-combos, tap vs hold detection, and double-tapping.
- [input_generator.txt](/lkl/input_generator.txt)
    - Given a list of input names and types (which can be placed into separate groups), will automatically generate new wire inputs and outputs as you link things up.
- [e2_applytorque.txt](/lkl/e2_applytorque.txt)
    - Provides access to [Expression 2](https://github.com/wiremod/wire)'s version of [applyTorque()](http://thegrb93.github.io/StarfallEx/#Types.Entity.applyTorque), which has been [modified from base-game](https://github.com/wiremod/wire/blob/master/lua/entities/gmod_wire_expression2/core/compat.lua#L78).
    - Also provides tools to easily rotate an unfrozen entity to align with a specific angle using stable torque.

### Non-Library Tools
- [enhanced_first_person.txt](/lkl/enhanced_first_person.txt)
    - Lets you see yourself in first person, well and truly.
    - Uses calcview so your playermodel actually gets rendered, no janky fake models or duplicate rendering required.
    - Best used with [PAC3](https://github.com/CapsAdmin/pac3) to see yourself or force your `player movement` parts to apply without needing third person or the wonky pac camera.
- [true_crosshair.txt](/lkl/true_crosshair.txt)
    - Ever notice that high recoil guns tend to shoot away from the center-screen crosshair? Well, that's because the base-game crosshair is a lying little bugger, and there's actually a lot of things it gets wrong!
    - This script will give you a new crosshair that gets positioned to your player hitpos, meaning it will **always** be exactly correct for telling you where you're going to shoot, whether it be for weapons, toolgun, physgun, whatever.
    - A must-have tool when using [enhanced_first_person.txt](/lkl/enhanced_first_person.txt), as the default crosshair will be very unreliable otherwise.
- [undo_buffer.txt](/lkl/undo_buffer.txt)
    - Spawns a buffer of six auto-respawning props to put a stop-gap in your undo history, preventing you from accidentally undoing a large build, etc.
    - Works great on its own or when used in [utility_chips_dir](/lkl/utility_chips_dir)
- [utility_chips_dir](/lkl/utility_chips_dir)
    - Any chips placed in this folder will be auto-ran when you use [utility_chips.txt](/lkl/utility_chips.txt) to package all of your general-purpose utility scripts into one chip.
    - Great for reducing chip count, restarting your utilities with a single press, and spawning them without needing to use a dupe.
    - Usage and further information can be found in the [utility_chips_dir](/lkl/utility_chips_dir) README.
- [door_maker.txt](/lkl/door_maker.txt)
    - Lets you create practically **any** kind of door imaginable, and then some!
    - Doors can be rotating hinges, sliding doors, or physical sliding doors.
    - Lots of config options for making doors move, have sounds, etc.
    - Super easy to parent doors to objects (including other doors) or parent objects to a door.
    - Broadly, this makes objects that fluidly go from one position/orientation to another and back. Anything with just two states to move between, you can create it with this, like a bridge, drawer, window, whatever.
- [advanced_entity_marker.txt](/lkl/advanced_entity_marker.txt)
    - Recreates the functionality of the [Wiremod](https://github.com/wiremod/wire) AdvEntMarker, but compresses multiple marker lists into one chip, and has several quality of life improvements.
- [sh_propinfo.txt](/lkl/sh_propinfo.txt)
    - If your server doesn't have [Customizable Prop Info](https:/github.com/legokidlogan/customizable_prop_info) but you need accurate info of whatever you're looking at to make building easier or to find the owner of a prop, why not try the addon's predecessor?
    - Take this with a grain of salt, though. Because of the addon, *I will not be maintaining the Starfall version anymore*.
    - This requires [sv_propinfo.txt](/lkl/sv_propinfo.txt) and [cl_propinfo.txt](/lkl/cl_propinfo.txt) as well.
- [hitmarkers.txt](/lkl/hitmarkers.txt)
    - By the same token, here's the predecessor to [Customizable Hitmarkers](https:/github.com/legokidlogan/customizable_hitmarkers)
