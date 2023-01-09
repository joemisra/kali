### 20230109 (0.999-1)
* Removed DC filter on output, was cutting more low end than intended.
* Fixed outputs 2R and 3R inversion.

### 20221209 (0.991-1)
* Range adjustments in Parvati (granular) modes to stop screen stuttering
* Feedback limit increased slightly in basic mode

### 20221130 (0.991)
* Extended meta2 range in basic mode (now divides 1 to 32) 

### 20221124 (0.991)
* Fixed an error where scaling + offset were applied in wrong order.

### 20221124 (0.99)
* Config version should now automatically detect and re-initialize settings once after an update.  These changes are getting much less frequent and will only happen if new config settings have been added.
* "OTHER SETTINGS" options page added after REVERB SETTINGS page - use left encoder on main screen to change page.
* Input width setting added to OTHER SETTINGS page (currently only 0% or 100%, range planned in future).
* Global envelope follower attack/release placeholders added to OTHER SETTINGS page.
* "Freeze Mode" added to OTHER SETTINGS page. This changes the freeze input and
  button to LFO phase reset, allowing you to use LFOs as envelopes etc. This does disable the freeze DSP effect.
 
### 20221110 (0.98)
* Re-added calibration, long-press right encoder when in LFO edit.
* Fixed inverted CV outs.
* Offset now changes in steps of 128 instead of 2.

### 20221019 (0.97-7-q997d8ba)
* Scale & Offset in LFO Editor

### 20221001 (0.97-6-q950b1df)
* Fix: For 'Shards' and 'Splat' mode, switched from ReadHermite to Read (delay
  read interpolation, was having glitch/stuttering issues with high meta1/meta2 values).

### 20220924 (0.97-3-qd46034f)
* Fix: Typo in parvati/shards mode.
* Trial feature: Internal CV out scaling (calibration, sort of).

### 20220918 (0.97-2-qe258fc9)
* Fixed: Chorus Meta1 knob was causing noise.
* Improved: Tweaked Chorus algorithm.

### 20220911 (0.97-1-aca219b9)
* Added: LFO Sidechain Mode - LFO amplitude is compressed/ducks in response to
  audio input.
* Fix: Increased knob smoothing for LFO Rate (was in some cases causing global multiplier to
  jump around = noisy LFO)

### 20220910 (0.96-2-a7ac710f)
* Changed: Sync improvements for LFOs when clocked by an external source.

### 20220908 (0.96-1-af371b80)
* Added: LFO Adjust now used on a per LFO basis in LFO editor, *currently LFO adjust will have no effect on main page*.
* Added: Pulsewidth for KaliOscillator, only used w/ square and polyblep square.
* Added: LFO Settings now save on exiting LFO Edit.
* Added: Options saved to flash incl lfo adjust & multiplier/divider.
* Added: LFO Raw mode (sends constant voltage, set by lfo adjust knob)
* Added: LFO Random Reset mode (lfo adjust knob = probability)
* Added: LFO Random Shape mode (lfo adjust knob = number of cycles before randomize)
 
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
