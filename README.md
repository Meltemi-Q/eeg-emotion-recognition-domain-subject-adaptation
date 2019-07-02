# eeg-emotion-recognition
EEG Emotion Recognition project, experiment on SEED (SEED-IV), DEAP dataset

### Database

- DEAP:
	- 32 participants
	- 40 one-minute videos
	- 40 channels (32 first channels are EEG)
	- 4 unique emotion state: arousal, valence, dominance, liking
	- After watching each video, each person was rating emotion point, ranging from 1.0 to 9.0 for each state. We applied our proposal method for binary classification for each state. Ex: low/high arousal, low/high valence, .v.v.
	- The continuous rating is thresholded at 4.5. Therefore, if the rating was higher or equal to threshold, the emotion of this video was classified as high emotion, and vice versa.
	- Metadata:
		- Sampling rate: 128Hz

- SEED-IV:
	- 15 participants
	- 3 sessions, 1 session ~ 24 trials (24 videos) = 24 * 3 == 72 unique videos
	- 62 EEG channels
	- 4 emotions: happy, sad, neutral, fear
	- For each session, 24 videos showed for each person and EEG signal are collected with the 62-channels ESI NeuroScan System.
	- Different trials (videos) have different samples because the length’s film clips are not the same. 
	- Metadata:
		- Sampling rate: 200Hz

### Some common pitfalls:

- Train-test-split scenarios.
- Curse of dimensionality: various number of custom features → decrease model’s acc

### Train-test-split scenarios:

- Random-train-test
- Subject-dependent: video-based. Ex: 40 videos, 30 for training, 10 for testing
- Subject-independent (a.k.a Cross-subject & leave-one-subject-out): 15 people, train on 14, test on the left one.

### Preprocessing and feature extraction:

- Bandpass filter
	- DEAP: 4.0 - 45.0 Hz
	- SEED: 1.0 - 50.0 Hz

- Artifact removal

- Segment signal:
	- DEAP (1s) - 128 samples / segment
	- SEED (4s) - 800 samples / segment

- Feature smoothing:
	- LDA: linear dynamical system 
	- Moving average

- Feature extraction:
	- PSD (FFT) - STFT
	- DE - Different Entropy
	- Wavelet Transform (DWT, CWT)
	- Ensemble Wavelet Transform (entropy; statistic: median, mean, std, var, ..; crossing; …)
	- Ensemble features extraction (PSD, ensemble wavelet, hjorth, entropy, ...): 

- Feature selection:
	- ANOVA
	- RFE (most reference), ...

### Model
	- CNN-1D, CNN-2D
	- LSTM (apply on raw data and feature extracted)
	- SVM
	- RF
	- Gradient Boosting

### Result

- WIP