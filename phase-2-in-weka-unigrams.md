# Phase 2 in Weka

Let’s now move to Weka for classification, but let us first get the unigrams from R.

_**Create a new script from File -&gt; New Script, and save it as Unigrams.**_

Copy paste the code section into Unigrams.R It is similar to Bigrams.R.

##### 

##### Code Block: Unigrams.R

```
#create a vector of all the packages you want to load
packs <- c("tm","tau","qdap","RWeka", "wordcloud")
lapply(packs, require, character.only = TRUE)

#load the dataset as a matrix
inputText = read.csv(file = "pathToFile/AirlineTweets.csv", header = TRUE, sep = ",")
input=as.matrix(inputText)

# remove retweet entities
some_txt = gsub("(RT|via)((?:\\b\\W*@\\w+)+)", "", inputText[,1])

# remove at people e.g. @ArabWic
some_txt = gsub("@\\w+", "", some_txt)

# remove punctuation
some_txt = gsub("[[:punct:]]", "", some_txt)

# remove numbers
some_txt = gsub("[[:digit:]]", "", some_txt)

# remove html links
some_txt = gsub("http\\w+", "", some_txt)

# remove unnecessary spaces
some_txt = gsub("[ \t]{2,}", "", some_txt)
some_txt = gsub("^\\s+|\\s+$", "", some_txt)

#convert some_txt into a corpus and remove stopwords and punctuations
corp=Corpus(VectorSource(some_txt))
as.VCorpus(corp)
corp=tm_map(corp, removeWords, stopwords('english'))
corp <- tm_map(corp, removePunctuation)

#create the unigrams and Term document matrix and a wordcloud
UnigramTokenizer <- function(y) NGramTokenizer(y, Weka_control(min = 1, max = 1))
tdm <- TermDocumentMatrix(corp, control = list(tokenize = UnigramTokenizer))
m= inspect(tdm)

library(wordcloud)
set.seed(1234)
v = sort(rowSums(m), decreasing = TRUE)
#you can change the frequency of the terms to a number of your choice.
wordcloud(names(v), v, min.freq = 10)

#prepare to write the csv file 
DF <- as.data.frame(m, stringsAsFactors = FALSE)
nrow(DF)
DF=as.matrix(DF)
tdf=as.data.frame(t(DF))
tdf=cbind(tdf,input[,2])
len=ncol(tdf)
header=c(1:(len-1))
header=c(header,"Class")
colnames(tdf)=header
write.csv(tdf, file = "pathToFile/Unigram.csv",row.names=FALSE)
```

_**Make sure to change the path to the file.**_

_**Say bye to R, and hello to Weka! :\)**_

```
FUN: Worried you have Alzheimer’s? Take this test to find out.
> alzheimer_test(char1 = c("9", "O", "M", "I", "F","D"), 
char2 = c("6", "C", "N", "T", "E", "O"), nr = 5, nc = 10, seed = NULL)
```

### Applying Filters

Let us start by opening Weka! You will get the following screen.

![](https://lh5.googleusercontent.com/icg2Jc7xXFaXxZoMGMOROr-ykyZvsHH1-8ldEtwOzJLVj8xnK7MEkl7zv113q8uCnI3dtnhQk0gUcFk0dSY3WKYJCvUlDNZHIQA88tZZj_A2OOtt5VLaBm4Cpf2iYKr_tpoPJmY "Screenshot 2017-01-23 15.41.24.png")

_**Click on the explorer tab.**_

_You will see the following screen._

![](https://lh5.googleusercontent.com/M_4SdExaNdPRtp0NAuttJq3MuS7daRmWwd91EqRAH9KnMdb61EbVd645VjNZlQAVGnzeP7UswnfsKcTiqGjGEpN4GuqO4upSi2dcIDxp4-Ze90dHMhVJwJNGuCxIhJuoRU3UgZ0 "Screenshot 2017-01-23 15.43.44.png")

1. Click on the \_**“Open File” **\_button. This will open a small window.

2. Browse to the folder where the _**Unigram.csv**_ file is located.

3. Select CSV as the option in the\_** “Files Of Type” **\_dropdown list box \(shown below\).![](https://lh6.googleusercontent.com/hCAE-8mYqbcb8VM-lzWup6ev94uRMf-kgM8MiyQnQ6EAnOddNGRLKRdn0578tNQDup5wp59tLnu2RiS5T2svY9BvdRWjZMG40QXkdkMPJjezPTAk1T8sD3MaXvGs30_w8f9Mg1w "Screenshot 2017-01-23 15.44.08.png")

4. Wait for the file to load. Once loaded you will see all of the attributes under the \_**“Attributes” **\_area \(shown below\).![](https://lh5.googleusercontent.com/aEq-iR62MD8cZK_zycg5rsQl7dHoesj1PcKu-JfmahwiaWVFnHrJ0BPCC759jdrUtpard3TtgjqgjLFV-1VnhO71x9H1N4zOV6_rDVUL37FRxHpTIWacb3lOPNyhjDQ5zVpGNjQ "Screenshot 2017-01-23 15.53.27.png")

5. Click on attribute 1. You can see the minimum/maximum value along with other details under _**“Selected Attribute”**_. You can see that the type is _“numeric”._

6. Let us now convert the class variable to Nominal. Click on _**Choose -&gt; filters -&gt; unsupervised -&gt; attributes \(scroll down\) -&gt; StringToNominal **_\(shown below\).![](https://lh3.googleusercontent.com/xeORfe8gD99si0RScLq-9XDOqFxHskxUgoof7q3pNbj1OiW4In80b-GrlhS62n_p4i6ewZ86ofFQipO6TY2t3XQJN7HEiyTOhMdixEDTjiC4FOgg8Wm6JWL4-ns7ySmn18Iibbk "Screenshot 2017-01-23 15.49.52.png")

_We can stick with the default settings, as the filter is applied to the last column. You can now select the last attribute from the list of attributes. The type of it will be“nominal”._

### 

### Classification in Weka

You can run various classifiers from Weka.

1. To start, click on _**“Classify”**_ tab.

2. Choose any classifier you want from the list that opens, when you click on the _**“Choose”**_ button. Leave it at the default for the first time.

3. You can choose between _Cross-validation and Percentage split_. Leave it at the default for the first time.

4. Click on _**“Start”**_ to run the classifier.

![](https://lh4.googleusercontent.com/FJZ_XwM1Pi3EIKrkCuPe3xJnjMT_wfStuE42ntRk5aKCFXy_yIWINc4ge-UXymSoSUv9RL2xaiLNpaHcVPYBvAcyADTF8wxMJ3WkilEqBCChb7aQiiNXzNSEC5Fc5pWsuK0Hw2g "Screenshot 2017-01-23 16.06.22.png")

_This will run the ZeroR classifier by default. Why not choose other classifiers?_

You will find _**bayes-&gt;NaiveBayes, function -&gt; SVM, lazy -&gt; IbK \(KNN\)**_ and a whole lot of other classifiers, when you click on the choose button. We will use the J48 tree classifier in the next steps.

_We have been using the cross-validation techniques for so long. Let us move to % split next._

Let us now split our data, 90% into the train set and 10% into the test set.

Let us try this technique.

1. Click on _**Percentage Split  and set it to 90%.**_

2. Click on _**More Options button **_\(just below it\).

3. In the pop-up window, check the option_** Preserve Order for % split.**_

![](https://lh6.googleusercontent.com/4iOBU73azGu_m_u7Vn3Ck7Amgtts9XO4XZOT3JPDLAuxzB6EM4jlVCesA7DoMDnUp3eOWdQUmFFd4Qp182RS9fd9Hs0ZvXd27ezpXljWRSNJJbhhRy_KWGWQGIx0EMzxGGs_NK8 "Screenshot 2017-01-23 16.15.14.png")

1. Choose the J48 classifier fromChoose -&gt; trees -&gt; J48.

2. Startthe classifier.

Congratulations! Your model just achieved an accuracy of ~85%!!

### Visualize the Tree

1. Click on **J48** under the _Result List column and right-click it_.

2. Click on _Visualize tree._

![](https://lh3.googleusercontent.com/NBSgxRogv0CRgzsfMCziRy19kxsU7lMRN2jQrXD5OHBqLCkXJbGJaE3_nhR_GyThpHYHvq1IPnGFpRe6uZkmPJJLZw4AIHJYzpbdzofV4zVAwRuaJ36vrHMqRNauR9m_PVglhRo "Screenshot 2017-01-23 16.26.43.png")

1. In the pop-up window that appears, you can see an extremely cluttered tree.

2. Right-click anywhere on the window and select Auto-Scale, Fit-to-Screen OR Center on top node.

3. You can now view the tree \(similar to the one below\).

![](https://lh5.googleusercontent.com/XNUaE2-WIOtoLiHvgqjqYSHpjBfZUR2Wj7ruy_8zedEDkyDRE3F0KtTkmx7ZT1pdq8VYNwVgP3yeJwiYLQFljeM0mtAlsMDFLd2x1yUJ7nFnLIiNleJzUj6qTOHHWPK-ktEVHMg "Screenshot 2017-01-23 16.31.46.png")

