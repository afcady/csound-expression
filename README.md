Csound-expression guide
===============================================================================

[![Join the chat at https://gitter.im/anton-k/csound-expression](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/anton-k/csound-expression?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Welcome to the simplest textual synthesizer.

~~~{.haskell}
> dac $ osc 440
~~~

Csound-expression is a Haskell framework for computer music.
With the help of the library we can create our instruments on the fly. 
A couple of lines in the interpreter is enough to get the cool sound going
out of your speakers. It can be used for simple daily sound-file processing 
or for a full-blown live performances. It's available on [Hackage](http://hackage.haskell.org/package/csound-expression).

Let's look at how we can create computer music with Haskell. 

-------------------------------------------------------------------


* [Introduction](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Intro.md)

* [Basic types](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/BasicTypesTutorial.md)

* [Rendering Csound files](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/ProducingTheOutputTutorial.md)

* [Basics of sound synthesis](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/SynthTutorial.md)

* [User interaction](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/UserInteractionTutorial.md)

* [Scores](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/ScoresTutorial.md)

* [Events](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/EventsTutorial.md)

* [Real-world instruments show case](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Patches.md)

* [FX family](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/FxFamily.md)

* [SoundFonts](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/SoundFontsTutorial.md)

* [Custom temperament. Microtonal music](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Tuning.md)

* [Samples](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/SamplesTutorial.md)

* [Signal segments](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/SignalSegmentsTutorial.md)

* [Widgets for live performances](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/LiveWidgetsTutorial.md)

* [Padsynth algorithm](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Padsynth.md)

* [Granular synthesis](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/GranularSynthesisTutorial.md)

* [Arguments modulation](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/ModArg.md)

* [Csound API. Using generated code with another languages](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/CsoundAPI.md)

* [Creating plugins with Cabbage](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/CabbageTutorial.md)

-------------------------------------------------------------------

Appendix:

* [Introduction to Csound for Haskellers](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/appendix/CsoundInstro.markdown)

* [Overview of the library](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/appendix/Overview.markdown)

-------------------------------------------------------------------

WARNING: the library works best within ghci. The real-time sound rendering 
function `dac` spawns a child process in the background which may continue 
to execute after you stop the main process that runs the programm. 
It's not so in vim but it happens in the Sublime Editor and when you 
invoke `runhaskell`. So the best is to write you program in the separate 
file and then load it in the ghci and invoke the function `main`
(which runs the sound rendering with the function `dac`).


---------------------------------------------------------------------

News
-----------------------------

**The 5.1 is out! Let's warm up our hearts with new bright ideas in this Cold winter! New features:**

csound-expression


* **New data type for Patches!** This change is incompatible but it brings better support for playing patches live!
   The polyphonic and monophonic patches are united with single data-type so we can play them with the same functions.
   Also now we can create layered patches to play several patches at the same time and also we can split the keyboard
   on sections to play different patches on different sections. It's useful feature available in many modern synthesizers.
   But here we can include any number of layers! and we can mix mono and poly instruments together! 

   See the [guide on patches](https://github.com/spell-music/csound-expression/blob/master/tutorial/chapters/Patches.md) to read the details.

* **Hard and soft sync**. Lots of functions added for hard and soft sync. Check out the module `Csound.Air.Wave.Sync`.

* **Morpheus is here**. New cool granular synthesizer is included. It's based on partikkel opcode. 
   The aim is to simplify the work-flow with partikkel opcode. The API is experimental right now and might change.
   See the module `Csound.Air.Granular.Morpheus` for details.

* **Rewrite for filters**. Filters get new names that suppose the audio-quality of the filter. Also many filters were redesigned
   to unify the parameters (order of arguments and ranges). Check out the module `Csound.Air.Filter`.

* **Many great filters were added** thanks to the work of Steven Yi. Now we can use 

   * zero-delay filters: `zlp`, `zhp`, `zbp`, `zladder`, `zdf2`, `zdf4`.

   * diode ladder filter (famous acid sound of TB-303): `diode`, `linDiode`

   * Korg 35 filters: `korg_lp`, `linKorg_lp`, `korg_hp`

   New classical analog-like filters:

   * Chebyshev type I and II low pass filters: lpCheb1, lpCheb2 (also there are high-pass versions)

   * new butterworth filters: `clp`

  Named filters with specific character suggested with a name: `plastic`, `wobble`, `trumpy`, `harsh`.

* **Transforming the audio with impulse responses now is super easy**. Check out the new functions `monoIR`, `stereoIR`
   from the module `Csound.Air.Fx`. With those functions we can easily add complicated and beautiful reverbs
   from natural environments or classical reverberation units. There are plenty IR resources you can find out on the WEB.
   Also it adds the cool `zconv` function for zero convolution delay kindly provided by Victor Lazzarini.

* **Cabbage support**. Adds full support for building [cabbage](http://cabbageaudio.com/) interfaces. Checkout the module `Csound.Cabbage`.
  We can create vst-plugins with it!  Still needs help for testing. We can check out the tutorial on how to build cabbage interfaces
  with csound-expression library: [Cabbage guide](https://github.com/spell-music/csound-expression/blob/master/tutorial/chapters/CabbageTutorial.md).

* **Useful aliases for classic reverbs** with single dry-wet ratio as a parameter: `room`, `chamber`, `hall`, `cave`.
  We can use it like this: `dac $ hall 0.25 mySynt` instead of `dec $ mixAt 0.25 largeHall2 mySynt`.

* **Raw waveforms for analogue-like oscillators**: `rawSaw`, `rawTri`, `rawSqr` non-band limited based
  on table lookup. Can be useful for LFOs or more light-weight versions of oscillators than `saw`, `tri` or `sqr`.

* **mul' new scaling function**. Scaling with side-effects. Can be useful to scale with random envelope.

* **Adds table read and write opcodes**. Adds opcodes `tablewa`, `tablew`, `readTab`, `readTable`, `readTable3`, `readTablei`.
    See the module `Csound.Tab` for details.

* **Convenient aliases for reading from audio-files to tables**. New names `wavLeft`, `wavRight`, `mp3Left`, `mp3Right` to read  
   audio by channels. Also we can read both channels with functions `wavs` and `mp3s`.

* **Support for up to 8 outputs**. More instances for `RenderCsd` were added. Now we can play back up to 8 signals at the same time!

* **Useful option to suppress the event printing on the screen**. By default the Csound prints out every message on the screen (with time stamps and amplitudes).
    Now we have useful function `noTrace` to suppress those messages. Just write `dacBy noTrace $ mySigs` to stop them.

* **Adds More option setters for RT-audio engines**. New option setters: `setAlsa`, `setMme`, `setCoreAudio`.
    Also it fixes the name of the RT-engine for OSX.

csound-sampler

* **Adds randomized patterns** with which we can skip the beats in the fixed pattern by given probability: `rndPat` and `rndPat'`.

**The 5.0 is out! New features:**

csound-expression

* **Microtonal tunings**. We can use custom temperaments with insturments, patches, soundfonts and MIDI-instruments.
   Check out the guide on tuning and microtonal music (see also module `Csound.Tuning`).
   There are many predefined tunings (including ancient ones).
   Now we can play the authentic Bach music with Haskell! 
   See [Custom temperament. Microtonal music](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Tuning.md)
   for details.

* **Functions for Csound API**. We can interface with generated code through many other languages.
   We can generate the code with Haskell and the use it in other environments. we can build UI with Python or Clojure,
     we can create an Android synthesizer. See the guide section on Csound API.
     See [Csound API. Using generated code with another languages](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/CsoundAPI.md)
     for details.

* **Padsynth algorithm** (need Csound 6.05). There are functions that makes it easy to use wonderful PADsynth algorithm,
    This algorithm is designed to make "alive" instruments, natural pads. 
    There are not only function that explore the algorithm but also new PAtches in the
    package csound-catalog that are based on it! See the section in the guide on the PADsynth.
    Lot's of padsynth instruments are mode with morphing support. We can crossfade between 2 or even 4 timbres.    
    See [Padsynth algorithm](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Padsynth.md)
    for details.

* **Argument modifiers** make it very convinient to modulate the rguments (apply vibrato to frequency
   or add some randomness to the parameter). See [Arguments modulation](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/ModArg.md)
   for details.

* The **hard clipping** was substituted with **limiter**. There should be no distortion when
   amplitude goes higher than `0dbfs` value.

* Adds **Ping-pong delay** implementation. See function `pingPong` at the module `Csound.Air.Fx`.

* Adds Rory Walsh's brand **new analog filters** (need Csound 6.07). See functions `alp1`, `alp2` and `alp3` at the module `Csound.Air.Filter`.

* Bugfixes for `mixAt` function. Now it doesn't duplicates the effectful-code.
   Now `mixAt` is not a function that is based on class `At`. It becomes
   a method in it's own class called `MixAt`. That fixes the code duplication problem.

csound-catalog

* **new instruments** that are based on **PADsynth algorithm**. Check out `Csound.Patch`
   at the section on PADsynth Sharc instruments. There are new deep spiritual vedic pads
   (vibhu, rishi, agni, prakriti, rajas, avatara, bhumi).
   See [Padsynth algorithm](https://github.com/anton-k/csound-expression/blob/master/tutorial/chapters/Padsynth.md)
    for details.


csound-sampler

* adds some useful instances for class `At` and `MixAt`.

**The 4.9.0 is out! New features:**

csound-expression

* Functions for creation of FM-synthesizers. We can create
the whole graph of FM-units (with feedback). Check out the module `Csound.Air.Fm`

* Support for Monosynth patches. See atMono in the module `Csound.Air.Patch`

* Easy to use Binaural panning. See the module `Csound.Air.Pan`

* Construction of patches for sound fonts (`sfPatch`, `sfPatchHall`). 

* Table of tables. We can create a table that contains tables.

* Harmonic oscillators for subtractive synth: `buz` and `gbuz`

* Reverbs for patches. It's very easy to add a reverb to your  patch
 (`withSmallHall patch`, `withLargeHall patch`, etc)

* Some bug-fixes

csound-catalog

* Many mono-synth were added. You can use them with function `atMono`
  in place of `atMidi`. The mono versions of patches have suffix `m`.

* SHARC instruments. SHARC db contains a FFT-samples for sustain notes. 
   It includes many orchestra instruments. There are many new patches that
   use natural sounding timbres taken from the SHARC library. 
   Check out functions `soloSharc`, `padSharc`, `dreamSharc`.

csound-sampler

* Handy function `withBpm` allows to query current bpm with in the scope
  of expression.

* Sampler mappers were generalized.

* Char trigering functions are synchronized with bpm.

**The 4.8.3 is out! New features:**

This is a very important release to me.
It tries to solve the problem present in the most open source music-production libraries.
It's often the pack of beautiful sounds/timbres is missing. User is presented with
many audio primitives but no timbres are present to show the real power of the framework.
This release solves this problem. See the friend package csound-catalog on Hackage.
It defines 200+ beautiful instruments ready to be used. 

The csound-expression defines a new type called `Patch` for description of an instrument 
with  a chain of effects. It's good place to start the journey to the world of music production.

There are new functions for synchronized reaction on events. The triggering of events 
can be synchronized with given BPM.

There examples are fixed and should work.

The library is updated for GHC-7.10!

**The 4.8.2 is out! New features:**

This release improves oscillators in many ways.
Adds phase control to many standard oscillators.
There are functions to detune oscillator and create unisions of oscillators 
(multioscillators or chorus effect). 

Adds support for randomly generating events (with random frequency).

**The 4.8 is out! New features:**

A multitap looper is implemented (see `Csound.Air.Looper`). It's  a powerful widget 
with lots of controls. We can create unlimited number of taps.
And the length of the loops doesn't have to be the same for all taps.
We can insert effects and even external controllers. And all this is packed
as a simple function that produces a widget and the output signal.
Three types of loopers are available one is for raw signal inputs,
another for midi instruments and the last one is for soundfonts.
You can see it in action at [youtube](https://www.youtube.com/watch?v=cQQt9bu_x-A).

There are lots of new step sequencers available. 
Pre 4.8 step sequencers could only produce signals
with equal time segments but new step sequencers can 
play a tiny melodies. The API of temporal-media is 
supported for step sequencers (see `Csound.Air.Envelope`).
There is a new type called `Seq`. It's for step sequencers
that can play monophonic melodies.

There is a type class for humanization of envelopes.
It works for linseg and step sequencers. It adds some amount
of randomness to durations or values (see `Csound.Air.Envelope` `HumanValue`
and `HumanTime`). 

A midi chooser ui-box was implemented (see `Csound.Air.Live`, `hmidiChooser`, `uiMidi`). 
It makes it easy to choose a midi instrument among several alternatives. There are stand alone
widgets and widgets implemented as an effect-box.

The class `Compose` from `temporal-media` package was broken 
to two classes: `Harmony` (with function `hor`) 
and `Melody` (with function `mel`).

**The 4.7 is out! New features:**

The Scores are redesigned! The low level `CsdEventList` is substituted
with more advanced and flexible type `Sco`. The instruments are triggered not
with pairs or triplets (individual events) but with scores!

The lib now depends on common APIs for delaying and composing values.
There are common type classes for composition. 

There is a simple API for composition of samples, notes and signal segments.
The `mel` plays units sequentially, The `hor` plays units at the same time.
The `del` delays the unit by given amount of time, The `lim` limits the unit in time.
the `loop` creates infinite loops. The `loopBy` creates finite loops.
The list of all functions can be found in the package temporal-media. See 
the module `Temporal.Class`.

I need to update the guide for changes!

**The 4.6 is out! New features:**

* Granular delays and effects (see `Csound.Air.Granular`)

* It's possible to create tables not only for reading but also for writing.
  We can create sound buffers (see `newTab` and `newGlobalTab` in the module `Csound.Tab`). 

* Hyper Vectorial Synthesis (HVS). Easy to use functions for HVS (see `Csound.Air.Hvs`)
   With HVS we can control lots of parameters with a couple of sliders. 
   The HVS can reduce the size of control parameters by interpolating between snapshots of parameters.

* New spectral functions for spectral fusion: `crossSpecFilter` and `crossSpecVocoder` (see `Csound.Air.Spec`)

* New effect for playing input samples in segments (back and forth) `trackerSplice` 
  (original design by Rory Walsh). With it we can extract segments of live audio and 
  repeat them or play in reverse.

**The 4.5 is out! New features:**

* Easy to use granular synthesis (see `Csound.Air.Granular`)

* Support for opcode `mincer`. It's possible to scale pitch and tempo 
  of audio files independently (see `Csound.Air.Wav` ram reading functions). 

**The 4.4 is out! New features:**

* Signal segments.  With signal segments we can schedule audio signals
    with event streams. We can limit audio signals with clicks of the buttons
    or some other live events. We can retrigger samples, play them in sequence and 
    perform many more actions shich are tied to the event streams. 

* Triggering samples with keyboard and midi-events (see `Csound.Air.Sampler`). 

