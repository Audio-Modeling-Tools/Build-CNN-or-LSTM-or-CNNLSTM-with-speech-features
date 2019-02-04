## Extract Speech Features and Train Deep Neural Networks

In this workshop, our goal is to experiment with speech feature extraction and the training of deep neural networks in Python.

Applying deep learning to the speech signal has many uses. We all know that we can speak to Siri and Alexa, but speech can also be used for security purposes, as in <a href="https://arxiv.org/abs/1803.05427">speaker verification</a>, as well as in <a href="https://www.dw.com/en/voice-analysis-an-objective-diagnostic-tool-based-on-flawed-algorithms/a-17187057">healthcare contexts</a>, for example, identifying if a person has Parkinson's or if they have Attention Deficit Hyperactivity Disorder. While I just listed a couple, there are many other fields where the analysis of the speech signal is relevant.

In much of the research I have read, recurring speech features used in machine and deep learning are the <a href="http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/">Mel Frequency Cepstral Coefficients</a> (MFCC) and the Mel Filterbank Energies (FBANK), which are similar but less filtered than the MFCC.

Additionally, deep learning neural networks I see quite often are the convolutional neural network (CNN) and, for time series analysis, long short-term memory neural networks (LSTM).

Python offers libraries for audio analysis, <a href="https://librosa.github.io/">Librosa</a>, as well as for deep learning, <a href="https://keras.io/">Keras</a>. In this workshop, we will explore speech feature extraction using Librosa and the training of neural networks via Keras.

## Installation

For Installation instructions, see <a href="https://github.com/a-n-rose/Build-CNN-or-LSTM-or-CNNLSTM-with-speech-features/blob/master/INSTALLATION.md">here</a>.

## Run

After you have installed everything, start up your virtual environment:

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

features_and_models_2019y2m2d22h6m19s

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

## New Folders and Graphs

Once these scripts are through, you can look through the newly created files in your directory. You should see 'ml_speech_projects'. If you look in that folder, you will see a folder for each time you extracted features. It will have a name similar to this one:

```
features_and_models_20h32m31s
```

Inside of that folder you will find all of the train, validation, and train datasets, a folder showing graphs of how the model trained, the label the labels were encoded as, and other information as well.


## Future Use

You can explore other kinds of speech data, as well. I am collecting a list of free and available speech databases <a href="https://a-n-rose.github.io/2019/01/06/resources-publicly-available-speech-databases.html">here</a>. I offer directions for downloading a small dataset of female and male speech <a href="https://a-n-rose.github.io/2019/01/31/small-female-male-speech-data.html">here</a>. Note: in order to work with these scripts, the wavefiles need to be separated by class within the 'data' folder.
