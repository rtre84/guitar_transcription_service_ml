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

### Overview
This repository is a proof-of-concept that turns an isolated guitar track from YouTube into guitar tablature using a Colab/Jupyter notebook workflow. There is no conventional package structure; everything lives in a single notebook (`GuitarTranscription.ipynb`) alongside the `README.md`. The notebook interleaves code and shell commands to download audio, convert it to MIDI, generate tablature, and optionally render MIDI back to audio.

---
`NOTE: Below explanation generated using ChatGPT Codex. The explanations and suggestions are sound and similar to what I've stated in notebook comments.`

### General Structure
1. **Environment setup**  
   - Installs Miniconda for Python 3.9 and uses `apt`/`pip` to fetch dependencies such as `ffmpeg`, `yt-dlp`, `basic-pitch`, `tuttut`, and a fork of `guitar-tabs-to-MIDI`.  
   - Designed for Google Colab, so local execution may require adapting package versions and system libraries.

2. **Audio download**  
   - Defines `download_youtube_audio(youtube_url, output_dir, filename)` which uses `yt-dlp` and `ffmpeg` to extract the best audio track from a YouTube link.  
   - Warns that downloading from YouTube might violate the platform’s Terms of Service.

3. **Audio → MIDI**  
   - Uses Spotify’s open‑source **Basic Pitch** CLI to convert the downloaded `.mp3` into a `.mid` file.  
   - Generates MIDI into an `output/` directory, expecting a single file named after the input audio.

4. **MIDI → Guitar Tabs**  
   - Installs a fork of **Tuttut** (midi‑to‑guitar‑tab converter) modified for notebook use.  
   - Copies the MIDI into a `midis/output/` directory and runs `tuttut-fork/tuttut/midi_tabs_cli.py` to create tablature in `tabs/`.  
   - The algorithm chooses fret positions via shortest‑path search on the guitar neck; the README notes this is not always how humans finger notes, so it’s an area for improvement.

5. **Tab → MIDI (optional)**  
   - Clones a fork of **guitar-tabs-to-MIDI** to convert generated tablature back into MIDI.  
   - Allows side‑by‑side comparison between original and tab‑derived MIDI for evaluation.

6. **Playback / Visualization**  
   - Uses IPython’s `Audio` widget to attempt MIDI or WAV playback.  
   - Contains commented guidance on converting MIDI to WAV using libraries like `pretty_midi` or `fluidsynth` if direct playback fails.

---

### Important Things to Know
- **Notebook-centric**: There’s no modular Python package; the pipeline runs sequentially in the notebook.  
- **Heavy external dependencies**: Requires `ffmpeg`, `yt-dlp`, and several niche libraries (Basic Pitch, Tuttut, guitar-tabs-to-MIDI).  
- **Colab assumptions**: Paths and installation commands assume a Google Colab environment; local replication may demand Docker or virtual-env work.  
- **Manual/experimental steps**: Some cells are exploratory or commented out. The workflow isn’t fully automated and may require manual intervention when run elsewhere.  
- **Focus on isolated guitar tracks**: Quality of transcription drops with complex mixes. The workflow is optimized for single-instrument guitar stems.

---

### Suggested Next Steps for Learners
1. **Understand external tools**  
   - Study [Spotify’s Basic Pitch](https://github.com/spotify/basic-pitch) for audio-to-MIDI techniques.  
   - Explore [Tuttut](https://github.com/urin/tuttut) and its forks to learn how MIDI is mapped to guitar tablature.  
   - Review the `guitar-tabs-to-MIDI` fork to see how tablature is parsed back into MIDI events.

2. **Packaging and automation**  
   - Convert notebook cells into Python modules or CLI scripts so the pipeline can be run headlessly.  
   - Use `virtualenv`/`conda` or Docker to encapsulate dependencies.  
   - Add tests to ensure each step (download, conversion, tab generation) produces expected outputs.

3. **Algorithmic improvements**  
   - Improve fretboard position selection (e.g., incorporate fingering heuristics or machine learning to mimic human choices).  
   - Investigate better evaluation metrics to compare original audio, generated MIDI, and final tabs.

4. **Audio/MIDI fundamentals**  
   - Learn about MIDI format, guitar tab notation, and music information retrieval (MIR).  
   - Explore signal processing basics—spectrograms, pitch detection, and onset detection—to understand what Basic Pitch and similar models do internally.

5. **User interface & distribution**  
   - Consider building a web or desktop UI that wraps the pipeline for less technical users.  
   - Package the workflow as a Python library or web service for broader reuse.

---

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
