**🚩 CTF Challenge: The Frequency of Deception**

**Author: L4!n.st3p**

**Category: Misc / Steganography**

**Difficulty: Medium**
📝 **Challenge Description**

    We intercepted this audio transmission, but it's nothing but static and weird beeps. Our junior analyst found a flag in the metadata, but it didn't work. Can you look—and listen—deeper?

    Note: The flag is in three pieces. Combine them in order.

    File: The Frequency of Deception.wav

🛠️ Solution / Writeup
Phase 1: The Red Herring (Metadata)

The first step most players take is checking the file properties or using exiftool.
Bash

exiftool The Frequency of Deception.wav

Finding: * Comment: "Everything is noise until you look closer."

    Artist: SECE{Y0u_Found_Me_Or_D1d_You?}

This is a Fake Flag. The real challenge begins here.
Phase 2: Visualizing the Noise (Spectrogram)

Opening the file in Audacity shows 10 seconds of high-intensity noise.

    Switch the track view from Waveform to Spectrogram.

    The player must apply a High-Pass Filter (around 5000Hz) or adjust the spectrogram settings to reveal hidden text.

    Hidden String: DR%E3FZV60

This string is encoded in Base45.

    Decoding DR%E3FZV60 yields: SECE{H34r_ (Part 1/3)

Phase 3: The Audible Binary (Bacon Cipher)

Following the spectrogram noise, a series of "Beep-Boops" play. There are two distinct frequencies:

    High Pitch (1000Hz): Representing 1 or B

    Low Pitch (400Hz): Representing 0 or A

By transcribing the pulses into a Baconian/Bacon Cipher, the player decodes the sequence:

    Binary/Bacon Result: th3_Un533n_ (Part 2/3)

Phase 4: The Touch-Tone Key (DTMF & Steghide)

At the very end of the audio, a short burst of telephone keypad tones plays.

    The player uses a DTMF Decoder (or listens carefully) to identify the numbers: 2807.

    Knowing there might be hidden data, the player uses Steghide with this numeric password.

BASH :steghide extract -sf The Frequency of Deception.wav -p 2807

Result: A file named secret.txt is extracted containing: Fr3q5} (Part 3/3)
🏁 Final Flag

Combining all three parts discovered by L4!n.st3p:

SECE{H34r_th3_Un533n_Fr3q5}
