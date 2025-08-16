# Music to Guitar Tab Transcriber

This Collab Notebook lays out the steps to convert an isolated guitar track from Youtube to Guitar Tabs and evaluate generated tabs.

## The Why?

Guitar tabs are a relatively easy way to represent music primarily music played on a guitar or similar stringed instrument. Sheet notation is what is formally used in a lot of settings but reading sheet music isn't exactly the easiest. Guitar tabs have won the hearts and minds of a lot of people.

- Easier to read, learn and comprehend
- More specific in some contexts
- Playable formats exist that make learning and comprehending even easier

<img width="784" height="497" alt="reaperSheetMusic" src="https://github.com/user-attachments/assets/4a7998a2-4e3b-43d6-98e6-6dfa7ff2fb59" />


Compare that to Guitar tabs below

<img width="671" height="343" alt="reaperTab" src="https://github.com/user-attachments/assets/eabad079-137a-4e00-930d-7b9c26d720a0" />


So we now have a readable or easier format to deal with but there's a problem. Creating guitar tabs (or sheet music for that matter) is no easy task. There are experts and transcribing music is a huge part of the learning process but finding transcriptions for songs you like becomes a hard task when you look for less popular or more niche music. The quality of tabs also vary.

The best and accurate tabs are usually done by musicians who do it professionally and this in turns takes time and money. So a niche piece of music or even more technical music is even harder to find and transcribe. This is a problem that AI and ML can help solve.

## Pipeline

![gtpipeline](https://github.com/user-attachments/assets/67dd0297-0b90-4f23-9d66-ed638ece811d)

## Current Version
The current python notebook code was written to run in a Collab notebook. Certain dependencies have been forked and changed to run in that environment. 

## TODO
- The current python notebook code needs to be ported to run on a local Jupyter notebook environment. Currently certain package python version and inconsistencies is what stops anyone from running this in the ver 3.9.12 for example.
- The code needs to be packaged better so it can be called in as a dependecy.
- The algorithm needs some love especially the graph traversal bit that finally decides where to fret. The current version finds the shortest path which doesn't translate a 100% all the time to how a human guitar player would arrange it. 
