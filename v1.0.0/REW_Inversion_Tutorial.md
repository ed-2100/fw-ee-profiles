# REW Inversion Tutorial

Here is a detailed step-by-step guide to make your own correction (for REW v5.31.3, but probably applicable across versions).

Here are some reasons why I didn't use other techniques:

- **Swept Sine Measurements**:
  1. Very hard to get a notch-free measurement, even with IR windowing.
  2. Requires multiple measurements, which takes a lot of time.
  3. Very easily messed up by a car passing by, or an air conditioner.
  4. End result doesn't sound good in my opinion (easily fatiguing).
- **Graphic EQ via REW's Filter Optimizer**:
  1. Less accurate when compared to convolution inversion.
  2. Not deterministic.

Here is the meat and potatoes:

- Move to an open space with minimal reverb and place your laptop on a hard surface.
- Make sure your calibration file is loaded and easyeffects has been shut down.
- Max out your speaker's volume on both your desktop and using alsamixer.
- Open up the Generator and the RTA Window.
  1. **Generator Settings**:
    - Pink Noise
    - Full Range
    - Output: L
  2. **RTA Settings**:
    - FFT Length: 64k
    - Averages: Forever
    - Window: Hann
    - Max Overlap: 93.75%
- Start the Generator at somewhere around -15 dB.
- Start slowly waving your microphone around in your listening area while having it pointed at the laptop touchpad.
- Begin the RTA measurement and continue slowly waving the microphone around for about 100-200 averages.
- Stop the measurement and generator and save the current measurement. Select the the right channel and repeat.
- In the All SPL tab, open Actions and perform a dB average of the two measurements. This is the measurement that is used for correction.
- Hide the other two measurements.
- In Actions, select var smoothing (or 1/48 if you want unnecessary precision) and apply it.
- Open up Measurement actions, and create a min. phase version of the dB average. This is needed to work around a REW bug when performing trace arithmetic later on.
- Hide the original response.
- Now, select the min. phase response open up the EQ window.
- Expand the Target Settings tab and input the following parameters:
  - Target Type: Full Range
  - LF Cutoff: 0 Hz
  - Add Room Curve: [X]
  - LF Rise Start: 20,000 Hz
  - LF Rise End: 10 Hz
  - LF Rise Slope: 3.0 dB/octave
  - HF Fall Slope: 0.0 dB/octave
- Click "Calculate target level from response" and then "Generate measurement from target shape".
- Back to the main window.
- Go to Actions and open Trace arithmetic.
- Perform the following actions:
  - **A / B**:
    - A: min. phase response
    - B: Generated Target
    - No lower or upper limit.
  - **1 / |A|**:
    - Maximum Gain: 30 dB
    - A: The newly generated response
    - Lower Limit: 70 Hz
    - Upper Limit: 13,000 Hz
    - Target Level: 0 dB
    - Exclude Notches: [ ]
- The generated response should be centered around 0 dB and look like the opposite of your original measurement.
- With this new measurement selected, go to File -> Export -> Export impulse response as WAV. Use the following settings:
  - Export min phase version of IR.
  - Place t=0 at sample index 64.
  - Export this sample count: 8k
- Click ok, name your file, and there you go.
