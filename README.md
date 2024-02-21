# Sample Generation
### CSE 40868 - Neural Networks
### Sam Webster

## Part 0: GitHub setup and topic selection
**Project Topic**: Music sample/audio generation\
**Group Members**: Samuel Webster\
**GitHub Repo**: Here! (May end up using a Kaggle/Colab notebook, not sure yet)


## Part 1: Conceptual Design

My project idea is to create a generative neural network for audio, specifically in the application of music production. In music production, short audio clips are called samples. The goal of this project is to generate percussive samples, ideally from multiple types of percussive instruments, such as kicks, snares, hi-hats, and cymbals. 

This project requires a neural network with generative capabilities. A popular machine learning framework for this is Generative Adversarial Networks (GANs), which I often hear about in the context of image generation. An architecture that you suggested I research for this application is Variational Auto-Encoders (VAEs), which are versatile and would a good stepping stone for adapting to this project on audio generation. 

As for data, there are plenty of accessible sample packs on the internet. Sample packs are, as their name suggests, bundled packs of audio samples for music production. Preparation of data would involve collecting drum samples from multiple sample packs and grouping them by their percussive instrument. I would also need to add some stage of data cleaning/preparation that ensures the dataset is cohesive since the individual samples would originate from multiple different sources. For training, validation, and testing, this conglomerate of samples can be divided into sections and used for their respective purposes. I will probably do a split such as 70% training, 15% validation, and 15% testing, which my internet research indicates is a good middle ground for data splitting. I imagine my quantity of data will be on the lower side, but the data will also be diverse. Balancing having enough data to train on with a wide enough range to validate/test on will be important for this project. One thing I am still considering is evaluation metrics. An option is sonic similarity between generated samples and validation/testing sets. 

As I mentioned in my Part 0 submission, I am inspired to create this project by a startup I’ve been following called Soundry. Soundry’s product is text-to-sample generation, where the user can describe what sound they want to create. While text-based input is most likely out of the range of this semester project, I really like how the implementation of text allows the user to describe attributes about the sound they want created. For example, a user may want a “boomy kick” with lots of bass and reverb, versus wanting a “punchy kick” with a dry sound and high frequency impact. The text element allows the user to have much more control over sound, which is of course desirable. If possible as a future scope goal, I would like to be able to add genre selection to the generation, as many sample packs are divided by genre. If a user is creating an electronic track needs a kick they could select kick → electronic. A lo-fi track producer in need of a snare might select snare → lofi. This implementation could allow much more control over my model’s generation capabilities and make it generally much more useful for music production. 

As suggested, I pasted my project info into ChatGPT and asked for advice as a brainstorming buddy. It suggested I research how audio is represented digitally so that I may adapt a neural network to train and generate it. It also suggested that I can use data augmentation to artificially expand the size of my dataset through pitch shifting, time warping, and adding noise, which I think is a great idea. I think that overall ChatGPT will be a good resource moving forward to help me think through project development and give me ideas on how to progress through the project. 

I am completing this project individually.

## Part 2: Datasets
For this project, I will be using the NSynth dataset provided by Google Magenta.

Dataset: https://magenta.tensorflow.org/datasets/nsynth <br>
Original GANSynth post: https://magenta.tensorflow.org/gansynth

I mentioned in the previous section that I would be amassing a dataset of my own by combining existing accessible sample packs. However, in my research of other audio synthesis research projects, I learned that Google Magenta's NSynth dataset is available for use. This dataset was originally used by Magenta for their 2019 project GANSnyth, which achieved a very similar goal of an audio generation from trained audio samples. 

This dataset is markedly different from what I aimed to collect previously: the samples in the NSynth dataset are tonal, versus the percussive samples I aimed to gather before. Technically, this shouldn't cause any difference, it just means that I will be training on and generating tonal samples instead of percussive ones. This change is not a dealbreaker to me at all. I'd even go as far as saying I think it will make the audio generation more fun! 

There are many benefits to this dataset compared to what I planned on doing before. Each sample in this set comes with plenty of metadata annotating the sound's quality, such as it's instrument, instrument family, and sonic attributes (which is what I described as wanting in the previous section!). By incorporating these qualities as inputs to training my model, it will allow for the control of sound that I desire. On top of the great amount of data associated with each sound in the dataset, there is another benefit of using this dataset: it is huge! It contains 305,979 tonal samples, with variance in pitch, intensity, and timbre. This scale of sound data  was achieved by doing the same thing that ChatGPT suggested I do previously: sounds are sampled at as many MIDI pitches that are within their range, and at five different velocities. So, for a single sample, there are up to 440 variably pitched and velocity'd sounds. The 305k sounds are extracted from 1,006 instruments in this manner, giving a wide variety of sounds to be learned. 

This dataset is already divided into non-overlapping train, validate, and test splits. There are 289,205 samples in the train set, 12,678 samples in the validation set, and 4,096 in the test set. This is about a 94/4/2, which is quite narrow on testing. I suspect this choice was to maximize sample diversity in the training set. I will start by using this same split, but will change if I feel I am being limited by having such a small test size compared to training size. 

Here is an example entry of the dataset:
```"bass_synthetic_033-022-050": {
    "note": 201034,
    "sample_rate": 16000,
    "instrument_family": 0,
    "qualities": [
        0,
        1,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0
    ],
    "instrument_source_str": "synthetic",
    "note_str": "bass_synthetic_033-022-050",
    "instrument_family_str": "bass",
    "instrument_str": "bass_synthetic_033",
    "pitch": 22,
    "instrument": 417,
    "velocity": 50,
    "instrument_source": 2,
    "qualities_str": [
        "dark"
    ]
}
```
