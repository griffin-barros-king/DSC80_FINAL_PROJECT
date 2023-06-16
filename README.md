Problem Identification:
The prediction problem I am looking at is predicting the duration of a power outage based on certain factors of where and why the outage happened. I used a classification model setting three potential classifications for the duration of an outage. 'short' for less than 8 hours. 'medium' for more than 8 hours and less than 64 hours. and 'long' for more than 72 hours. I chose these sections as short would imply it wouldn't affect an entire waking day. It would also have the chance to not completely affect a work day. Medium would definitely affect workplaces and other areas, but would not be a huge that would pose serious risk to human life or food supplies. long being longer than 3 days gets into the area where the outage could have serious safety and economic implications. This is of course a multiclass classification system.

I decided to use accuracy for the project as it would be important to get this absolutely right every time. If we incorrectly predicted short when it was long, there would not be enough preparations and could cause greater issues. If it were to be the opposite, however, or even if we predicted medium in that case. there might be some misguidance of resources and supply issues that would be cause artificially because of the prediction. I also feel that accuracy is more valuable when looking at multiclass classifications.


Baseline Model:
my baseline model takes into consideration the population of the place where the outage occured, the percent of the population that was urban, and the cause of the power outage. The first two are quantitative and the last is nominal.  For the baseline I left the Quantitative alone and I one-hot-encoded the causes of the power outages. I used a KNeighbors classifier with the default 5 neighbors. the training accuracy was 49.32% whichis not great, but at least not too high to imply overfitting, but the testing accuracy was a mear 48.51%. This poor testing accuracy implies that the model would not be very useful in the case of an emergency. It is basically the same as guessing blindly. I believe part of this is due to the raw population data begin used. and also the kneighbors classifier not looking deep enough.


Final Model:
One of the features I added was a StdScaler transform on the population. I did this as I felt it would give a more accurate value describing the size of the city in comparison to others that experience and outage. another feature I added was a arcsin transform of the population percentage. I did this as arcsin transformations are known to be good at drawing meaning from percentages. my training and testing accuracy shot up significantly, being 64.95% and 64.77% respectively. I believe this is due to the logical decisions in feature derivation, along with the switch to a decision tree and the use of hyperparameter analysis.

to visualize the difference models and their accuracies here are the confusion matrices for both models:
![A confusion matrix for my baseline model. if this fails, but you still want to look at the images, the repository is public and the images are visible their](https://github.com/griffin-barros-king/DSC80_FINAL_PROJECT/blob/main/Baselin_Model_Conf_Matrix.png) ![A confusion matrix for my Final model](https://github.com/griffin-barros-king/DSC80_FINAL_PROJECT/blob/main/Final_Model_Conf_Matrix.png)

Fairness Analysis:
My choices for group X and Y were the first and second half of the year for when the outage occured. I evaluated them on accuracy. My null hypothesis is that my model is fair and that it would have the same accuracy regardless of when the outage occured. My alternative hypothesis was that it would be more accurate in the the first half of the year. My test statistic was simply whether or not the accuracy for the first half of the year was greater than the second half of the year's accuracy.
the resulting p value was 0.497. My conclusion is that I fail to reject the null hypothesis. According to my test I conclude that my model is fair.


