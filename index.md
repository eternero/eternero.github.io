---
layout: default
title: "3M-RS"
---

# About
Our project, 3M-RS proposes the development of a Multi-Modal Music Recommendation System. The approach
that we propose departs from traditional solutions. Instead of heavily relying on **Collaborative Filtering** (CF)
and past user behavior, which have shown to cause issues like _popularity bias_ and _filter bubbles_,
our solution is built around the intrinsic characterisics of the music itself.

By leveraging audio analysis, signal processing, user-generated content (e.g. social tags), and
direct user input, our system aims to offer a more equitable, transparent, and user-controlled recommendation
experience which aims to stray away from the issues observed in other solutions.


# What data do we use?
As it was just mentioned, we use three primary sources to create an _audio profile_ of sorts for
the music in our dataset. These sources will be discussed in detail in the sections below.


## Music Information Retrieval (MIR) Models and Algorithms
The main driving force behind our project is the usage and application of Music Information Retrieval
models and algorithms. By using this, we're able to retrieve significant features from tracks such as
_tempo, timbre, instrumentality, acousticness, MFCC_ and more.

This also allows us for the creation of _individual audio profiles_ using high-dimensional features like
_timbre, mel-frequency coefficients_ and _pitch_. This combination of numerical and high-dimensional features
enables us to capture in great detail the distinct features of music – which later on allows us to be
able to make intricate comparisons which lead to accurate recommendations.

It is worth mentioning that we source most of our models and algorithms from **Essentia** \[1] with the additional
usage of **HarmoF0** \[2] as our Pitch-Estimating Model and the **Spotify API** to retrieve song popularity.


## User Generated Content
While our project does deviate from CF-Based approaches, it is still important to attempt to capture
the subjective and socially perceived characteristics of music. We aim to do this by retrieving
release data from RateYourMusic (RYM) such as _Genre, Subgenres, Descriptors, Scenes_ and _Movements_.

By carefully processing this data and converting it into embeddings, we're then able to turn these into
significant features for our tracks and even being able to be used as a filtering option – for example,
users would be able to filter results to include or exclude the genres in their input.


## Signal Processing

Signal processing is a fundamental component of our project, playing a vital role in transforming raw audio into meaningful representations. Our system utilizes various mathematical transforms to analyze and extract essential characteristics from music. These transformations allow us to decompose signals into components that reveal structure, pitch content, and compressibility. All relevant transform implementations are applied to our algorithm.

### Fourier Transform

The Fourier Transform (FT) allows us to break down a time-domain audio signal into its frequency components. This is especially valuable when analyzing complex musical compositions composed of overlapping tones. Our implementation applies FT to visualize and extract dominant frequencies in each track.

By identifying which frequencies are most prominent in a song, we can infer pitch content, tonal complexity, and harmonic relationships. This is useful in clustering similar-sounding tracks, building timbral profiles, and providing recommendations based on musical structure rather than popularity metrics.

### Constant-Q Transform

The Constant-Q Transform (CQT) is well-suited for music due to its logarithmic frequency scale, which mirrors human pitch perception. Unlike FT, CQT provides higher frequency resolution at lower pitches exactly where musical detail often resides. Our implementation extracts musical notes and harmonic patterns from audio signals.

CQT enhances our ability to detect instrument specific timbres, distinguish overlapping notes, and identify musical motifs. These capabilities are critical for producing accurate, musical recommendations. In particular, CQT helps the system recommend songs with similar melodic or harmonic structure, even if the genre or instrumentation differs.



# Current Progress

Since the beginning of the project, out primary focus has been on understanding and capturing the complex nature of music. To accomplish this we've dedicated substantial effort to the study and implementation of advanced audio feature extraction techniques, which form the backbone of our recommendation system.
  
## Track Fingerprinting: Feature Research and Implementation

We conducted an in-depth technical analysis of Essentia’s **algorithms**, focusing on how these descriptors can improve our track fingerprinting process. The goal was to capture core musical characteristics that go beyond traditional metrics like tempo or loudness, providing a deeper comprehension of timbre, brightness, and dynamics.

Our list of implemented features include:

- **RhythmExtractor2013**: Extracts tempo and beat positions, good for understanding the traks pacing.
- **Energy**: Measure the overall energy of the track, good for identifying high-energy and calm, softer tracks.
- **LoudnessEBUR128**: Quantifies perceived loudness and dynamic range based on industry standards.
- **SpectralCentroidTime**: Measures the brightness of a track, distinguishing between bright sounds and darker, bass-heavy ones.
- **RollOff**: Measures how much of the signal's energy is under the specified percentage part of a spectrum. Excellent to identify false-positive when a track has high percutions but is dark.
- **SpectralContrast**: Captures the harmonic textures
- **HFC**: Highlights energy in higher frequencies
- **Flux**: Measures the rate of spectral change, captures the dynamic progression and energy shifts within a track. 
- **FlatnessDB**: Distinguishing between harmonic, melodic content and noisy, chaotic textures like percussive or distorted sounds.
- **EnergyBandRatio**: Breaks the tracks frequency spectrum into bands, this offer a detailed insight into the energy distribution inside each band.
- **SpectralPeaks**: Good for analyzing dominant frequency peaks to understand its harmonic structure.
- **MFCC**: Great at capturing timbral characteristics, widely used in speech recognition and audio analysis. 
- **GFCC**: Provides a more robust, noise resistant timbral profiling than MFCC, inspired by the human auditory perception.

This comprehensive `toolbox` of features enables our system to **capture the unique audio signature of each track**

## Feature Documentation and Analysis

To ensure transparency and maintainability, we have fully documented each algorithm:
- **Purpose**: Why is this algorithm useful in our music analysis.
- **Unique** Value: How it complements our system and what makes it unique.
- **Interpretation**: What its output reveal about the track. 

This documentation will support future development, help guide future selection, and form the foundation for our eventual recommendation model.
## Next step ???
As we move forward, we'll be focusing on:
- Implement the distance-based similarity methods with the newly integrated algorithms.
- Growing our dataset.
- Creating the initial prototype of our recommendation engine.


# References
\[1] Bogdanov, D., Wack N., Gómez E., Gulati S., Herrera P., Mayor O., et al. (2013). ESSENTIA: an Audio Analysis Library for Music Information Retrieval. International Society for Music Information Retrieval Conference (ISMIR'13). 493-498.

\[2] W. Wei, P. Li, Y. Yu and W. Li, "Harmof0: Logarithmic scale dilated convolution for pitch estimation", IEEE International Conference on Multimedia and Expo (ICME), pp. 1-6, 2022.

\[3] T. Akiba, S. Sano, T. Yanase, T. Ohta, and M. Koyama, “Optuna,” Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pp. 2623–2631, Jul. 2019. doi:10.1145/3292500.3330701