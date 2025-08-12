# Kali Firmware Manual
*Created with assistance from Claude 4 Sonnet*  
*https://claude.anthropic.com/chat/...*

## Overview

Kali is a powerful delay and modulation system built for the Daisy platform. At its core, Kali combines sophisticated delay algorithms with an extensive 6-oscillator LFO system, offering everything from classic delays to granular processing and complex modulation routing.

### Key Features

- **Multi-Algorithm Delay Engine**: 15+ delay modes including basic delays, ping-pong, chorus, granular processing, resonators, and waveshaping
- **6-Oscillator LFO System**: Independent LFOs with multiple waveforms, sync modes, and modulation capabilities
- **Advanced Clock System**: Internal/external/MIDI clock sync with phase-locked loop outputs
- **Extensive Modulation**: Cross-modulation between LFOs, envelope following, MIDI control, and external CV patching
- **Real-time Control**: Dedicated knobs for all major parameters plus CV inputs
- **Visual Feedback**: OLED display with waveform visualization and parameter monitoring

### Signal Flow

```
Input → Delay Processing → Filter → Output
  ↑           ↑              ↑
  └─ LFO Modulation ────────┘
  └─ Clock/Sync System
  └─ MIDI/CV Control
```

The system processes audio through selectable delay algorithms, with extensive modulation from the 6-LFO system. A sophisticated clock system provides sync capabilities, while real-time visual feedback keeps you informed of all parameters.

---

## Complete Options Reference

This section provides a comprehensive reference for every option in Kali, organized by category with explanations of their purpose and typical use cases.

### Global Options Reference

| Option | Range | Default | Purpose |
|--------|--------|---------|---------|
| **LFO Rate Multiplier** | 1-255 | 24 | Global speed control for all LFOs. Allows quick tempo changes without adjusting individual LFO rates. Useful for live performance tempo shifts. |
| **Left Clock PPQN** | 2-127 | 24 | PPQN setting for left clock output. Determines subdivision: 4=quarters, 8=eighths, 16=sixteenths, 24=MIDI standard. Essential for syncing external gear. |
| **Right Clock Rate Multiplier** | 1-16 | 1 | Clock division/multiplication for right output relative to left. Creates polyrhythmic clock relationships for complex sequencing setups. |
| **External CV Clock PPQN** | 1-127 | 1 | Defines pulses-per-quarter-note when syncing to external CV clock. Must match your external clock source for proper sync. Critical for Eurorack integration. |
| **Sync Mode** | 0-2 | 0 | Master clock source selection. 0=Internal (self-clocked), 1=External CV (Gate 1), 2=MIDI Clock. Determines what drives the entire timing system. |
| **Sync Button Mode** | 0-1 | 0 | Gate Input 1 behavior. 0=Clock trigger input, 1=Reset all LFO phases. Switch based on whether you need clock sync or manual reset control. |
| **Freeze Button Mode** | 0-1 | 1 | Gate Input 2 behavior. 0=Freeze delay (stops writing, mutes wet), 1=System reset. Choose based on performance needs. |
| **Use Allpass** | 0-1 | 1 | Enables allpass filtering in feedback path. Creates smoother, more musical feedback. Disable for harsher, more aggressive feedback tones. |
| **Reverb Wet Send** | 0-50 | 0 | Amount of delay output sent to reverb (currently disabled). Reserved for future reverb implementation. |
| **Reverb Dry Send** | 0-50 | 0 | Amount of dry input sent to reverb (currently disabled). Reserved for future reverb implementation. |
| **Reverb Feedback** | 50-99 | 85 | Reverb feedback amount (currently disabled). Reserved for future reverb implementation. |
| **Reverb Damp** | 1000-19000 Hz | 7500 | Reverb damping frequency (currently disabled). Reserved for future reverb implementation. |
| **Input Gain** | 0-255 | 215 | Input gain control. 215=0dB reference. Lower values reduce input sensitivity. Adjust if input is too hot or too quiet. |
| **Output Gain** | 0-255 | 255 | Output gain control. 255=maximum output. Reduce if output is clipping or too loud for your system. |
| **Input Width** | 0-1 | 1 | Stereo processing mode. 0=Sum to mono, 1=True stereo. Use mono for centered processing, stereo for width effects. |
| **Invert Encoders** | 0-1 | 0 | Reverses encoder direction. Enable if clockwise feels like it should go the other direction. Hardware-dependent setting. |
| **Enable Debug Info** | 0-1 | 1 | Shows debug pages and additional system information. Enable for troubleshooting or development work. |
| **Global Preset Load** | 0-32 | 0 | Load complete system state from preset slot. Recalls all settings, LFOs, and DSP configuration. |
| **Global Preset Save** | 0-32 | 0 | Save current system state to preset slot. Stores everything for instant recall. |

### DSP Options Reference

| Option | Range | Default | Purpose |
|--------|--------|---------|---------|
| **Mode** | 0-6 | 1 | Primary delay algorithm selection. Each mode has different sonic characteristics and use cases. See DSP Modes section for details. |
| **Parameter 1** | 0-100 | 0 | Algorithm-specific control. Function varies by DSP mode. |
| **Parameter 2** | 0-100 | 0 | Algorithm-specific control. Function varies by DSP mode. |
| **Parameter 3** | 0-100 | 0 | Algorithm-specific control. Function varies by DSP mode. |
| **Parameter 4** | 0-100 | 0 | Algorithm-specific control. Function varies by DSP mode. |
| **Distortion Algorithm** | 0-7 | 0 | Selects the distortion algorithm (see Distortion System). |
| **Distortion Amount** | 0-99 | 0 | Distortion intensity. |
| **Distortion Target** | 0-3 | 0 | Where distortion is applied: Off/Dry/Wet/Both. |
| **Distortion Trim** | 0.0-1.0 | 1.0 | Post-distortion trim to control level. |
| **Filter** | 0-2 | 0 | Selects FIR/IIR/Off for additional filtering. |
| **Delay Range** | 0-4 | 1 | Selects delay time range preset (see Delay Range Presets). |
| **DSP Preset Load** | 0-32 | 0 | Load DSP configuration preset. |
| **DSP Preset Save** | 0-32 | 0 | Save current DSP configuration. |
| **Distortion Algorithm** | 0-8 | 0 | Distortion type selection. Each algorithm provides different harmonic characteristics. See Distortion section for details. |
| **Distortion Amount** | 0-99 | 0 | Distortion intensity. Higher values = more harmonic content and saturation. Start low and increase to taste. |
| **Distortion Target** | 0-3 | 0 | Where distortion is applied. 0=Off, 1=Input only, 2=Output only, 3=Both. Affects tone and gain staging. |
| **Distortion Trim** | 0.0-1.0 | 1.0 | Post-distortion gain reduction. Compensates for distortion gain increase. Prevents clipping and maintains levels. |
| **DSP Preset Load** | 0-32 | 0 | Load DSP configuration from preset. Recalls mode, parameters, and distortion settings only. |
| **DSP Preset Save** | 0-32 | 0 | Save current DSP configuration. Stores DSP-specific settings for recall. |

### LFO Options Reference

| Option | Range | Default | Purpose |
|--------|--------|---------|---------|
| **Waveform** | 0-9 | 0 | Basic oscillator shape. Each waveform has different harmonic content and modulation character. |
| **LFO Mode** | 0-13 | 0 | Fundamental LFO behavior. Changes how the LFO responds to sync, triggers, and other inputs. See LFO Modes section. |
| **Oneshot** | 0-1 | 0 | Single-cycle mode. LFO runs once per trigger instead of continuously cycling. Useful for envelope-style modulation. |
| **Multiply L Time** | 1-100 | 1 | Primary frequency multiplier relative to left delay. |
| **Divide Numerator** | 1-1000 | 1 | Frequency divider/multiplier. |
| **Polarity** | 0-3 | 1 | Output voltage range. 0=Unipolar+, 1=Bipolar, 2=Unipolar-, 3=Inverted bipolar. Match to destination module requirements. |
| **Adjust** | 0.0-1.0 | 0.0 | Multi-function parameter. Changes meaning based on LFO mode. Often controls sensitivity, rate fine-tuning, or effect intensity. |
| **Offset** | -2048 to +2048 | 0 | DC offset added before scaling. Shifts the LFO center point. Useful for biasing modulation around specific values. |
| **Attenuate** | 1-100% | 100 | Output amplitude scaling. Reduces LFO depth without changing other parameters. Essential for subtle modulation. |
| **Phase Offset** | 0-360° | 0 | Phase relationship to other LFOs. Creates polyrhythmic patterns and stereo effects when LFOs are related. |
| **Trigger/Reset** | 0-2 | 0 | External trigger source. 0=None, 1=Gate 1, 2=Gate 2. Allows manual or clock-driven LFO reset. |
| **Offset Cal** | -2048 to +2047 | 0 | Hardware calibration offset. Fine-tunes CV output accuracy. Adjust if CV outputs don't match expected voltages. |
| **Attenuate Cal** | 1-100% | 100 | Hardware calibration scaling. Fine-tunes CV output range. Adjust if CV outputs don't reach full range. |
| **ADSR Attack** | 0.0-10.0s | 0.0 | Envelope attack time (Envelope mode). How quickly envelope rises when triggered. |
| **ADSR Decay** | 0.0-10.0s | 0.0 | Envelope decay time (Envelope mode). How quickly envelope falls from peak to sustain. |
| **ADSR Sustain** | 0.0-1.0 | 0.5 | Envelope sustain level (Envelope mode). Hold level while gate is active. |
| **ADSR Release** | 0.0-10.0s | 0.2 | Envelope release time (Envelope mode). How quickly envelope falls when gate released. |
| **EOC Action** | 0-7 | 0 | End-of-cycle behavior. What happens when LFO completes one cycle. Creates complex modulation interactions. |
| **EOC Target** | 0-10 | 0 | Which LFO receives end-of-cycle action. Enables one LFO to control another's behavior. |
| **FM Source** | 0-10 | 0 | Which LFO provides frequency modulation. Creates complex, evolving modulation patterns through cross-modulation. |
| **FM Amount** | -100% to +100% | 0 | Frequency modulation depth. Positive/negative values create different modulation characters. |
| **AM Source** | 0-10 | 0 | Which LFO provides amplitude modulation. Creates tremolo and dynamic modulation effects. |
| **AM Amount** | -100% to +100% | 0 | Amplitude modulation depth. Controls how much AM source affects output level. |
| **LFO Preset Load** | 0-32 | 0 | Load LFO configuration from preset. Recalls all settings for this specific LFO. |
| **LFO Preset Save** | 0-32 | 0 | Save current LFO configuration. Stores this LFO's settings for future recall. |

### Why These Options Exist

**Hardware Compatibility**: Options like encoder inversion and calibration settings accommodate different hardware implementations and manufacturing tolerances.

**Performance Control**: Preset systems, quick adjust knobs, and direct CV control enable live performance without menu diving.

**Integration Flexibility**: Multiple sync modes, PPQN settings, and polarity options ensure Kali works with any setup from standalone to complex modular systems.

**Creative Depth**: Cross-modulation options, multiple LFO modes, and algorithm parameters provide deep creative possibilities while maintaining intuitive operation.

**Future Expansion**: Reserved parameters and disabled options (like reverb settings) provide upgrade paths without requiring hardware changes.

**System Optimization**: Range settings, calibration options, and processing modes allow optimization for different use cases and signal levels.

---

## Hardware Interface

### Main Controls
- **8 Knobs**: Meta1, Meta2, LFO Rate, Time L, Time R, Cutoff, Feedback, Mix
- **2 Encoders**: Left (navigation), Right (parameter editing)
- **2 CV Inputs**: LFO Adjust, Delay Adjust (with dedicated knobs)
- **2 Gate Inputs**: Sync/Trigger, Freeze/Reset
- **Audio I/O**: Stereo input/output
- **6 CV Outputs**: 4 from LFOs 1-4, 2 from LFOs 5-6
- **2 Gate Outputs**: Phase-locked clock outputs
- **MIDI**: Full MIDI I/O with clock sync

### Display Navigation

Kali uses a sophisticated encoder interface with multiple interaction methods:

#### Encoder Actions
- **Turn**: Rotate encoder clockwise/counterclockwise
- **Click**: Quick press and release
- **Hold**: Press and hold (400ms+ triggers hold state)
- **Hold + Turn**: Turn encoder while holding down
- **Both Encoders Held**: Press and hold both encoders simultaneously

#### Left Encoder (Navigation)
- **Turn**: Navigate between main pages (LFO Edit → Options → DSP Edit → Presets → MIDI → Debug)
- **Click**: Context-dependent action:
  - **LFO Edit**: Toggle between editing LFO selection vs. parameter values
  - **DSP Edit**: Jump to Debug page
  - **Options**: Jump to DSP Edit page
  - **Debug**: Reset to factory defaults
- **Hold**: Access secondary functions (varies by page)
- **Hold + Turn**: Navigate through pages while in hold mode

#### Right Encoder (Parameter Control)
- **Turn**: 
  - **LFO Edit**: Navigate LFO parameters OR edit parameter values (depending on mode)
  - **Options/DSP**: Navigate options OR edit values (depending on edit state)
  - **Debug**: Select debug display type
- **Click**: Toggle edit mode (enables parameter value editing)
- **Hold**: Enter modulation editing mode (400ms+ hold time)
- **Hold + Turn**: Edit parameters while in hold mode

#### Special Combinations
- **Both Encoders Held**: Save current settings to memory
- **Right Encoder Hold + Freeze**: Reset all oscillators and system state

#### Page-Specific Behaviors

**LFO Edit Page:**
- Left encoder selects which LFO (1-6) to edit
- Right encoder navigates parameters and edits values
- Click left encoder to toggle between LFO selection and parameter editing
- Click right encoder to enter/exit value editing mode
- LFO Adjust knob provides direct access to current LFO's Adjust parameter

**Options/DSP Pages:**
- Left encoder navigates between pages
- Right encoder navigates options and edits values
- Edit state determines whether turning right encoder selects options or changes values

**Debug Pages:**
- Left encoder cycles through debug display types
- Right encoder changes debug information shown
- Left click resets to factory defaults
- Right click saves current settings

---

## Global Options

Access global options by navigating to the OPTIONS page with the left encoder.

### Clock and Sync Options

#### LFO Rate Multiplier (1-255)
Global multiplier applied to all LFO rates. Higher values increase all LFO speeds proportionally.

#### Left Clock Rate Multiplier (2-127, default: 24)
Sets the PPQN (Pulses Per Quarter Note) for the left clock output. Standard values:
- **4**: Quarter notes
- **8**: Eighth notes  
- **16**: Sixteenth notes
- **24**: MIDI standard (sixteenth note triplets)

#### Right Clock Rate Multiplier (1-16, default: 1)
Clock divider/multiplier for the right output relative to the left clock.

#### External CV Clock PPQN (1-127, default: 24)
Defines how many external CV pulses equal one quarter note when using external clock sync.

#### Sync Mode (Internal/External CV/MIDI)
- **Internal**: Use internal clock generator
- **External CV**: Sync to Gate Input 1
- **MIDI**: Sync to incoming MIDI clock

#### Sync Button Mode (Trigger/Reset)
Sets Gate Input 1 behavior:
- **0 (Trigger)**: Acts as clock input
- **1 (Reset)**: Resets LFO phases

#### Freeze Button Mode (Freeze/Reset)
Sets Gate Input 2 behavior:
- **0 (Freeze)**: Freezes delay buffer, mutes wet signal
- **1 (Reset)**: Resets system state

### Audio Options

#### Use Allpass (On/Off, default: On)
Enables allpass filtering in the feedback path for smoother, more musical feedback behavior.

#### Input Width (Mono/Stereo, default: Stereo)
- **0 (Mono)**: Sum inputs to mono before processing
- **1 (Stereo)**: Maintain stereo separation

#### ADC/DAC Attenuation (0-255)
Input and output gain control. 215 = 0dB, lower values reduce gain.

### System Options

#### Invert Encoders (Off/On)
Reverses encoder rotation direction (useful for different encoder types).

#### Enable Debug Info (Off/On)
Shows additional debug pages and information.

#### Preset Options
Load/Save global presets (0-32).

---

## DSP Options

Navigate to DSP EDIT page to access delay algorithm settings.

### Core DSP Settings

#### Mode (0-6)
Selects the primary delay algorithm:

**Basic Delays:**
- **0 - Basic**: Classic stereo delay
- **1 - Ping Pong**: Alternating left/right delay
- **2 - Unlinked**: Independent left/right delay times
- **3 - Ping Pong Unlinked**: Alternating delay with independent timing

**Modulated Delays:**
- **4 - Resonator**: MIDI-note tuned delays for harmonic effects
- **5 - Chorus**: Classic chorus with LFO modulation
- **6 - Knuth**: Crystal-style delay with sharp playback jumps

*Note: Additional modes (Granular, Waveshaping, etc.) are currently being rewritten and temporarily disabled.*

#### Delay Range Presets
- **Precision (0)**: ~1–500 ms
- **Studio (1)**: ~10 ms–2 s
- **Ambient (2)**: ~50 ms–8 s
- **Looper (3)**: ~100 ms–20 s
- **Experimental (4)**: ~1 ms–30 s

In external sync modes, the working delay range is dynamically adjusted to musical divisions of the incoming tempo.

#### Parameters 1-4 (0-100)
Algorithm-specific parameters that change function based on selected mode:

**Basic Mode:**
- **P1-P4**: Currently unused

**Chorus Mode:**
- **P1**: Modulation frequency multiplier (0-100)
- **P2**: Stereo spread amount (0-100)
- **P3-P4**: Currently unused

**Knuth Mode:**
- **P1**: Scan frequency ratio (0-100)
- **P2**: Modulation depth (0-100)
- **P3-P4**: Currently unused

**Resonator Mode:**
- **P1-P4**: Currently unused (MIDI note control)

### Distortion System

The distortion system in Kali is available across all delay modes and provides additional harmonic shaping. The distortion can be applied to the dry input signal, the wet delay output, or both.

#### Distortion Algorithm (0-7)
Eight distortion algorithms are available:

- **0 - Sine**
- **1 - Fold**
- **2 - Tanh**
- **3 - Quant**
- **4 - Diode**
- **5 - HardClip**
- **6 - SoftClip**
- **7 - Modulo**

#### Distortion Amount (0-99)
Controls the intensity of the selected distortion algorithm. Higher values increase the amount of distortion applied.

#### Distortion Target (0-3)
Determines where in the signal chain the distortion is applied:
- **0 (Off)**: No distortion applied
- **1 (Dry)**: Distortion applied to the input signal before delay processing
- **2 (Wet)**: Distortion applied to the delay output after processing  
- **3 (Both)**: Distortion applied to both input and output signals

#### Distortion Trim (0.0-1.0)
Output gain control applied after distortion processing to prevent clipping and maintain consistent levels. Lower values reduce the output level proportionally.

---

## LFO System

The heart of Kali's modulation capabilities lies in its 6-oscillator LFO system. Navigate to LFO EDIT page to access these settings.

### LFO Selection and Navigation
- **Left Encoder Turn**: Select which LFO (1-6) when in selection mode
- **Left Encoder Click**: Toggle between editing LFO selection vs. parameter editing
- **Right Encoder Turn**: Navigate parameters (when not editing) OR edit values (when in edit mode)
- **Right Encoder Click**: Enter/exit parameter value editing mode
- **Right Encoder Hold**: Enter modulation editing mode (for advanced modulation routing)
- **LFO Adjust Knob**: Direct access to the Adjust parameter for the currently selected LFO
- **Delay Adjust Knob**: When editing, can set parameter values directly for some parameters

### Core LFO Parameters

#### Waveform (Sin/Tri/Saw/Ramp/Square/etc.)
Base oscillator waveform:
- **Sin**: Smooth sine wave
- **Tri**: Triangle wave
- **Saw**: Sawtooth (rising)
- **Ramp**: Sawtooth (falling)  
- **Square**: Square wave
- **Noise**: Sample-and-hold noise
- Additional variations and filtered versions available

#### Mode (0-13)
Fundamental LFO behavior:

- **0 - Core**: Standard oscillator behavior
- **1 - S+H**: Sample and hold on sync
- **2 - T+H**: Track and hold mode
- **3 - RandRst**: Random reset on trigger
- **4 - RndShp**: Randomly change waveform  
- **5 - Jitter**: Frequency jitter based on noise
- **6 - Osc**: Basic oscillator mode
- **7 - Glacier**: Very slow, divided rates
- **8 - Clocks**: Clock-synchronized operation
- **9 - Follow**: Envelope follower mode
- **10 - Sidechain**: Ducking/sidechain mode
- **11 - Envelope**: ADSR envelope mode
- **12 - Turing**: Turing machine-style sequences
- **13 - Raw**: Direct knob/CV control
  

#### Frequency Control

**Multiply L Time (1-100)**: Primary frequency multiplier relative to left delay. Combined with global LFO rate and clock sync to determine final frequency.

**Divide Numerator (1-1000)**: Frequency divider/multiplier.

**Effective Rate Calculation:**
```
Final Rate = Base Rate × (Meta / Meta Divider) × Global Multiplier
```

#### Output Control

**Polarity (+, +/-, -, -/+)**:
- **+ (Unipolar Positive)**: 0V to +5V output
- **+/- (Bipolar)**: -5V to +5V output  
- **- (Unipolar Negative)**: -5V to 0V output
- **-/+ (Inverted Bipolar)**: Inverted bipolar output

**Offset (-2048 to +2048)**: DC offset added to LFO output before scaling.

**Attenuate (1-100%)**: Output amplitude scaling.

### Advanced Modulation

#### Cross-Modulation
**FM Source (0-10)**: Select which LFO provides frequency modulation.  
**FM Amount (-100% to +100%)**: Frequency modulation depth.

**AM Source (0-10)**: Select which LFO provides amplitude modulation.  
**AM Amount (-100% to +100%)**: Amplitude modulation depth.

#### Envelope and Timing
**ADSR Controls** (when in Envelope mode):
- **Attack (0-10s)**: Envelope attack time
- **Decay (0-10s)**: Envelope decay time  
- **Sustain (0-100%)**: Envelope sustain level
- **Release (0-10s)**: Envelope release time

**Phase Offset (0-360°)**: Phase relationship between LFOs.

**Trigger/Reset Source**:
- **0**: No external triggering
- **1**: Gate Input 1
- **2**: Gate Input 2

#### End-of-Cycle Actions
**EOC Action**: What happens when LFO completes a cycle:
- **0**: Nothing
- **1**: Reset target LFO
- **2-4**: Add phase offset to target (90°, 180°, 270°)
- **5**: Random waveform change
- **6**: Scramble parameters

**EOC Target**: Which LFO receives the end-of-cycle action.

### Calibration and Fine-Tuning

#### Adjust (0-100%)
Multi-purpose parameter that changes function based on LFO mode:
- **Standard modes**: Fine frequency control
- **Noise modes**: Update rate/smoothing
- **Jitter mode**: Jitter amount
- **Follow mode**: Sensitivity  
- **Raw mode**: Direct output level

#### Calibration Parameters
**Offset Cal (-2048 to +2047)**: Hardware calibration offset.  
**Attenuate Cal (1-100%)**: Hardware calibration scaling.

### LFO Routing and Outputs
- **LFOs 1-4**: Available on dedicated CV outputs
- **LFOs 5-6**: Available on auxiliary CV outputs  
- **Internal Cross-Modulation**: LFOs can modulate each other via FM/AM sources
- **External Patching**: CV outputs can be patched to CV inputs for delay parameter modulation

---

## Advanced Features

### Advanced Features

### Clock System and Synchronized Modulation

One of Kali's most powerful features is its ability to synchronize LFO rates to delay times and musical timing. This creates musically coherent modulation that stays in sync with your material.

#### Why Synchronized LFO Rates Matter

**Musical Coherence**: When LFO rates are synchronized to delay times, modulation creates predictable, musical patterns rather than chaotic drift. For example, an LFO cycling once per delay repeat creates a regular pulse that enhances rhythm rather than obscuring it.

**Harmonic Relationships**: LFO rates that are simple ratios of delay times (1:1, 1:2, 2:1, etc.) create harmonic relationships between the delay pattern and modulation. This is similar to how musical intervals work - simple ratios sound more consonant and musical.

**Tempo-Locked Effects**: With clock sync, both delays and LFOs lock to a master clock (Internal, External CV, or MIDI), ensuring that modulation enhances the groove rather than fighting it.

#### Practical Applications

**Rhythmic Modulation**: Set an LFO to cycle at 1/4 note rate while your delay is set to 1/8 notes. The LFO creates a slower pulse that groups the faster delay repeats into musical phrases.

**Polyrhythmic Patterns**: Use multiple LFOs at different ratios (1:1, 3:2, 4:3) to create complex polyrhythmic modulation that repeats over longer cycles, adding interest without losing musicality.

**Harmonic Tremolo**: Modulate delay feedback at rates synchronized to the delay time to create harmonic tremolo effects that enhance rather than obscure the original timing.

**Progressive Filtering**: Use tempo-synced LFOs to modulate filter cutoff in sync with delay repeats, creating evolving tonal patterns that follow musical structure.

#### Traditional Approaches vs. Kali

**Without Kali**, achieving synchronized LFO/delay relationships typically requires:
- **Manual Calculation**: Computing LFO rates based on delay times and tempo by hand
- **External Clock Division**: Using multiple clock dividers to generate different sync rates
- **Separate LFO Modules**: Dedicating individual LFO modules for each modulation target
- **Complex Patching**: Extensive cable management to route sync signals to multiple destinations
- **Constant Adjustment**: Manually tweaking multiple modules when tempo changes

**With Kali**, the system automatically:
- **Calculates Ratios**: Maintains musical relationships between delay times and LFO rates
- **Unified Sync**: All elements sync to a single master clock (internal/external/MIDI)
- **Integrated Routing**: Built-in cross-modulation matrix between 6 LFOs
- **Tempo Following**: Automatic adjustment when master tempo changes
- **Visual Feedback**: Real-time display of sync relationships and timing

#### Setting Up Synchronized Modulation

1. **Choose Master Clock**: Set sync mode (Internal/External CV/MIDI) in global options
2. **Set Base Timing**: Use Time L/R knobs to establish delay times relative to tempo
3. **Configure LFO Rates**: Set LFO Meta/Meta Divider for musical ratios (1/4, 1/2, 2/1, etc.)
4. **Patch Modulation**: Connect LFO CV outputs to CV inputs for delay parameter control
5. **Fine-Tune Ratios**: Use LFO Adjust knobs for precise timing relationships

This integrated approach transforms complex polyrhythmic modulation from a technical challenge into an intuitive creative tool.

### MIDI Integration
- **Full MIDI I/O**: Note on/off, CC, clock
- **MIDI Clock Sync**: Lock to incoming MIDI clock
- **CC Control**: Map MIDI controllers to parameters
- **Clock Output**: Send MIDI clock downstream

### Preset System
- **Global Presets**: Save complete system state
- **LFO Presets**: Individual LFO configurations  
- **DSP Presets**: Delay algorithm settings
- **Automatic Save**: Hold both encoders to save current state

### Visual Feedback
The OLED display provides real-time visualization:
- **Waveform Display**: See LFO output in real-time
- **Parameter Values**: Current settings with units
- **VU Meters**: Simple input/output level monitoring for signal diagnosis
- **Activity Indicators**: MIDI, sync, and trigger status
- **Clock Information**: BPM, sync status, timing

---

## Tips and Techniques

### Navigation Tips
1. **Quick Parameter Access**: Use the LFO Adjust and Delay Adjust knobs for immediate parameter control without entering edit mode
2. **Edit Mode**: Always click the right encoder to enter edit mode before trying to change parameter values with encoder turns
3. **Page Navigation**: Left encoder always handles primary navigation between pages
4. **Factory Reset**: On debug page, left encoder click performs factory reset
5. **Save Settings**: Hold both encoders simultaneously to save current state
6. **Encoder Direction**: If encoders feel backwards, enable "Invert Encoders" in global options
   - **Symptoms of Reversed Encoders**: 
     - Turning right moves parameters/pages to the left or decreases values when you expect them to increase
     - Navigation feels counterintuitive - clockwise turns go backwards through menus
     - Parameter values decrease when you turn clockwise expecting them to increase
     - The encoder response feels "upside down" compared to typical knob behavior

### Getting Started
1. **Basic Delay**: Start with "Basic" mode, adjust Time L/R and Feedback knobs
2. **Add Modulation**: Navigate to LFO 1 (left encoder turn), click left encoder to select parameter mode, set to "Core" mode with slow triangle wave
3. **Route Modulation**: Use LFO CV outputs patched to CV inputs to modulate delay time or other parameters
4. **Sync to Clock**: Set sync mode in options and use clock outputs to sync other gear
5. **Edit Parameters**: Always click right encoder to enter edit mode before changing values

### Creative Applications

**Synchronized Modulation**: Set LFO rates to musical ratios of delay times for polyrhythmic patterns that stay musical and coherent.

**Evolving Textures**: Combine multiple LFOs with cross-modulation and different rates.

**Granular Soundscapes**: Explore Parvati and Granular modes with envelope following.

**Harmonic Processing**: Use Resonator mode with MIDI note control for pitched delays.

**Complex Modulation**: Patch LFO CV outputs to CV inputs for delay time modulation, or chain LFOs using FM/AM sources for non-repeating patterns.

### Troubleshooting

**No Output**: Check Mix knob, ensure it's not fully dry. Use VU meters to confirm signal presence.

**Distorted Sound**: Reduce input gain or feedback amount. Monitor levels with VU meters.

**LFOs Not Working**: Verify LFO rate isn't too slow, check output scaling.

**Sync Issues**: Confirm sync mode matches your setup (Internal/External/MIDI).

**Clock Problems**: Check PPQN settings match your system's expectations.

---

## Specifications

- **Sample Rate**: 48kHz
- **Bit Depth**: 32-bit floating point processing
- **Maximum Delay**: 40 seconds (2M samples)
- **CV Outputs**: 0-5V, 12-bit resolution, optimized for frequencies <1kHz
- **LFO Range**: 0.001Hz to ~1kHz (aliasing above 1kHz on CV outputs)
- **MIDI**: Full MIDI 1.0 specification
- **Display**: 128x32 OLED with real-time graphics

---

*Firmware Version 2.0 - Built for Daisy Platform*