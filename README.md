# Everything You Love Will One Day Be Taken From You
A listening machine that slowly destroys a sound every time it plays back.
For more background about this instrument: http://www.impracticaldevices.com/volume-3/

How does it work?
A sound is recorded directly into the instrument. There is space for a few seconds of recording. The design discourages loading sounds into the machine from an external source, and it is deliberately difficult to record the sound in as well, in order to encourage focusing on listening to a single sound for as long as possible.
The sound playback is done through two wavetables, one for each channel. Whilst holding down the button the sound is looped. Each time the sound is looped a random "glitch" is written into the wavetables, glitching the playback of the sound (and flashing the LED), which then overwrites the original sound in the array (with a short delay to account for the current playback). The patch is automatically saved whenever the button is released. 
I'm not entirely sure why the sound ends up disappearing, I suspect this has to do with the delay that I'm using to offset the overwriting of the sound. The wavetable glitching method makes the glitches recognisable as part of the original sound, and it is relatively easy to adjust the parameters of the random numbers that are being sent to the wavetable to change how quickly the sound deteriorates.
The sound is played out through surface transducers so the instrument itself is generating the sound. There is no direct output.


This instrument uses the following hardware:
- Bela (with BeagleBoard)
- Momentary Button Switch
- 1 LED
- 2 Gel Audio Surface Transducers

And the following software:
- Pure Data

Some notes on each of these...

Bela:
The software runs on a Bela, which is a high-performance audio-focused shield for the BeagleBoard microcomputer system. It can also run on a Raspberry Pi (or any other Linux-based machine) but the performance is considerably less good when it comes to auto-saving the patch. I'm not entirely sure why this is. The full-sized Bela also includes two channels of amplifier output, which makes for a simpler hardware setup as the speakers can be connected directly to the board. 

Momentary Button Switch:
For this instrument I chose a momentary button, so the playback of the sound occurs whilst the finger is holding down the button. This felt like a more rewarding and poignant method for destroying the sound. Releasing the button saves the destroyed sound permanently, vaguely reminiscent of how a land mine works, with considerably less dire consequences.
The button is connected to a digital input pin on the Bela. I used a rather expensive but very nice metal "anti-vandal" button: https://www.digikey.co.uk/product-detail/en/bulgin/MP0050-2/708-1437-ND/1980794

LED:
The LED flashes each time the wavetables are glitched. This is controlled from a digital output pin on the Bela.


Software:
The patch runs entirely in Pure Data. I have also created a version of the software that is better suited to running on a desktop machine here: https://github.com/yannseznec/Everything-you-love-demo
One of the crucial aspects of the software is that the sound is stored as an array in PD, rather than as a sound file. This is so that when the patch is saved the original audio data is permanently overwritten. 
