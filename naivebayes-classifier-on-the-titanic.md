### NAIVE BAYES CLASSIFIER

| Haven’t heard about NaiveBayes?? Choose between a [video](http://machinelearningmastery.com/naive-bayes-tutorial-for-machine-learning/) and an easy [tutorial](http://machinelearningmastery.com/naive-bayes-tutorial-for-machine-learning/) to know more. |
| :--- |


_**Create a new script and save it as NaiveBayes. \(File -&gt; New Script\)**_

The NaiveBayesTitanic.R script uses the same package and is almost similar to the IrisSvm.R script.

The Titanic dataset comes with an extra unwanted attribute called “frequency” during conversion into a data structure that is readable. We will add a piece of code to remove this attribute and will use the NaiveBayes model instead of the SVM model.

##### NaiveBayesTitanic.R

```
library(e1071)
library(caret)
data(Titanic)

#convert the Titanic dataset into a dataframe and remove the unwanted frequency attribute
input=as.data.frame(Titanic)
input=input[,-5]

#split into train and test sets
index <- 1:nrow(input)
testindex <- sample(index, trunc(length(index)/2))
testset <- input[testindex,]
trainset <- input[-testindex,]

#create the naivebayes model
nb.model <- naiveBayes(Survived ~ ., data = trainset, cost = 100, gamma = 1)
nb.pred <- predict(nb.model, testset[,-4])

#create the confusion matrix
pred <- factor(nb.pred)
xtab <- table(pred, testset[,4])
confusionMatrix(xtab)
```

_Copy paste this code in the NaiveBayes.R script. _

We can run the entire script just by clicking on the button **Source -&gt;Source with Echo.** \(No need to select any lines in the script like we did with the Run button! \)

```
FUN: You deserve a break!! See the Towers of Hanoi in motion. (Make sure the "PLOTS" TAB IS ENABLED)
> tower_of_hanoi(n = 4)
```



