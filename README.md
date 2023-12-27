# About
This program is a simple text-to-audio converter that generates audio from input text. The program maps each character to a specific musical note frequency and then creates an audio waveform based on the mapped frequencies. The output is an audio file containing the synthesized audio corresponding to the input text.

The program uses a dictionary notes_map to map characters to their respective musical note frequencies. It then iterates through the input text, retrieves the frequency for each character from the dictionary, and synthesizes the corresponding audio waveform using NumPy. The audio waveform data is then saved to an audio file, allowing for easy playback and distribution of the generated audio.

Made by KVI Kontent

# Setup
To use this text-to-audio converter, follow these steps:

1. Install the required dependencies:
   ```
   pip install numpy soundfile
   ```
2. Copy the following code into your Python project or create a new Python file with this content:
   ```
   import numpy as np
   import soundfile as sf
   
   def text_to_audio(text, output_file):
       notes_map = {
           'a': 220, 'b': 246.94, 'c': 261.63, 'd': 293.66, 'e': 329.63, 'f': 349.23, 'g': 392, 'h': 440,
           'i': 493.88, 'j': 523.25, 'k': 587.33, 'l': 659.25, 'm': 698.46, 'n': 783.99, 'o': 880,
           'p': 987.77, 'q': 1046.5, 'r': 1174.66, 's': 1318.51, 't': 1396.91, 'u': 1567.98, 'v': 1760,
           'w': 1975.53, 'x': 2093, 'y': 2349.32, 'z': 2637, ' ': 0
           # Add more characters as needed
       }
   
       text = text.lower()
       prompt = text
   
       audio_data = np.array([])
       for char in prompt:
           if char in notes_map:
               freq = notes_map[char]
               duration = 1  # You can adjust the duration as needed
               t = np.linspace(0, duration, int(44100 * duration), False)
               note = np.sin(freq * t * 2 * np.pi)
               audio_data = np.append(audio_data, note)
   
       sf.write(output_file, audio_data, 44100, 'PCM_24')
   
   text = "example text to convert to audio"
   output_file = "output_audio.wav"
   text_to_audio(text, output_file)

   ```

3. Adjust the text variable to contain the desired input text.
4. Run the Python file, and it will create an audio file named output_audio.wav, containing the audio generated from the input text.

5. Enjoy the synthesized audio and share it as needed!

# Usage
To use the text-to-audio converter, call the text_to_audio function, providing the input text and the desired output file name. The function will then generate an audio file containing the synthesized audio for the input text.

# Examples

| Prompt | Output |
|--------|--------|
| e e e e e e e g c d e f f f f f e e e e e d d e d g | Jingle Bells melody |
| g g a g c b a a b a d c g g a g e e e c d c b b a a a b a g g a g c b a a b a d c | We Wish You A Mary Christmas |
