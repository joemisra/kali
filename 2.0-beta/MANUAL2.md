# Manual Layout Draft
A fair amount of details are incorrect here, but the structure is pretty good.

# KALI User Manual

## Table of Contents

1. Introduction
   - About KALI
   - Key Features

2. Hardware Overview
   - Front Panel Layout
   - Inputs and Outputs
   - Controls and Interface Elements

3. User Interface Guide
   - Common UI Elements & Navigation
   - Screen Layout
   - Basic Navigation Principles
   - Universal Encoder Functions
   - Control Knobs

4. Basic Operation
   - Navigation System
   - Encoder Controls
   - Operating Mode Overview

5. Primary Operating Modes
   - LFO Edit Mode
     - LFO Parameters
     - Waveform Selection
     - Timing Controls
   - DSP Edit Mode
     - DSP Algorithms
     - Parameter Controls
     - Effect Types
   - Options Mode
     - System Settings
     - Clock Configuration
   - Presets Mode
     - Saving/Loading Presets
   - MIDI Mode
     - MIDI Monitoring
   - Debug Mode
     - System Diagnostics

6. Clock Synchronization System
   - Clock Sources
   - Timing Division/Multiplication
   - Advanced Synchronization Techniques

7. DSP Effects in Detail
   - Delay-based Effects
   - Granular/Texture Processing
   - Distortion Algorithms
   - Filtering Options

8. LFO System in Detail
   - LFO Waveform Types
   - LFO Modes
   - Signal Flow & Modulation Routing
   - Cross-Modulation
   - End-of-Cycle Actions

9. Integration & Advanced Techniques
   - Patching Examples
   - Creative Applications
   - Polyrhythmic Modulation
   - Adaptive Effects
   - Clock-Synchronized Buffer Scanning

10. Connectivity
    - Audio Routing
    - CV & Gate Integration
    - MIDI Implementation

11. Preset Management
    - Preset Types
    - Saving & Recalling Presets
    - Factory Presets

12. Tips & Tricks
    - Performance Techniques
    - Creative Patching Ideas
    - Troubleshooting

13. Specifications
    - Technical Details
    - Power Requirements

14. Support & Resources
    - Firmware Updates
    - Online Resources
    - Contact Information

## Introduction

Thank you for purchasing the KALI Eurorack module by dsp.coffee! KALI is a powerful audio processing and modulation generating module that combines multi-mode delays, distortion effects, modulation sources, and clock synchronization capabilities in a compact Eurorack format. This manual will guide you through the features and operation of KALI.

### About KALI

KALI represents a new approach to Eurorack effects processing by combining sophisticated DSP algorithms with an intricately synchronized modulation system. At its core, KALI is a stereo multi-effects processor with six independent LFOs that can modulate virtually any parameter, all synchronized to a master clock.

### Key Features

- Versatile multi-mode DSP engine with delay, granular, and distortion algorithms
- Six independent LFOs with extensive waveform and behavior options
- Sophisticated clock synchronization system
- Cross-modulation capabilities between LFOs
- Multiple clock sources: internal, external gate, or MIDI
- End-of-cycle actions for complex generative patterns
- Comprehensive preset management
- High-quality 48kHz, 24-bit audio processing
- Intuitive interface with OLED display for visual feedback

## Hardware Overview

KALI is based on the Daisy Patch platform by Electro-Smith, offering high-quality digital signal processing with an intuitive interface.

### Front Panel Layout

The KALI front panel features a clean, organized layout with clear labels for all controls and connections.

### Controls and Interface Elements

- **OLED Display** - Shows current parameters, waveforms, and menus
- **2 Encoders** - Navigation and parameter adjustment
   - Left Encoder (E2) - Page navigation and parameter selection
   - Right Encoder (E1) - Value editing and parameter selection
- **10 Control Knobs**:
  - META1, META2 - Multi-function controls that adapt to the current mode
  - LFO RATE - Controls LFO speed
  - L TIME, R TIME - Left and right delay times
  - CUTOFF - Filter cutoff frequency
  - FEEDBACK - Delay feedback amount
  - MIX - Wet/dry balance
  - LFO ADJUST - Selects/adjusts LFO parameters
  - DELAY ADJUST - Fine-tunes delay parameters

### Inputs and Outputs

- **Gate Inputs** (2) - For clock sync and triggering functions
- **Gate Outputs** (2) - For clock signals and trigger outputs
- **CV Outputs** - For modulation signals from the LFOs
- **Audio Inputs** (stereo) - For processing external audio
- **Audio Outputs** (stereo) - For the processed signal

## User Interface Guide

The KALI interface is designed to provide deep functionality while maintaining an intuitive workflow. Understanding these common interaction patterns will help you navigate all aspects of the module.

### Screen Layout

The OLED display is your primary visual interface and typically shows:

- **Top Section**: Current page/mode name and status indicators
- **Middle Section**: Parameter visualization (waveforms, values)
- **Bottom Section**: Current parameter values or additional information

### Basic Navigation Principles

- **Mode Selection**: The left encoder (E2) click cycles between major modes
- **Parameter Selection**: Turn encoders to highlight different parameters
- **Value Editing**: Click right encoder (E1) to toggle edit mode, then turn to adjust values
- **Visual Indicators**: Parameters being edited will blink or appear highlighted
- **Return to Default View**: After a period of inactivity, the display returns to the main view

### Universal Encoder Functions

**Left Encoder (E2)**:
- **Single Click**: Navigate between major modes (LFO, DSP, Options, etc.)
- **Turn**: When not in edit mode, scroll through available parameters
- **Long Press**: Access secondary functions (varies by page)
- **Double Click**: Not used in standard operation

**Right Encoder (E1)**:
- **Single Click**: Toggle edit mode for the selected parameter
- **Turn**: Adjust selected parameter value when in edit mode
- **Long Press**: Access modulation assignments (on relevant pages)
- **Click While Editing**: Confirm value and exit edit mode

### Control Knobs

Physical knobs provide direct access to frequently used parameters:
- Changes are reflected immediately on the display
- In some modes, knobs may have context-specific functions
- LFO ADJUST and DELAY ADJUST knobs have special functions depending on current mode

## Basic Operation

KALI operates through different pages that can be accessed by clicking and turning the encoders.

### Navigation System

The module uses a page-based navigation system, where each page represents a different operational mode. The current mode is always displayed at the top of the screen.

### Encoder Controls

- **Left Encoder (E2)**
  - **Click** - Move between pages or toggle editing mode
  - **Hold** - Enter special functions
  - **Turn** - Navigate between parameters or pages

- **Right Encoder (E1)**
  - **Click** - Toggle edit mode for the selected parameter
  - **Hold** - Access modulation settings
  - **Turn** - Adjust parameter values

### Operating Mode Overview

KALI has six primary operating modes:

1. **LFO Edit** - Configure oscillator/modulation settings
2. **DSP Edit** - Adjust audio processing and effects
3. **Options** - Global system settings
4. **Presets** - Save and recall configurations
5. **MIDI** - MIDI monitoring and settings
6. **Debug** - System diagnostics and advanced settings

## Primary Operating Modes

### LFO Edit Mode

KALI features 6 independent oscillators for modulation that can be configured in this mode.

#### Navigation in LFO Edit Mode

1. **Enter LFO Edit**: Click left encoder until "LFO" appears at top of screen
2. **Select LFO Number**: Turn left encoder to choose which LFO (0-5) to configure
3. **Navigate Parameters**: 
   - Turn right encoder to cycle through LFO parameters (Waveform, Rate, etc.)
   - Alternatively, use LFO ADJUST knob to quickly select parameters
4. **Edit Parameter**: 
   - Click right encoder to enter edit mode (parameter will blink)
   - Turn right encoder to adjust value
   - For some parameters, DELAY ADJUST knob provides fine-tuning
5. **LFO Visualization**: Current LFO waveform is displayed in the center of the screen
6. **Quick Selection**: The LFO ADJUST knob can directly select which LFO to edit

#### LFO Parameters

- **Waveform** - Sine, Triangle, Saw, Square, etc.
- **Mode** - SyncStraight, Sample & Hold, Random, Turing, etc.
- **Oneshot** - Toggle between continuous and one-shot mode
- **Clock Multiplier/Divider** - Control LFO timing relative to master clock
- **Polarity** - Unipolar, Bipolar, etc.
- **Offset/Attenuate** - Adjust output range
- **Phase Offset** - Shift starting phase
- **ADSR** - Attack, Decay, Sustain, Release envelope controls
- **FM/AM** - Frequency/Amplitude modulation from other LFOs

### DSP Edit Mode

Configure audio processing effects in this mode.

#### Navigation in DSP Edit Mode

1. **Enter DSP Edit**: Click left encoder until "DSP" appears at top of screen
2. **Select DSP Mode**: First parameter is the DSP algorithm (Straight, PingPong, etc.)
3. **Navigate Parameters**:
   - Turn right encoder to move through parameters (P1-P4, distortion, etc.)
   - Each DSP algorithm exposes different parameters with context-specific functions
4. **Parameter Adjustment**:
   - Click right encoder to enter edit mode for a parameter
   - Turn to adjust value
   - META1/META2 knobs often provide direct control of primary parameters
5. **Visual Feedback**: The screen may show special visualizations based on the selected algorithm

#### DSP Algorithms

- **Delay Types**:
  - Straight (Linked/Unlinked)
  - Ping Pong (Linked/Unlinked)
  - Resonator
  - Chorus

- **Granular/Texture Modes**:
  - Parvati (granular processor)
  - Shards (granular fragmentation)
  - Knives (harsh granular cutting)
  - Splat (granular scattering)
  - Grampa/Gramma (vintage-sounding granulation)

- **Distortion Algorithms**:
  - Saturation
  - Foldback
  - Tanh
  - Quantizer
  - Diode Clipper
  - Hard/Soft Clip
  - Asymmetric
  - Modulo

### Options Mode

Configure global settings for KALI's operation.

#### Navigation in Options Mode

1. **Enter Options**: Click left encoder until "OPT" appears at top of screen
2. **Category Navigation**: Turn left encoder to move through option categories
3. **Parameter Selection**: Turn right encoder to select a specific parameter
4. **Value Adjustment**:
   - Click right encoder to begin editing (value will highlight)
   - Turn right encoder to change value
   - Click again to confirm
5. **Options Organization**: Options are grouped by function (Clock, Audio, System)

#### System Settings

- **Clock divisions and multipliers**
- **Sync modes** (Internal, External, MIDI)
- **Reverb parameters**
- **Input/Output gains**
- **Envelope follower settings**
- **Filter mode** (Low-pass, High-pass, Band-pass)

### Presets Mode

Manage configuration presets for global settings, LFOs, and DSP effects.

#### Navigation in Presets Mode

1. **Enter Presets**: Click left encoder until "PRESETS" appears
2. **Select Operation**: Turn right encoder to choose between Load/Save operations
3. **Select Preset Type**: Choose between Global, LFO, or DSP presets
4. **Preset Slot Selection**: Navigate to desired preset slot (0-32)
5. **Confirm Action**: Click right encoder to execute the selected preset operation

### MIDI Mode

Monitor MIDI activity and MIDI clock information.

#### Navigation in MIDI Mode

1. **Enter MIDI Mode**: Click left encoder until "MIDI" appears
2. **View MIDI Activity**: The screen displays recent MIDI events and status
3. **Monitor Parameters**: 
   - MIDI clock rate information is displayed
   - Last received MIDI event details are shown
4. **No Editable Parameters**: This mode is primarily for monitoring

### Debug Mode

Access system diagnostics and advanced settings.

#### Navigation in Debug Mode

1. **Enter Debug Mode**: Click left encoder until "Debug" appears
2. **View System Information**: 
   - Key system parameters are displayed
   - Use right encoder to cycle through debug information pages
3. **Special Functions**: Some diagnostic tools may be available by clicking right encoder
4. **Clock Debug View**: Shows detailed timing information about the clock system

## Clock Synchronization System

KALI's clock synchronization system is a central feature that allows all modulation and timing to remain musically coherent.

### Clock Sources

KALI offers multiple clock synchronization options:

- **Internal Clock** - Generated by KALI's internal clock generator
- **External Clock** - Via Gate Input 1, for synchronizing with external clock sources
- **MIDI Clock** - From MIDI input, for synchronizing with DAWs or MIDI gear

### Timing Division/Multiplication

Each LFO can have its own timing relationship to the master clock:

- **Multipliers** - Speed up LFOs relative to the master clock (x1, x2, x3, etc.)
- **Dividers** - Slow down LFOs relative to the master clock (÷2, ÷4, ÷8, etc.)
- **PPQN Setting** - Pulses Per Quarter Note determines the resolution of the clock

### Advanced Synchronization Techniques

The power of KALI's modulation comes from how these timing divisions interact:

```
Master Clock (e.g., 120 BPM)
   ↓
LFO 1: x1 (quarter notes) → Controls delay time
   ↓
LFO 2: ÷4 (whole notes) → Adjusts filter cutoff
   ↓
LFO 3: x3 (eighth note triplets) → Modulates distortion
   ↓
LFO 4: x4 (16th notes) → Triggers grains
```

This clock hierarchy creates complex but musically coherent patterns that would be impossible with free-running LFOs.

## DSP Effects in Detail

KALI features a versatile multi-mode DSP engine capable of a wide range of sound processing techniques.

### Delay-based Effects

- **Straight Delay** - Traditional delay with separate left and right times
  - **Linked Mode** - Left and right channels have synchronized delay times
  - **Unlinked Mode** - Independent control over left and right delay times

- **Ping Pong Delay** - Signal bounces between left and right channels
  - **Linked Mode** - Symmetric ping-pong effect
  - **Unlinked Mode** - Asymmetric ping-pong with different timing for each bounce

- **Resonator** - Creates pitched resonances from delay feedback
  - Produces metallic, bell-like tones through pitched delay networks
  - Can be tuned to specific musical intervals

- **Chorus** - Creates subtle pitch variations for thickening sounds
  - **Simple Chorus** - Basic chorus effect with minimal controls
  - **Chorus** - Full-featured chorus with depth and rate controls

### Granular/Texture Processing

- **Parvati** - Core granular processor
  - Controls for grain size, density, position, and pitch

- **Shards** - Granular fragmentation
  - Creates glassy, fragmented textures with angular transitions

- **Knives** - Harsh granular cutting
  - Produces aggressive, cutting textures with sharp transitions

- **Splat** - Granular scattering
  - Spreads grains across the stereo field in cloud-like formations

- **Grampa/Gramma** - Vintage-sounding granulation
  - Emulates the character of early granular processors with lower fidelity

### Distortion Algorithms

- **Saturation** - Smooth, analog-style distortion
  - Gradually increases harmonics as input level increases

- **Foldback** - Creates complex harmonic content
  - Signal "folds back" when it exceeds a threshold, creating complex waveshaping

- **Tanh** - Mathematical distortion based on hyperbolic tangent
  - Provides smooth, symmetrical clipping

- **Quantizer** - Reduces bit depth for lo-fi effects
  - Creates stepped distortion similar to bit reduction

- **Diode Clipper** - Emulates analog diode distortion
  - Asymmetric clipping similar to guitar pedals

- **Hard/Soft Clip** - Simple clipping distortion
  - **Hard Clip** - Aggressively clips signal at threshold
  - **Soft Clip** - Gradually rounds off peaks

- **Asymmetric** - Different clipping for positive and negative signal components
  - Creates even harmonics for a "tube-like" character

- **Modulo** - Mathematical modulo operation on the signal
  - Creates unique aliasing and digital artifacts

### Filtering Options

A multimode filter can be applied to shape the frequency content:

- **Low-pass** - Allows frequencies below cutoff to pass
- **High-pass** - Allows frequencies above cutoff to pass
- **Band-pass** - Allows a band of frequencies around cutoff to pass

## LFO System in Detail

KALI's modulation system is built around six independent low-frequency oscillators (LFOs) that can synchronize with clock sources and modulate both DSP parameters and each other.

### LFO Waveform Types

KALI features comprehensive waveform options for each LFO:

- **Sine** - Smooth, continuous modulation
- **Triangle** - Linear ramps with sharp corners
- **Saw** - Rising ramp with instant fall
- **Ramp** - Falling slope with instant rise
- **Square** - Alternating high/low states
- **Pulse Variants** - Modified square waves with variable pulse width
- **Noise** - Random fluctuations

### LFO Modes

The LFO modes fundamentally change how each modulator behaves:

- **SyncStraight** - Traditional LFO synchronized to master clock
- **SyncSH (Sample & Hold)** - Captures and holds random values at clock-synced intervals
- **SyncTH (Track & Hold)** - Similar to S&H but follows input while gate is high
- **RandReset** - Resets phase randomly based on probability settings
- **RandShape** - Randomly changes waveform at the end of cycles
- **Turing** - Algorithmic sequencer that generates patterns with adjustable "probability"
- **Wavetable** - Reads through user-defined tables of 16 values
- **Jitter** - Adds controlled randomness to timing
- **FeedbackFollower** - Uses audio envelope to control modulation depth
- **Sidechain** - Attenuates modulation based on audio input

### Signal Flow & Modulation Routing

#### LFO Output Shaping

Before modulating parameters, each LFO's output can be shaped by:

- **Polarity Settings**:
  - **Unipolar+** (0 to +100%)
  - **Bipolar** (-100% to +100%)
  - **Unipolar-** (-100% to 0%)
  - **Inverted** (flips the waveform)

- **Offset** - Shifts the center point of modulation
- **Attenuate** - Controls the modulation depth

### Cross-Modulation

LFOs can form complex relationships by modulating each other:

- **FM (Frequency Modulation)** - One LFO controls another's rate
- **AM (Amplitude Modulation)** - One LFO controls another's depth

The amount of this cross-modulation can be positive or negative (-100% to +100%), allowing for both reinforcement and cancellation effects.

### End-of-Cycle Actions

When an LFO completes a cycle, it can trigger special events:

- **Restart** - Reset another LFO
- **Halt** - Stop another LFO
- **Toggle** - Switch another LFO on/off
- **Flip** - Invert another LFO's polarity
- **RandWave** - Change another LFO's waveform randomly
- **Scramble** - Randomize multiple LFO parameters
- **Teleport** - Jump to a specific phase

## Integration & Advanced Techniques

### Patching Examples

#### Basic Rhythmic Delay

1. Set master clock to sync with your system (Internal, External, or MIDI)
2. Select Straight Delay in DSP Edit mode
3. Set LFO 1 to Square wave, SyncStraight mode, x1 multiplier
4. Route LFO 1 to modulate Left Delay Time
5. Set LFO 2 to Square wave, SyncStraight mode, x2 multiplier
6. Route LFO 2 to modulate Right Delay Time
7. Result: Rhythmic delay pattern that follows your master clock

#### Evolving Granular Texture

1. Select Parvati in DSP Edit mode
2. Set LFO 1 to Sine wave, SyncStraight mode, ÷4 divider
3. Route LFO 1 to modulate grain size
4. Set LFO 2 to Triangle wave, SyncStraight mode, x3 multiplier
5. Route LFO 2 to modulate position
6. Set LFO 3 to Sample & Hold mode, x4 multiplier
7. Route LFO 3 to modulate pitch
8. Result: Evolving granular texture with shifting character but consistent timing

### Creative Applications

#### Evolving Delay Patterns

By connecting LFOs to delay parameters:

- **LFO 1** (slow triangle) → **Left Delay Time** = Gradually shifting echoes
- **LFO 2** (16th notes, square) → **Right Delay Time** = Rhythmic delay jumps
- **LFO 3** (random) → **Feedback** = Unpredictable decay patterns

#### Dynamic Granular Textures

In granular modes like Parvati or Shards:

- **LFO 1** (sine) → **Grain Size** = Breathing texture
- **LFO 2** (one-shot envelope) → **Density** = Bursts of grains triggered by gate input
- **LFO 3** (clock-synced) → **Position** = Rhythmic scanning through the buffer
- **LFO 4** (FM from LFO 1) → **Pitch** = Correlated pitch variations

#### Rhythmic Distortion

For aggressive sound design:

- **LFO 1** (clock-divided square) → **Distortion Algorithm** = Switching between different types
- **LFO 2** (sample & hold) → **Distortion Amount** = Stepped distortion changes
- **LFO 3** (sine with EOC reset) → **Filter Cutoff** = Filtered distortion sweeps

### Polyrhythmic Modulation

Create complex evolving patterns with multiple time signatures:

1. LFO 1: 3/4 time division (dotted eighth notes)
2. LFO 2: 4/4 time division (quarter notes)
3. LFO 3: 5/4 time division (quintuplet pattern)

These will phase against each other, creating evolving patterns that repeat only after extended periods.

### Adaptive Effects

Using FeedbackFollower and Sidechain modes:

1. Configure an LFO in FeedbackFollower mode
2. Assign it to control reverb or delay mix
3. Louder passages will drive more modulation
4. Result: Dynamic effects that respond to your playing

### Clock-Synchronized Buffer Scanning

In delay and granular modes, the synchronized LFOs can scan through the delay buffer at musically relevant intervals. For example:

1. Set a basic 1-second delay
2. Use an LFO at 1/4 speed to scan through the buffer
3. Add a second LFO at 1/16 speed to create micro-variations
4. Use EOC actions to reset phases at specific points

## Connectivity

### Audio Routing

KALI features stereo inputs and outputs for audio processing:

- **Audio Inputs (L/R)** - Connect external audio sources to be processed
- **Audio Outputs (L/R)** - Connect to your mixer, other modules, or audio interface

For maximum flexibility, you can also:
- Use a single mono input which will be processed in stereo
- Self-patch by connecting outputs back to inputs for feedback effects

### CV & Gate Integration

- **Gate Inputs (2)**:
  - **Gate 1** - Often used for clock sync
  - **Gate 2** - Can trigger the Freeze function or other features

- **Gate Outputs (2)**:
  - Output clock signals derived from internal clock
  - Can be used to sync other modules

- **CV Outputs**:
  - Transmit modulation signals from the LFOs
  - Can modulate parameters on other modules

### MIDI Implementation

KALI accepts MIDI data for clock synchronization and parameter control:

- **MIDI Clock** - Synchronize KALI's timing to external MIDI equipment
- **CC Messages**:
  - CC21: Controls DSP Parameter 1
  - CC22: Controls DSP Parameter 2
  - CC23: Controls DSP Parameter 3
  - CC24: Controls DSP Parameter 4
- **Note On/Off** - Can be used to trigger functions (varies by firmware version)

## Preset Management

KALI can store and recall presets for different aspects of its configuration.

### Preset Types

- **Global Presets** - Save all settings including LFOs and DSP
- **LFO Presets** - Save just the LFO configurations
- **DSP Presets** - Save just the DSP effect settings

### Saving & Recalling Presets

To save a preset:
1. Navigate to the appropriate page
2. Select the "Save Preset" option
3. Choose a preset slot (0-32)
4. Confirm save

To load a preset:
1. Navigate to the appropriate page 
2. Select the "Load Preset" option
3. Choose a preset slot
4. Confirm load

### Factory Presets

KALI comes with factory presets that demonstrate various capabilities:
- Basic delay effects
- Complex modulation examples
- Granular textures
- Rhythmic patterns

## Tips & Tricks

### Performance Techniques

- **Use Gate Input 2** to trigger the Freeze function for glitching effects
- **Try different clock divisions** to create polyrhythmic patterns
- **Combine different LFO modes** for complex, evolving modulation
- **Use one-shot LFOs** triggered by gates for envelope-like behavior
- **Experiment with cross-modulation** by setting one LFO to modulate another

### Creative Patching Ideas

- **Feedback patching**: Route KALI's outputs back to its inputs for self-generative sounds
- **CV control**: Use external CV to modulate KALI's parameters alongside internal LFOs
- **Clock division**: Send KALI's clock outputs to other modules for synchronized systems
- **Audio-rate modulation**: Try using audio-rate signals as modulation sources
- **Gate sequencing**: Use a gate sequencer into Gate Input 2 for rhythmic parameter changes

### Troubleshooting

- **Clock sync issues?** Use the Debug page to monitor clock timing
- **Distortion too extreme?** Check the Input Gain in Options mode
- **LFOs not syncing?** Verify the correct sync mode is selected
- **Parameters jumping unexpectedly?** Check for active modulation assignments
- **Display turning off?** This is normal after period of inactivity; touch an encoder to wake

## Specifications

### Technical Details

- **Audio**:
  - Sample Rate: 48kHz
  - Bit Depth: 24-bit
  - Latency: <1ms
  - Frequency Response: 20Hz-20kHz

- **Inputs & Outputs**:
  - 2 Audio Inputs (3.5mm TS/TRS)
  - 2 Audio Outputs (3.5mm TS/TRS)
  - 2 Gate Inputs (3.5mm TS)
  - 2 Gate Outputs (3.5mm TS)
  - Multiple CV Outputs (3.5mm TS)

- **Controls**:
  - 10 Potentiometers
  - 2 Rotary Encoders with Push Buttons
  - OLED Display (128x32)

### Power Requirements

- **Format**: Eurorack
- **Width**: 26HP
- **Depth**: 25mm
- **Power**: +12V DC, 150mA

## Support & Resources

### Firmware Updates

KALI's firmware can be updated to add new features and fix bugs. Visit the dsp.coffee website for the latest firmware and update instructions.

### Online Resources

- **Official Website**: [dsp.coffee](https://dsp.coffee)
- **User Forum**: Connect with other KALI users to share patches and techniques
- **Video Tutorials**: Step-by-step guides to KALI's features
- **Patch Library**: Download and share preset configurations

### Contact Information

For technical support, questions, or feedback:
- Email: support@dsp.coffee
- Social Media: @dspcoffee

---

Thank you for choosing KALI! We hope this manual helps you unlock its full potential.`