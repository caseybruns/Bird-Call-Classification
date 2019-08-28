# Bird-Call-Classification
## Problem Statement
- **Shazam for birds**
- This project is the beginings of building a working model that can predict species from a audio recording of a bird call/song. Cornell Lab of Ornithology has already done this and put it into an app. This project's goal was to be able to create that application and try and improve apon it. Many groups studing population density and diversity around the world could use this technology to make faster and more informed descions on land and resource management if they are able to know who's there.

## Data Description
**Ideal:**
- Birds: 765 species from 23 different families
- Size: Estimate roughly 1TB of wav file data


**Actual:**
- Birds: 10 species (Chosen for birds that live in Austin, TX at somewhat random)
    - Monk Parakeet
    - Great Horned Owl
    - Carolina Wren
    - Blue Jay
    - Painted Bunting
    - Great-tailed Grackle
    - Red-shouldered Hawk
    - Lesser Goldfinch
    - House Finch
    - Northern Cardinal
- Size: 30GB, 2,084 individual wav files

### Pre-processing
- Cleaning
    - Using a sound envelope, I was able to reduce some of the effect from random noise. This is hard to automate for so many files, but I was able to reduce it for most of the data.
- Fourier Transform
    - Also known as a power spectrogram, this transformation plots power(y) by frequency(x). This serves as a way to understand how far down I should down sample the audio as well as prequsit for Filter Bank Coefficient.
- Filter Bank Coefficient
    - This transformation plots frequency(y) by time(x). The audio at this point has been down-sampled. In an effort to mimic animal hearing range, the audio was put under triangular filtering to expand and capture more detail at the lower frequencies and collapse the larger, less informative frequencies.
- Mel Frequency Cepstrum Coefficient
    - This tranformation is again frequency(y) by time(x), but the audio information has been cut down to improve model efficiency. Additionally, the data goes through a descrete cosine transformation to decorrelate the sound files.
- Sampling
    - The last step before input the data into the model is creating samples of the data. I chose to sample half second increments. These half second MFCC's are what is transformed into numbers that represent power at every frequency for every time. This vector is what the model is using to learn the differences in sound.
    
## Modeling
**Idealy**
- Using a powerful GPU instance on AWS, being able to download all the audio for 765 species using Selenium and then running a convolutional neural network on the cleaned and MFCC tranformed data. 

**Actually**
- Using my laptop, I was limited on how much data I could pull down and how many times I could run my model. So I was only able to run a cnn with 10 species. This took several hours and I was only able to make it to the 4th epoch before having to shut it down. By this 4th epoch my model reached 67% accuracy.

## Moving Forward
- I have every intension of seeing this project to the end, or at least where I thought it should end. With a working model of all 765 species that can be used as shazam for birds.

## Acknowledgements
- Seth Adams [GitHub](https://github.com/seth814/Audio-Classification) and [YouTube Channel](https://www.youtube.com/watch?v=Z7YM-HAz-IY&list=PLhA3b2k8R3t2Ng1WW_7MiXeh1pfQJQi_P&index=1) really help me understand the preprocessing stage of my project.
- James Lyons [GitHub](https://github.com/jameslyons/python_speech_features) was used for the python_speech_features library.
