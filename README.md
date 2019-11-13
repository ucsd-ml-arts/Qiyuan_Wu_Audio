# Project 3 Generative Audio

Qiyuan Wu, qiw103@eng.ucsd.edu


## Abstract

I used a set of instructions to build a markov chain in python and play it using FluidSynth Midi synthetiser. The instructions are generated from a MIDI file (.mid) and converted into json format using ToneJS Midi. Then, they are fed into a simple markov chain that generates midi phrases out of the ones from the original track, and playes them using pyfluidsynth.

In this example, Chopin Concerto No1 E Minor Op11 and River Flows In You are used to generate the instructions in the markov chain. Both the original and generated track's Midi File from the MIDM database.

## Model/Data

- trained models
I used Markov chain model, which is a stochastic model describing a sequence of possible events in which the probability of each event depends only on the state attained in the previous event. Essentially, Markov chains are mathematical systems that track the probabilities of state transitions. It's usually used to model complex systems and predict behavior. They’re used in many commercial applications, from text autocomplete to Google’s PageRank algorithm. 

- training data (or link to training data)
Because of the concise and accurate property of their structure, I chose to use MIDI files for this project. MIDI files are simple files that consist of chunks which contain information about the music encoded in the file. A significant distinction to note is that MIDI files are not playable audio files like MP3 files. Rather, they contain instructions on how to play tunes, which can be played by numerous different computer generated instruments. Due to this property, they are limited in that they can only store a certain range of notes and cannot store complex audio like vocal lyrics.
Conventionally, MIDI files starts with one header chunk containing information about the “instruments” playing the sounds, followed by track chunks containing the notes played and their durations, velocities (volume), etc.

## Code

Your code for generating your project:
- Python: generative_code.py
- Jupyter notebooks: generative_code.ipynb

## Results

In the repository

## Technical Notes

Any implementation details or notes we need to repeat your work. 
- Does this code require other pip packages, software, etc?
- Does it run on some other (non-datahub) platform? (CoLab, etc.)

## Reference

References to any papers, techniques, repositories you used:
- Papers
- Repositories
- Blog posts
