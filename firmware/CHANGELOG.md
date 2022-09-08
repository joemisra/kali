### 20220908 (Upcoming)
* Added: LFO Adjust now used on a per LFO basis in LFO editor, *currently LFO adjust will have no effect on main page*.
* Added: Pulsewidth for KaliOscillator, only used w/ square and polyblep square.
* Added: New Wavefolder mode for Kali mode, from recent daisysp update.
 
### 20220907 (0.9-14-a4282b2d)
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
