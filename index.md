---
layout: default
title: "3M-RS"
custom_css: style.css
---

# About
Our project, 3M-RS proposes the development of a Multi-Modal Music Recommendation System. The approach
that we propose departs from traditional solutions. Instead of heavily relying on **Collaborative Filtering** (CF)
and past user behavior, which have shown to cause issues like _popularity bias_ and _filter bubbles_,
our solution is built around the intrinsic characteristics of the music itself.

By leveraging audio analysis, signal processing, user-generated content (e.g. social tags), and
direct user input, our system aims to offer a more equitable, transparent, and user-controlled recommendation
experience which aims to stray away from the issues observed in other solutions.


# How does it work?
The main idea behind our project is rather easy to understand, and so is the user workflow! You provide some tracks
and you get recommendations that should be similar to your input. The steps below should serve as a quick user guide to understand
our project and get some recommendations!

1. **Provide an audio input** : This could be a single track or multiple, whichever you'd like.
2. **Provide preferences for filtering** : Indicate what type of songs you'd like to be recommended. For example, songs of the same
genre only or songs with high tempo.
3. **Wait for your results** : Once this has been done, all that is left is for the audio input to be processed through the _Audio Data Pipeline_
and for it to then be compared with the songs in our dataset. Once we get a result from those comparisons, we apply the provided preferences as
filters and provide the top recommendations to the user!

# What data do we use?
As it was previously mentioned, we use three primary sources to create an _audio profile_ of sorts for
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

The **Fourier Transform** (FT) allows us to break down a time-domain audio signal into its frequency components. This is especially valuable when analyzing complex musical compositions composed of overlapping tones. Our implementation applies FT to visualize and extract dominant frequencies in each track.

By identifying which frequencies are most prominent in a song, we can infer pitch content, tonal complexity, and harmonic relationships. This is useful in clustering similar-sounding tracks, building timbral profiles, and providing recommendations based on musical structure rather than popularity metrics.

### Constant-Q Transform

The **Constant-Q Transform** (CQT) is well-suited for music due to its logarithmic frequency scale, which mirrors human pitch perception. Unlike FT, CQT provides higher frequency resolution at lower pitches exactly where musical detail often resides. Our implementation extracts musical notes and harmonic patterns from audio signals.

CQT enhances our ability to detect instrument specific timbres, distinguish overlapping notes, and identify musical motifs. These capabilities are critical for producing accurate, musical recommendations. In particular, CQT helps the system recommend songs with similar melodic or harmonic structure, even if the genre or instrumentation differs.


# Current Progress and the Future
At the time being, we've been able to develop all of the core aspects of our project by now. This includes the _Audio Data Pipeline_, the _RYM User-Generated Content Extraction Module_,
_implementation of transform-based algorithms_ and more. Furthermore, we're also working on optimizing the core algorithms behind our recommendation system by using **Optuna** \[3] for
hyperparameter tuning with distinct distance metrics as our objective functions and changes in the handling of high-dimensional features.

As we go along with our project, we aim to optimize what has already been developed and to create a robust recommendation system that is able to fully capture the essence of music.
Even as we've already gotten significant progress and amazing results from our first few tests with the current recommendation system, we're still constantly looking for ways to
improve our system, such as implementing new features that are highlighted in relevant literature and working around constraints that come about, whether it be the heavy
computational cost of Music Information Retrieval Models or lack of social tags from services like Spotify or RateYourMusic.


# References
\[1] Bogdanov, D., Wack N., Gómez E., Gulati S., Herrera P., Mayor O., et al. (2013). ESSENTIA: an Audio Analysis Library for Music Information Retrieval. International Society for Music Information Retrieval Conference (ISMIR'13). 493-498.

\[2] W. Wei, P. Li, Y. Yu and W. Li, "Harmof0: Logarithmic scale dilated convolution for pitch estimation", IEEE International Conference on Multimedia and Expo (ICME), pp. 1-6, 2022.

\[3] T. Akiba, S. Sano, T. Yanase, T. Ohta, and M. Koyama, “Optuna,” Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pp. 2623–2631, Jul. 2019. doi:10.1145/3292500.3330701