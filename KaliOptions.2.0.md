**NOTE: this is Claude reading KaliOptions.cpp returning exact parameter ranges, these may end up changing, typically parameters are not removed, but some get added that may not be up to date.**



Here is the updated **Group 3** section in Markdown format with links to detailed descriptions:

---

### Group 3: CV Output Parameters  

| **Description**                | **Short Name** | **Min**    | **Max**          | **Step**     | **Default** | **Units** |  
|--------------------------------|----------------|------------|------------------|--------------|-------------|-----------|  
| [Waveform](#waveform)                      | Waveform       | 0          | WAVE_LAST - 1    | 1.0          | 0.0         | ' '       |  
| [Mode](#mode)                            | Mode           | 0          | 13               | 1            | 0           | ' '       |  
| [Oneshot (Single Cycle/Env)](#oneshot)     | Oneshot        | 0          | 1                | 1            | 0           | ' '       |  
| [Multiply L Time](#multiply-l-time)       | Numera         | 1          | 100              | 1            | 1           | ' '       |  
| [Divide Numerator](#divide-numerator)     | Denomi         | 1          | 1000             | 1            | 1.0         | ' '       |  
| [CV Out Polarity](#cv-out-polarity)       | Polarity       | 0.0        | 3.0              | 1.0          | 1.0         | ' '       |  
| [LFO Adjust (Varies)](#lfo-adjust)        | Adjust         | 0.0        | 1.0              | 0.0625       | 0.0         | '%'       |  
| [Offset %](#offset)                      | Offset         | -2048.0    | 2048.0           | 128.0        | 0.0         | '%'       |  
| [Attenuate %](#attenuate)                 | Atten          | 1.0        | 100.0            | 1.0          | 100.0       | '%'       |  
| [Phase Offset](#phase-offset)             | PhzOff         | 0.0        | 360.0            | 1.0          | 0.0         | 'o'       |  
| [Gate In Select](#gate-in-select)         | GateIn         | 0.0        | 2.0              | 1.0          | 1.0         | ' '       |  
| [Calibrated Offset](#calibrated-offset)   | OffCal         | -2048.0    | 2047.0           | 1.0          | 0.0         | ' '       |  
| [Calibrated Attenuation](#calibrated-attenuation) | AttCal         | 1.0        | 100.0            | 1.0          | 100.0       | '%'       |  
| [ADSR Attack](#adsr-attack)               | Attack         | 0.0        | 10.0             | 0.001        | 0.0         | ' '       |  
| [ADSR Decay](#adsr-decay)                 | Decay          | 0.0        | 10.0             | 0.001        | 0.0         | ' '       |  
| [ADSR Sustain](#adsr-sustain)             | Sustain        | 0.0        | 1.0              | 0.01         | 0.5         | ' '       |  
| [ADSR Release](#adsr-release)             | Release        | 0.0        | 10.0             | 0.001        | 0.2         | ' '       |  
| [EOC Action](#eoc-action)                 | Eschaton       | 0.0        | 7.0              | 1.0          | 0.0         | ' '       |  
| [EOC Action Target](#eoc-action-target)   | PGOAT          | 0.0        | 10.0             | 1.0          | 0.0         | ' '       |  
| [FM From](#fm-from)                       | FM From        | 0.0        | 10.0             | 1.0          | 0.0         | ' '       |  
| [FM Amount](#fm-amount)                   | FM Amt         | -100.0     | 100.0            | 1.0          | 0.0         | '%'       |  
| [AM From](#am-from)                       | AM From        | 0          | 10               | 1            | 0           | ' '       |  
| [AM Amount](#am-amount)                   | AM Amt         | -100.0     | 100.0            | 1.0          | 0.0         | '%'       |  
| [Load Preset](#load-preset)               | Load           | -1         | 32               | 1            | 0           | 'p'       |  
| [Save Preset](#save-preset)               | Save           | 0          | 32               | 1            | 0           | 'p'       |  

---

## Detailed Descriptions  

### Waveform  
Defines the waveform used for the CV output. The available waveforms are defined by the `WAVE_LAST` constant in the oscillator class.  

* Sin - Sine Wave
* Tri - Triangle Wave
* Saw - Saw Wave
* Ramp - Ramp
* [ ] - Pulse
* Ptri - Polyblep (Band-limited) Triangle
* PSaw - Polyblep (Band-limited) Saw
* P[ ] - Polyblep (Band-limited) Pulse
* Noise

### Mode  
Selects the operating mode for the CV generator, such as standard oscillation, one-shot, or other modulation modes.  
Here is the **LFO Mode Array** presented as a bulleted list with descriptions:

- **Core**  
  Standard low-frequency oscillation mode, generating continuous waveforms like sine, triangle, or saw.

- **S+H** *(Sample and Hold)*  
  Produces stepped random values by sampling input at regular intervals.

- **T+H** *(Track and Hold)*  
  Tracks the input signal until a trigger occurs, then holds the last value.

- **RandRst** *(Random Reset)*  
  Generates a random waveform that resets when triggered.

- **RndShp** *(Random Shape)*  
  Randomizes the shape or characteristics of the waveform for unpredictable modulation.

- **Jitter**  
  Adds subtle or chaotic random variations (jitter) to the waveform's timing or amplitude.

- **Osc** *(Oscillator)*  
  Operates like a basic oscillator for audio-rate modulation or frequency generation.

- **Glacier**  
  Extremely slow modulation rates, useful for very long, evolving LFO cycles.

- **Clocks**  
  Synchronizes the LFO to clock signals or divisions for precise timing.

- **Follow**  
  Follows the input signal's amplitude or shape, behaving like an envelope follower.

- **Sidechain**  
  Modulation responds dynamically to an external input, typically for ducking or rhythmic effects.

#### Disabled in 2.0 beta temporarily.

- **Envelope**  
  Functions as an ADSR envelope generator for shaping modulation over time.

- **Turing**  
  Generates semi-random patterns that loop or evolve based on a controllable degree of randomness.

- **Raw**  
  Outputs raw, unfiltered modulation signals for further shaping or processing.

- **MIDI**  
  Responds to MIDI signals, allowing control over LFO parameters like rate or shape through MIDI messages.  

### Oneshot  
When enabled, the waveform or envelope completes a single cycle and then stops. Useful for percussive modulation or envelope generation.  

### Multiply L Time  
Multiplies the LFO's base time value, effectively slowing down or speeding up the frequency.  

### Divide Numerator  
Divides the LFO or time period value, allowing for more precise control of timing divisions.  

### CV Out Polarity  
Sets the polarity for the CV output: unipolar, bipolar, or other predefined options.  

### LFO Adjust  
Provides fine-grained adjustment of the LFO amplitude or behavior, represented as a percentage.  

### Offset %  
Adds a DC offset to the CV output, shifting the waveform or modulation center.  

### Attenuate %  
Attenuates (scales down) the CV output amplitude by a percentage.  

### Phase Offset  
Offsets the phase of the waveform by a specified angle in degrees. Useful for aligning multiple LFOs.  

### Gate In Select  
Selects the gate input mode for triggering or resetting the LFO or envelope.  

### Calibrated Offset  
Adjusts the calibrated DC offset of the CV output for precise voltage control.  

### Calibrated Attenuation  
Attenuates the CV signal with calibration applied to ensure consistent behavior across outputs.  

### ADSR Attack  
Sets the attack time for the ADSR envelope generator.  

### ADSR Decay  
Sets the decay time for the ADSR envelope generator.  

### ADSR Sustain  
Sets the sustain level for the ADSR envelope generator.  

### ADSR Release  
Sets the release time for the ADSR envelope generator.  

### EOC Action  
Defines the "End of Cycle" action, specifying what happens when the LFO or envelope completes a full cycle.  

### EOC Action Target  
Sets the target for the EOC action, determining which parameter or output is affected.  

### FM From  
Selects the modulation source for frequency modulation (FM) of the CV output.  

### FM Amount  
Sets the amount of frequency modulation applied, as a percentage.  

### AM From  
Selects the modulation source for amplitude modulation (AM) of the CV output.  

### AM Amount  
Sets the amount of amplitude modulation applied, as a percentage.  

### Load Preset  
Loads a preset configuration from memory, based on the preset index.  

### Save Preset  
Saves the current configuration to a preset slot in memory.  

---

This layout clearly links each parameter in the table to its longer explanation below, making the document more user-friendly and organized.
