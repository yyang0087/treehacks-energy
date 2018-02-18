# treehacks-energy Challenge
Submission for TreeHacks 2018 - Stem's Challenge.

## [Challenge](https://github.com/stemtreehacks/stem_treehacks_2018)
To forecast one site's energy consumption and simulate the activity of a behind-the-meter energy storage system in order to reduce this client's energy bill through peak shaving.

## Getting Started
The analysis and prediction model (as well as the dataset provided) can be found in this repo. To run, simply modify the path of the file in:
```
analysis.py and seeding_LSTM.py
```
Running the code will yield the results shown below. Alternatively, you can reproduce or enhance the plots:
```
Using: data_points.p
pickle.dump([trainPredict, trainY, testY, testPredict], open(dir+'data_points.p', 'wb'))
```
## Our Solution
Using long term short term memory layer (LTSM),  we are able to learn sequence patterns better by having memory of what it has seen before.

![Learning](https://github.com/yyang0087/treehacks-energy/blob/master/1.png)

As the train decreases over epoch, it's evident that the model is learning.
```
Train Score: 44.57 RMSE
Test Score: 46.17 RMSE
```
Since train and test scores are close, the model can correctly predict on data it hasn't seen yet.

### Main Plot
Here, is comparison of our known data (in blue), our training output (in orange), and our test data (in green).
![Main Plot](https://github.com/yyang0087/treehacks-energy/blob/master/3.png)

One issue that's evident in this plot is that our algorithm consistently underestimates the values. But since the understimation is consistent across time, we can design a correction factor to compensate for the offset.

![Correction Factor](https://github.com/yyang0087/treehacks-energy/blob/master/2.png)
This plot shows what a simple error correction would look like. Notice how the red lines (magnitude of peaks predictions) match the the actual data much more accurately now.

![Zoomed Prediction](https://github.com/yyang0087/treehacks-energy/blob/master/4.png)
It's evident and remarkable when zoomed in that the shape closely matches the actual data. The only issue is the biasing issue, which is why we have a correction factor. This essentially shows the the model can learn qualitative geometric features of the usage by training on past pulses. 

### Code source:
- Tensorflow
- Keras

## Acknowledgements
- Built for TreeHacks 2018
- Made by Nathan Zhao, Yu-Lin Yang, and David Ta
