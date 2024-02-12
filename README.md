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
