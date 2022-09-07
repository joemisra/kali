### 20220907
* Changed: LFO edit now has multipliers & dividers, multiplies by default.
* Changed: LFOs no longer have an automatic multiplier assigned (used to go in
  sequence x1,x2,x3,x4,x5,x6)
* Fix: LFO multiplier in bottom left corner was only showing up in basic mode,
  now will be present in all modes.

### 20220903
* Tweaked 'freeze' response in all modes.
* Adjusted clock sync to reflect multiplier displayed on main page.
* Adjusted kali mode levels to be more uniform between submodes.
* Small oled viz changes in parvati mode.
* Adjusted some constants for granular algorithms in parvati mode.
* Main page settings like clock div, reverb etc now save when you leave that
  page.
* Added some optimizations for parvati mode to reduce division operations.
* When kali is externally synchronized, delay link/unlink now adjusts 
  correctly.
