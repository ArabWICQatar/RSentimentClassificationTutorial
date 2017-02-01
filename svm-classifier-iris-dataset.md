#### Create a new script

Let us start by creating a new script. 

In the Menu bar, click on _**File -&gt; New Script.**_

Press _Ctrl+S or on the floppy disk icon_ to save the script. Enter_** IrisSvm**_ as the script name. \(DO NOT ADD .R EXTENSION\)

  


### SVM Classifier

| Don’t know SVM?? Here is a quick read [tutorial](http://www.svms.org/tutorials/Berwick2003.pdf), and an easier to follow [video](https://www.youtube.com/watch?v=1NxnPkZM9bc). |
| :--- |




##### We will run the scripts in this part of the tutorial as chunks of code. As you encounter a code block, paste it into the script.

  
Let us start by_ installing _all of the required packages.

Click on _**Tools -&gt; Packages**_ and install each of these packages one-by-one.

1. e1071

2. caret



Let us start by _loading_ all of the required packages and data.

##### Code Block 1

```
library(e1071)
library(caret)
data("iris")
input=iris;
```

Paste the code block in the_ IrisSvm.R_ script area. Select the lines that you just pasted and click on the Run button. \(Refer to below image\).

  
_**You should now be able to see the iris dataset and the input variable in the Workspace.**_

![](https://lh3.googleusercontent.com/SMSnOk9giMHd9zq2DV2O2gXiJP6KLf6Vs1zaQ-57Bcp7ZlKtM6xIxCT7odVU-zJ3TUtQXWs7c2rsJyHfS3cX93pESl-Mh1g4JXCxd3P2JVOA6Fg65w-SelMsM6dsD03ZuvLUvS0 "Screenshot 2017-01-23 02.04.48.png")

  


##### Code Block 2

```
# split the dataset by half into train and test set
index <- 1:nrow(input)
testindex <- sample(index, trunc(length(index)/2))
testset <- input[testindex,]
trainset <- input[-testindex,]
```

_Copy-paste this code block below the last code block. Select the newly pasted lines and run the code. \(Refer to below image\)_



* You can check the size of the train and test set by using nrow\(\).
  `> nrow(trainset)`
  `[1] 75`
  `> nrow(testset)`
  `[1] 75`



_**You can see that the data is split exactly in half! :\)**_

![](https://lh5.googleusercontent.com/-9Mu7EUZ3U66pE8cHxAgINpFYdhb8nyyWjavuYTId55SBgBVxmYxcYIBSHcXQX6B6Ui4fgGpD7CodegrVkBOPDAi8e3cwLKAOf-Oi_SUO7EYJZ29TM7M0kVUR1-x3RsRKuVpF4g "Screenshot 2017-01-23 02.10.19.png")



##### Code Block 3

```
# create the SVM model
svm.model <- svm(Species ~ ., data = trainset)
svm.pred <- predict(svm.model, testset[,-5])
```

Copy-paste this code block below the last code block. Select the newly pasted lines and run the code. \(Just like last time.\)

The svm.modelis a model variable that is built on the trainset for classifying the Species \(class attribute\) using all of the other attributes in the IRIS dataset.

We will now use thesvm. modelto predict the values in the testset. We are ofcourse removing “Species” \(class attribute\) which is the 5th column in the testset.



##### Code Block 4

```
#create the confusion matrix
pred <- factor(svm.pred)
xtab <- table(pred, testset[,5])
confusionMatrix(xtab)
```

Copy-paste … er … \(You know the drill!.\)

_**You should now be able to see the confusion matrix like the one below.**_

  
![](https://docs.google.com/drawings/d/s803wyVIVaLO2yhkS0KzjIw/image?w=516&h=386&rev=9&ac=1)

  
_**You can see, we have achieved an accuracy of 93.33% using the SVM classifier.**_



##### Code Block 5

```
#visualize the model
plot(svm.model, iris, Petal.Width ~ Petal.Length)
```

_You should now be able to see the plot under “Plots and Files”._



```
OPTIONAL: Did not like the colours in the plot? Why not try the Terrain colours to add some zing?
#visualize the model
plot(svm.model, iris, Petal.Width ~ Petal.Length, symbolPalette = rainbow(4),color.palette = terrain.colors)
```

 We have now finished exploring the IRIS dataset in detail!

  


