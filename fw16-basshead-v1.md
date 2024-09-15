# An Empirically Optimized EasyEffects Filter Profile for the Framework 16
This topic has, at this point, been bashed into the ground, but I have still found other people’s profiles lacking.
Every time I’ve tried other people’s profiles, I’ve been left with discontent and a compression headache.
I've therefore decided to create my own set of configs.

The following configs are intended to bring back sub-100Hz notes in certain genres of music and even out the vocal ranges
in a correct-ish manner.

## Here are instructions to reproduce this profile:
* We start off with a low-shelf filter to preemptively boost the lower bass that the framework 16 speakers cannot produce;
  this is for the “Bass Enhancer” filter in the next step. The low-shelf filter should be set in BWC (BT) mode with -15 dB
  on the input and +15 dB of gain with a cutoff frequency of 95 Hz and a slope of x16. For some reason, the underlying
  driver for the low-shelf filter will produce nasty harmonics when it is configured for MT mode, even though people
  allege that the MT mode is better.
* Next we add a “Bass Enhancer” filter. This filter should be set with the harmonics slider all the way to the right,
  “amount” at 0 dB, “Harmonics” at 10, “scope” at 170, and “floor” disabled. This filter will essentially take the bass
  frequencies we boosted with the previous filter and create harmonics at higher frequencies to “fake” the existence of
  real bass. This filter will really help with your bass-heavy beats.
* Finally, to wrap up the “fake-bass” section, we add a high-pass filter to prevent the original bass (that has been
  boosted by the shelf) from clipping and distorting our output. This filter should be set in BWC (BT) mode with a slope of
  x16 and a frequency of 95 Hz. All other settings should be set to 0, even the gain.
* Now comes the secret sauce to give our sound that apple feel. Here, we add the convolver filter. For people not wanting
  to do a bunch of work, you can just import the `ltcurve15-48k.wav` file and skip the rest of this step. Make sure
  to have all gain settings at 0 dB. If you want to create this yourself, I suggest you get a UMIK-2 and use REW with the
  RTA and wave the microphone around your computer to prevent the profile from picking up nodal resonances. If your
  measurements are coming out weird, you might be creating wind and or vibrations while moving your microphone. I suggest
  that you just try to clean up the speaker’s existing curve and don’t try to make drastic changes to the HF dropoff slope.
* To wrap things up, we add a limiter to prevent those bumps from becoming pops. The limiter filter should be set in “Herm
  Tail” mode with “Full x2 (3L)” oversample and no “dither,” along with 1 dB of “SC pre-amp” and 20 ms of “lookahead,” as
  well as 11 ms of “attack” and 0.25 ms of “Release” with a threshold 0 dB and “boost” disabled. Make sure that “Auto
  Levelling” is disabled as well, and add 15 dB of gain to the “input” parameter. These settings are optimized for audio
  quality and not latency, as I usually use IEMs while gaming, so you might want to adjust them if you intend to game on
  your laptop speakers.

The convolver file referenced in this post is based on measurements from a brand-new batch-15 Framework 16 without a GPU.
A small electret microphone that has a flat response from 20 Hz to 18kHz +-3 dB was used to take the measurements using the
REW RTA with a linearly-weighted moving average. The generic REW filter was used to optimize the mid-range frequencies.
