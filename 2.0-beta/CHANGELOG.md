### 2025-03-10
- Chorus and Knuth should function again too.
- Chorus now uses P1, P2 parameters: P1 is mod frequency, P2 is mod depth.

### 2025-03-06
- Clock modes are now consistent with each other (PPQN in config applies to all modes).
- In this beta, press down on both encoders to save settings.
- Default PPQN is 24 because of MIDI.

### 2025-02-24
#### v2 Beta
- **Granulish**: Experimental 'chorus' engine - delay line with modulatable playhead that wants you to modulate it.
- **Granulish**: Experimental 'knuth' engine - delay line with modulatable playhead that has internally synced modulation (only partially finished, depth is fixed).
- Trying a different min delay / max delay setup; in most modes, the value is in seconds.
- Adding MIDI CC input (not linked to any parameter yet, but there's a MIDI page now for debug info).

New delay modes respond in useful ways when time is slowly modulated.  
Feedback can explode but is also a good one to experiment with.  
Knuth has a different effect the larger the delay is; try a range.

There is a bug with ping pong unlinked mode I did not track down yet. Just avoid it; it should not crash anything.

### 2025-02-19
- More clock tweaks.
- **Fix**: If sync mode = external and the clock input drops, it will attempt to continue that rate until it starts again (or until you switch to another sync mode).
- **Fix/New**: Tap tempo sort of works if sync mode = external.
- **Bug**: On reboot, if sync mode = external and you aren't sending sync yet, try tap tempo or start sending it a pulse clock.
- Kali now understands internal sync and external Eurorack sync are often going to be slower than MIDI's 24 PPQN. These will be separate settings. MIDI will always be 24 PPQN; internal and external will be configurable.

### 2025-01-29
- More clock tweaks.
- **Fix**: If sync mode = external and the clock input drops, it will attempt to continue that rate until it starts again (or until you switch to another sync mode).
- **Fix/New**: Tap tempo sort of works if sync mode = external.
- **Bug**: On reboot, if sync mode = external and you aren't sending sync yet, try tap tempo or start sending it a pulse clock.
- Kali now understands internal sync and external Eurorack sync are often going to be slower than MIDI's 24 PPQN. These will be separate settings. MIDI will always be 24 PPQN; internal and external will be configurable.

### 2025-01-26
- Rewrote clock stuff - must select internal or external at the moment. MIDI clock untested; will check soon.
- Distortion in all modes; can choose distortion target: none, dry, wet, dry+wet.
- Distortion trim parameter to scale the gain down (since distortion making things louder is often desired).
- Be aware distortion applied to wet signal can make feedback go insane.
- Min/max delay time can be changed.
- Trying log scaling for delay time.
- Meta2 changes in simple/pingpong have fewer artifacts.
- Meta1 in simple/pingpong is now `ldelay + (ldelay * 0% - 33%)` and can do nice pitch bends.
- Feedback can be 100%, which works like a looper.
- A couple debug screens with scary numbers in there for me; don't be alarmed.

**Note**: This has some half-finished stuff. The above is worth sharing early. I don't think anything is going to lock up, but don't sit too far away from the feedback knob.

### 2024-10-09
- Tuned knob smoothing (was suffering from noise in the last beta).
- Meta1 in normal delay modes now has a range of +0-10% of left delay time (fine adjust/bend effects).
- High feedback 99.9% - much less noisy over time.

### 2024-04-15
- DAC input and output gain are back on.
- Tuned some slew rates on knobs.
- Added a check to return from the OLED callback if it interrupted AudioCallback (?).

**Note**: For anyone that has not installed v2 beta yet: To initialize the new settings format, hold both SYNC and FREEZE buttons as you power up Kali. Otherwise, you will get the dreaded undefined behavior.

### 2024-02-19
- Adjusted slew times for main knobs: L Time and R Time have been slewed more, Cutoff has been slewed more, Meta 2 has been slewed less.
- Began preset system (not 100% working yet).
- Will save/load LFO options. Press the FREEZE button to save.

#### Things to Test:
- On first boot, make sure to hold SYNC and FREEZE buttons.
- Change some settings on each LFO. When you've done that, hit the FREEZE button to save. The display will stutter quickly as it saves, but audio should not be affected.
- Turn Kali off and on again. Make sure your saved settings have been loaded.
- Turn Kali off again, then hold down SYNC and FREEZE again and power up. Verify things went back to defaults.
- Use however you would normally use it. Try saving settings you like.

### 2024-01-18
- Trying to get to the bottom of freezing LFOs - removed code to update input and output gain, may be taking up too much time with TIM5.
- **Addition**: Freeze input+button will now also reset the phase of all things to 0 (restarts all of them so everything starts at the same spot).