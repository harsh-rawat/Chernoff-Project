# Chernoff-Face-Project
This is the final project of CS 533 (Image Processing) at UW Madison. The project involves manipulating real world images to change the emotions of the subject. Additionally in Part II of the project, we perform sentiment analysis on live twitter data and then display the sentiment as a Chernoff face.

A Chernoff face is a simple sketch of a human face that is parameterized by a few variables. By manipulating the variables, it is possible to achieve a wide range of expressions.
The aim of this project is to simulate Chernoff Faces on real world images. We can manipulate the variables to change the expresions of the subject and simulate anger, surprise, sadness and happiness.

Part I of the project involves creating a simple Chernoff Face on the real world image.
Part II of the project involves extracting the real time tweets from twitter based on a hashtag and then classify the tweet's emotion using a Markov classifier. We then display the emotion using a Chernoff face on the real time image.

In part I of the project, we have used spatial mapping function BSplineFunction to shift the data-points of the image. We find the bounding rectangle of the feature and then shift the datapoints of the entire rectangle grid using spatial mapping function. For some features, where we require curvature, we use gradient to shift different data points at a different distance.

In part II of the project, the algorithm used is -

Preprocessing step : Train a classifier on the twitter sentiment data taken from Kaggle dataset (https://www.kaggle.com/c/sa-emotions/data).
1. Get the data from Twitter for the provided hashtag.
2. Clean the data - Specifically, we clean the special characters and digits. Additionally, we remove some redundant portions of the tweet text which do not contribute to the emotion.
3. We classify the cleaned text using our pre-trained classifier to find the probabilities of each emotion.
4. We perform thresholding on the derived probabilities and then we perform weighted scaling of the probabilities. This allows us to retain the dominant emotions of the text while discarding or scaling-down of passive emotions.
5. Based on the probabilities derived in above step, we generate the parameters for each feature which we need to manipulate. There is a correlation between features and different emotions. Such as for Eyebrows - Happy : Move Eyebrows upward, Surprise : Move Eyebrows upward, Sadness : Rotate anti-clockwise, Angry : Rotate clockwise. 
Example of setting parameter value for a text is : Probabilities <Sad : 0.2, Surprise : 0.8> <We move eyebrows upward to 0.8 times of max value of surprise and rotate 0.2 times of max sadness>. This is done for each feature.
6. Based on the parameters calculated above, we derive the grid positions to move and then we utilize the function we wrote in part I for generating the Chernoff face.
