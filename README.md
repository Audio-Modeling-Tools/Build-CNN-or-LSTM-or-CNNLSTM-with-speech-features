## Extract Speech Features and Train Deep Neural Networks

Inspiration for this workshop stemmed from this <a href="https://www.researchgate.net/publication/327350843_Dysarthric_Speech_Recognition_Using_Convolutional_LSTM_Neural_Network">paper</a>. I suggest downloading it as a reference. In this <a href="https://a-n-rose.github.io/2019/02/17/comparing-features-and-models-deep-learning-and-speech.html">post</a> I show via tables and graphs some experimentation results of this repo (training and implementing models w various speech features).

In this workshop, our goal is to experiment with speech feature extraction and the training of deep neural networks in Python. For my blog post on the features explored in this repo, click <a href="https://a-n-rose.github.io/2019/02/06/python-train-cnn-lstm-speech-features.html">here</a>.

Applying deep learning to the sound/ speech signal has many uses. We all know that it helps us to speak to Siri and Alexa, but it can also be used for security purposes, as in <a href="https://www.isca-speech.org/archive/interspeech_2015/papers/i15_2097.pdf">speaker verification</a>, <a href="https://people.xiph.org/~jm/demo/rnnoise/">noise reduction</a> when digitizing sound/ speech, and also in <a href="https://www.dw.com/en/voice-analysis-an-objective-diagnostic-tool-based-on-flawed-algorithms/a-17187057">healthcare contexts</a>, for example, identifying if a person has <a href="https://reader.elsevier.com/reader/sd/pii/S0952197618302045?token=B98CE82B0BE713AAA0653D37DF51401344710FD653E675D0900D0CE77C54070FD8AFBFBE1FB174169031EF17FCA7232C">Parkinson's</a>, <a href="https://ac.els-cdn.com/S2352872915000160/1-s2.0-S2352872915000160-main.pdf?_tid=d04d9cc3-f992-4820-af98-f083c847c322&acdnat=1549408007_fe358db560e7df5618e8d68875824413">Alzheimer's</a>, <a href="https://www.theverge.com/2014/7/17/5912491/diagnosing-sound-scientists-voice-recordings-Parkinsons-ADHD-Alzheimers">ADHD</a>, or various <a href="https://www.isca-speech.org/archive/Interspeech_2018/pdfs/1351.pdf">speech disorders</a>. I could go on.

In much of the research I have read, recurring speech features used in machine and deep learning are the <a href="http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/">Mel Frequency Cepstral Coefficients</a> (MFCC), the Mel Filterbank Energies (FBANK), which are similar but less filtered than the MFCC, as well as the <a href="https://ccrma.stanford.edu/~jos/sasp/Short_Time_Fourier_Transform.html">short-time fourier transform</a> (STFT) of the raw waveform. 

Additionally, deep learning neural networks I see quite often are the <a href="https://ujjwalkarn.me/2016/08/11/intuitive-explanation-convnets/">convolutional neural network</a> (CNN) and, for time series analysis, <a href="http://colah.github.io/posts/2015-08-Understanding-LSTMs/">long short-term memory</a> neural networks (LSTM), among others, but for this workshop, we'll stick with these.

Python offers libraries for audio analysis, <a href="https://librosa.github.io/">Librosa</a>, as well as for deep learning, <a href="https://keras.io/">Keras</a>. In this workshop, we will explore speech feature extraction using Librosa and the training of neural networks via Keras.

## Workshop Challenge Ideas:

Get a model(s) trained on your data and implement it as well:
* Was it successful?
* Where does it fail?
* What would you change to improve its performance?

Change the data to answer a specific question:
* How do the different networks handle similar sounding words?
* Are the models more or less robust when trained with speech mixed with noise?

Find a relavent paper, using STFT, FBANK, MFCCs and/or CNN, LSTM, CNN+LSTM models, and apply their methodology
* Does their methodology also work well with your question?
* If you change it (i.e. add noise to training data) does it improve how the model performs?

## Installation

For Installation instructions, see <a href="https://github.com/a-n-rose/Build-CNN-or-LSTM-or-CNNLSTM-with-speech-features/blob/master/INSTALLATION.md">here</a>.

## Run

After you have installed everything and downloaded/ set up your data, start up your virtual environment:

```
$ source env/bin/activate
```

As it is, the script 'extract_features.py' will extract only 5% of all the speech data. If you run the script 'as is', this will take appx. 6 minutes to complete.

```
(env)..$ python3 extract_features.py
```

This should print out something like this when it's done:

```
FOLDER NAME TO COPY AND PASTE FOR THE TRAINING SCRIPT:


features_and_models_20h32m31s

```

Note: If you come accross the following error: `fontconfig warning ignoring utf-8 not a valid-region tag`, see [here](https://stackoverflow.com/questions/24712158/how-to-solve-imagemagicks-fontconfig-warning-ignoring-utf-8-not-a-valid-regi) for a potential solution.

This is just a folder name with a unique time stamp. When you run the 'train_models_CNN_LSTM_CNNLSTM.py' script, it will prompt you to enter the folder with the prepared data. Simply paste this folder name there.

```
(env)..$ python3 train_models_CNN_LSTM_CNNLSTM.py

Using TensorFlow backend.


Which folder contains the train, validation, and test datasets you would like to train this model on?

features_and_models_20h32m31s

```

Press ENTER and it should start training! As is, the script should take appx. 4 minutes.

At the end, it will print out the name of the model you just created. If you would like to implement this model, copy this name and paste it in the 'implement_model.py' script (further instructions below).

```
If you want to implement this model, the model's name is:


CNNLSTM_speech_commands_4d13h41m48s

```

### OPTIONAL: IMPLEMENT THE MODEL

If you would like to implement the model, and test the model on speech you record, make sure you have installed the requirements for that (see INSTALLATION). Open the script 'implement_model.py'. Scroll to the bottom and enter the folder name (referred to above as 'features_and_models_20h32m31s') as well as the model name of the trained model you would like to test (referred to above as 'CNNLSTM_speech_commands_4d13h41m48s'):

```
if __name__=="__main__":
    
    project_head_folder = <ENTER FOLDER NAME>
    model_name = <ENTER MODEL NAME>
    
    main(project_head_folder,model_name)

```

When you run this, it will first record background noise; then it will prompt you to say something. (If you trained on words, say one of the words you trained on.) See how well it does!

In the workshop we will explore these scripts in detail, and change parameters to see how the training might be affected. Note: due to time constraints, we will not train on the entire dataset in the workshop. You are encouraged to do so at home, perhaps leaving the computer on and leave to extract features/ train through the night.

## Visualize Feature Extraction

If you would like to see visually what the various features look like, and how they look with added noise, beginning silence removal (vad - voice activity detection), etc. open the script 'visualize_features.py'. Once you have set the wavefile and features you would like to explore, run the script. This will create a new directory called 'visualizations' where visualizations will be stored. 

```
(env)..$ python3 visualize_features.py
```

## New Folders and Graphs

Once these scripts are through, you can look through the newly created files in your directory. You should see 'ml_speech_projects'. If you look in that folder, you will see a folder for each time you extracted features. It will have a name similar to this one:

```
features_and_models_20h32m31s
```

Inside of that folder you will find all of the train, validation, and train datasets, a folder showing graphs of how the model trained, the label the labels were encoded as, and other information as well.


## Future Use

You can explore other kinds of speech data, as well. I am collecting a list of free and available speech databases <a href="https://a-n-rose.github.io/2019/01/06/resources-publicly-available-speech-databases.html">here</a>. I offer directions for downloading a small dataset of female and male speech <a href="https://a-n-rose.github.io/2019/01/31/small-female-male-speech-data.html">here</a>. Note: in order to work with these scripts, the wavefiles need to be separated by class within the 'data' folder.

## Room for Improvement

1) Replicability and Randomization

I wanted to quickly train and compare many models without using only the same wavefiles, some of which might really suck. Therefore, right now, wavefiles are randomly assigned to train, validation, and test datasets. While it would be easy to implement a logging function, to document each time I extract features, which wavefiles were assigned to which dataset, as I am just experimenting, I don't want to busy my computer with more and more logging files. Furthermore, the noise is applied in varying strengths (0.25, 0.5, 0.75 the original volume). This variation in scale is applied at random. 

Fixes: 1) you can put together logging functionality to document the waves used in each dataset 2) assign the noise level to be just one number (I believe that's in the function "apply_noise" in the file "feature_extraction_functions.py".) 

2) Mixing of Noise

Right now, noise is mixed into the train, validation, and test datasets. I am exploring now if it's better to add the noise only to the train dataset. If that's the case, I will make that adjustment to the code as well.

3) Records a lot of background noise

I don't know if it's just my machine, but when I use sounddevice, a crazy amount of background noise is in the recording. I'm working on that.. just know if the same thing is happening to your recordings, you're not alone. And if you find a fix before I have, let me know what helped. 

