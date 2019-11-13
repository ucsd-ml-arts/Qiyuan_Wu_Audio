# Project 3 Generative Music using Markov Chain

Qiyuan Wu, qiw103@eng.ucsd.edu


## Abstract

I used a set of instructions to build a Markov chain in Python to train it to generate music based on the state correlation (each note is treated as a state). The instructions are generated from a MIDI file (.mid) and converted into json format using ToneJS Midi. Then, they are fed into a simple markov chain that generates midi phrases out of the ones from the original track, and playes them using pyfluidsynth.

In this example, Chopin Concerto No1 E Minor Op11 and River Flows In You are used to generate the instructions in the markov chain. Both the original and generated track's Midi File from the MIDM database.
![river](https://miro.medium.com/max/750/0*xyeeNUWzLO___J8P.jpg)
![chopin](https://i.ytimg.com/vi/38uEZN5-Hqg/maxresdefault.jpg)
## Model/Data

- I used Markov chain model, which is a stochastic model describing a sequence of possible events in which the probability of each event depends only on the state attained in the previous event. Essentially, Markov chains are mathematical systems that track the probabilities of state transitions. It's usually used to model complex systems and predict behavior. They’re used in many commercial applications, from text autocomplete to Google’s PageRank algorithm. 

- Because of the concise and accurate property of their structure, I chose to use MIDI files for this project. MIDI files are simple files that consist of chunks which contain information about the music encoded in the file. A significant distinction to note is that MIDI files are not playable audio files like MP3 files. Rather, they contain instructions on how to play tunes, which can be played by numerous different computer generated instruments. Due to this property, they are limited in that they can only store a certain range of notes and cannot store complex audio like vocal lyrics.
Conventionally, MIDI files starts with one header chunk containing information about the “instruments” playing the sounds, followed by track chunks containing the notes played and their durations, velocities (volume), etc.

The first thing I experimented was trying to find a Python library to dissect MIDI files. I chose mido after conducting some research. When I first attempted to do this using MIDO, there were syntax and logic errors in their example code, but it seems they’ve fixed that now last week. The library is quite easy to use.

from mido import MidiFile
mid = MidiFile('song.mid')
for i, track in enumerate(mid.tracks):
    print('Track {}: {}'.format(i, track.name))
    for message in track:
        print(message)
        
This is all the code required to read the information in the audio.  
![log](https://miro.medium.com/max/930/1*kVhhR7OsXtovWG6bRkYPkA.png)

Track zero includes much metadata about the midi, including its time stamp, tempo, etc. This part is not too important to this project.
Track one is where the data for how to play the song is stored. “note_on” messages contain information on the pitch, volume, and time that a note is played, which is the cruicial information need. (P.S.: the ‘time’ value represents delay after last message. So if time is 0, it means this note is played at the same time as last note). For every single note, I rounded its duration to the nearest 250 milliseconds and grouped it with every note that was played at the same time that it was.
Then I used a script I wrote (parser.py) to isolate all the “note_on” messages in the tracks and group them into a graph of progressions
![graph](https://miro.medium.com/max/820/1*_1_LSDlgkCQIN3DIlrPddw.png)\
This is the adjancent matrix I acquired from the graph I generated. We can represent it this way because we only care about the edges between the nodes and the frequency a particular note transitions to another note. For clarity, we will only care about the duration of the note being transitioned to and the number of times that note was transitioned to.
       C (500 ms) | D (250 ms) | F# (250 ms) | A (750 ms)
C       0            2            1             1
D       2            0            0             2
F#      1            0            0             1
A       1            1            0             1

Inside the Python, I represented it using dictionary, which is the HashMap implementation in Python. I stored these notes based on the conversion in the official document of MIDI.
![graph](https://miro.medium.com/max/645/1*GUQ8Q3yil6EjSrsbd-whcw.png)\
This is a fraction of the River Flows in You's breakdown:
![graph](https://miro.medium.com/max/1525/1*M_U2kn9-o689fUV7bFgRww.png)\
Since River Flows in You is written in A major, it is reasonable that there are a lot of transitions from note 81 (A6). It transitions to note 80, duration 500ms (G# in 6th octave) a total of 28 times.\

Now finally, we can generate music! I’m going to give initial push with a random note, search it in the matrix, and choose a random note that it transitions to (based on the post probability), weighted toward the more frequent transitions. 

## Code
I have uploaded 4 code files: 
Generator.py
json_handler.py
markov_chain.py
parser.py

## Results

Both the original and the generated audios are in the repository. I uploaded both the mp3 and midi version of the generated music.

## Technical Notes

My project requires fluidsynth framework installed in order to route MIDI in your computer. In order to use this pyfluidsynth library, you may install fluidsynth's version 1.1.x. Other common libraries such as NumPy is required as well.

## Reference

http://www.music-software-development.com/midi-tutorial.html
https://en.wikipedia.org/wiki/Markov_chain
