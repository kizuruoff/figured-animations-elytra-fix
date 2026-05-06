> [Читать на русском](README.ru.md)

# Figured Animations — Elytra Leg Fix

A bugfix for the [Figured Animations](https://ko-fi.com/s/4b72daaa14) avatar
for the [Figura](https://modrinth.com/mod/figura) Minecraft mod.

⚠️ **Important Notice**

This fix is for the **old version** of Figured Animations.  
The author is currently working on a full remake (Version 2.0), so this fix may become outdated soon.

## The Bug

When flying with elytra, the player's legs would visibly tremble/shake.

## Root Cause

In `EZAnims_modified.lua` (lines 578–587), the `ob.walking.active` condition had two issues:

1. The `gliding` state was not excluded from the walking condition, so walking
   animations could activate mid-flight.
2. There was a fallback line: 

```lua
   or (ob.elytra.active and next(ob.elytra.list) == nil)
```

   This caused the walking animation to trigger whenever elytra was active
   but had no animations assigned — which is exactly what happens during normal flight.
   The author likely intended this as a safety fallback, but it backfired.

## The Fix

- Added `and not gliding` to the walking condition.
- Removed the elytra fallback line entirely.

Both changes are clean — no workarounds, no patches on top of broken logic.

## Files

The fix applies to both avatar variants (Default/Steve and Slim).
In both cases the file is named `EZAnims_modified.lua` — the filenames in this
repository include the variant suffix just for clarity.

## Credits

Original avatar by [chmonyasik](https://ko-fi.com/Y8Y5GI5G8/shop).
This repository contains only the fixed script, not the full avatar.
To use: replace the original `EZAnims_modified.lua` in your Figura avatar folder with the file from this repo. ("/figura/avatars/Figured_Animations_Default/libs/EZAnims_modified.lua" or "/figura/avatars/Figured_Animations_Slim/libs/EZAnims_modified.lua")




Licensed under the [MIT License](LICENSE).
