# decodeAudioData
Different results of the channel data between audiocontext.decodeAudioData and octave reference (expectation)


## Case
We have a client app built with Google Polymer 3 implementing Audiocontext API to decode audio data. From our analyzing, the decoder returns different result of channel data to our reference/expectation. We use octave software as the reference.

On the folder audiofile, there is a sample wav file to be experimented.


## Run
* Open the file index.html on chrome browser
* Select the audiofile/h.wav file
* See the log result of channel data, will be like :

```
0: 0.738193154335022
1: 0.17993010580539703
2: 0.143886536359787
3: -0.49501433968544006
4: -0.581611156463623
5: -0.07922420650720596
6: 0.25858914852142334
7: 0.42484045028686523
8: 0.12840349972248077
9: -0.15169838070869446
...
```


## Compare
* Install first octave software :

```
sudo apt-get install octave
```

* Run the octave :

```
octave-cli
```

* Load the audio data

```
> audioDump
```

* Look at the fs and first 10 sample points of the audio data on the octave console

```
fs =  48000
ans =

   1.000000
  -0.059232
   0.408143
  -0.503169
  -0.554996
  -0.336158
   0.122070
   0.389484
   0.336810
   0.057144
```


### Expectation
The data we load into the browser should be identical or scaled to octave result


### Result
Both results are different and not identical nor scaled


## How the client app work?
* Read the audio file as ArrayBuffer using FileReader web API
* Decode the ArrayBuffer using AudioContext::decodeAudioData API
* Print out the channel data using getChannelData()


## Problem Solving
1. We have to know the audio file sample rate before create audiocontext instance
2. Once we know the audio file sample rate, set it on audiocontext initialization :

```
var audioCtx = new (window.AudioContext || window.webkitAudioContext)({
  sampleRate: <audio_file_sample_rate>
});
```
3. Now, we can decode the audio data through Audiocontext and get the same result as octave reference

Note : Currently, the sampleRate of an AudioContext can only be set manually in Firefox and Chrome 74+