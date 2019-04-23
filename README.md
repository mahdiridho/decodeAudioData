# decodeAudioData
Different results of the channel data between audiocontext.decodeAudioData and octave reference (expectation)


## Case
We have a client app built with Google Polymer 3 implementing Audiocontext API to decode audio data. From our analyzing, the decoder returns different result of channel data to our reference/expectation. We use octave software as the reference.

On the folder audiofile, there is a sample wav file to be experimented.


## Run
* Open the file index.html on browser
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
10: -0.27878567576408386
11: -0.13389098644256592
12: 0.07916242629289627
13: 0.18276247382164001
14: 0.11339849978685379
15: -0.03214486315846443
16: -0.11864637583494186
17: -0.08897825330495834
18: 0.006309896241873503
19: 0.07485105097293854
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

* Load the audio data into the vector h

```
> h=audioread('./audiofile/h.wav');
```

* Look at the first 20 sample points of the audio data on the octave console

```
> h(1:20)
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
  -0.204190
  -0.268489
  -0.131052
   0.069502
   0.179210
   0.140048
   0.010775
  -0.098861
  -0.115960
  -0.047979
```


### Expectation
The data we load into the browser should be identical or scaled to octave result


### Result
Both results are different and not identical nor scaled


## How the client app work?
* Read the audio file as ArrayBuffer using FileReader web API
* Decode the ArrayBuffer using AudioContext::decodeAudioData API
* Print out the channel data using getChannelData()