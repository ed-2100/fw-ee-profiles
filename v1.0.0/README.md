# v1.0.0

Goals for this profile:

- Flat Response
- Maximum Volume Headroom
- Simple
- Non-Fatiguing
- Subjective Element (I.E., clean-sounding sound)

Here are some of the reasons why I didn't use certain filters.

- **Bass Enhancer**:
  1. Uses squaring for the harmonic generation, which behaves differently depending on the amplitude of the track being played.
  2. The "scope" option uses a IIR lowpass, which causes combing, a type of phase cancellation creating an uneven frequency response, when paired with the other filters (this is the big one for me).
- **Multi-Band Compressor**:
  1. This is subjective, but I personally don't like the sound of compressing already compressed songs.
  2. Hard to tune. Very subjective in regards to the tuning as well.

Here is the basic filter layout:

- **Excursion-Reducing High-Pass**:
   - Removes frequencies that can't be rendered by the speakers.
   - The main use for it is to prevent the limiter from being triggered when it doesn't need to be.
- **Convolver**:
  - Flattens the frequency response.
- **Brickwall Limiter**:
  - Allows the music to be played at high volumes without clipping.

I use a UMIK-1 microphone with the calibration file loaded to take my measurements.

[Here](REW_Inversion_Tutorial.md) is a tutorial that guides you on making your own convolver correction.
