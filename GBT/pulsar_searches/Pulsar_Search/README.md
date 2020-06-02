# Pulsar Signal Folding - Breakthrough Listen Data

#### By Peter Ma | [Contact](https://peterma.ca/)
This notebook illustrates the implementation of pulsar folding and searching techniques from search. It finds the period of pulses within noisy data. (Below is a showcase of how "random" pulsar data can appear without proper algorithms)

Check out the [Notebook Tutorial](Pulsar_DedisperseV3.ipynb)

<p align="center"> 
    <img src="https://github.com/PetchMa/pulsar_notebooks/blob/master/assets/FAST_folding.gif?raw=true" >
</p>

# Brute Force Dedispersion Techniques 
When pulses reach Earth they reach the observer at different times due to dispersion. This dispersion is the result of the interstellar medium causing time delays. This creates a "swooping curve" on the radio spectrogram instead of plane waves. If we are going to fold the pulses to increase the SNR then we're making the assumption that the pulses arrive at the same time. Thus we need to correct the dispersion by shifting each channel down a certain time delay relative to its frequency channel. We index a  frequency column in the spectrogram. Then we split it between a time delay and original data and swap the positions.

But, the problem is, we don't know the dispersion measure `DM` of the signal. The DM is the path integral of the signal through the interstellar medium. What we can do is to brute force the `DM` value by running multiple trial `DM`s where we take the highest SNR created by the dedispersion with the given trial `DM`.
<p align="center"> 
    <img src="https://github.com/PetchMa/breakthrough/blob/master/GBT/pulsar_searches/Pulsar_Search/assets/dm.png?raw=true" width="250px">
</p>

<p align="center"> 
    <img src="https://astronomy.swin.edu.au/cms/cpg15x/albums/scaled_cache/wonderpulse-400x309.jpg">
</p>

# Fast Fourier and Fast Folding

Next, we apply the discrete Fourier transform on the data to detect periodic pulses. To do so, we look for the greatest magnitude of the Fourier transform. This indicates potential periods within the data. Then we check for consistency by folding the data by the period which the Fourier transform indicates.

The folding algorithm is simple. You take each period and you fold the signals on top of itself. If the period you guessed matches the true period then by the law of superposition it will increase the SNR. This spike in signal to noise ratio appears in the following graph. This algorithm is the following equation. 

<p align="center"> 
    <img src="https://github.com/PetchMa/breakthrough/blob/master/GBT/pulsar_searches/Pulsar_Search/assets/folding.png?raw=true" width="250px">
</p>



<p align="center"> 
    <img src="https://github.com/PetchMa/Pulsar_Folding/blob/master/assets/CAN_2.gif?raw=true">
</p>

Depending on the different periods we look at, the pulsar can have many profiles. For example with the same observation - instead, we look at a period of 0.19 seconds we get a different profile. The collection of profile forms the "fingerprint" of the pulsar. 

<p align="center"> 
    <img src="https://github.com/PetchMa/Pulsar_Folding/blob/master/assets/can_3.gif?raw=true">
</p>

# Questions?
Feel free to reach out to us if you're working with our data!



