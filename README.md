# Project 3 Generative Audio

Qiyuan Wu, qiw103@eng.ucsd.edu


## Abstract

I used a set of instructions to build a markov chain in python and play it using FluidSynth Midi synthetiser. The instructions are generated from a MIDI file (.mid) and converted into json format using ToneJS Midi. Then, they are fed into a simple markov chain that generates midi phrases out of the ones from the original track, and playes them using pyfluidsynth.

In this example, Chopin Concerto No1 E Minor Op11 and River Flows In You are used to generate the instructions in the markov chain. Both the original and generated track's Midi File from the MIDM database.

## Model/Data

-
I used Markov chain model, which is a stochastic model describing a sequence of possible events in which the probability of each event depends only on the state attained in the previous event. Essentially, Markov chains are mathematical systems that track the probabilities of state transitions. It's usually used to model complex systems and predict behavior. They’re used in many commercial applications, from text autocomplete to Google’s PageRank algorithm. 

- 
Because of the concise and accurate property of their structure, I chose to use MIDI files for this project. MIDI files are simple files that consist of chunks which contain information about the music encoded in the file. A significant distinction to note is that MIDI files are not playable audio files like MP3 files. Rather, they contain instructions on how to play tunes, which can be played by numerous different computer generated instruments. Due to this property, they are limited in that they can only store a certain range of notes and cannot store complex audio like vocal lyrics.
Conventionally, MIDI files starts with one header chunk containing information about the “instruments” playing the sounds, followed by track chunks containing the notes played and their durations, velocities (volume), etc.

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
