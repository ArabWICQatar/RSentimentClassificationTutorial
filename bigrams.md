### BIGRAMS

Let us start by installing the following required packages. Go to _**Tools -&gt; Install Packages**_** **and install each of these packages one-by-one.

* tm
* tau
* qdap
* RWeka
* e1071
* wordcloud

Let us now load all of these packages at one go!

##### Code Block 1

```
#create a vector of all the packages you want to load
packs <- c("tm","tau","qdap","RWeka")
lapply(packs, require, character.only = TRUE)
```

_The lapply function is very useful. Why not read about it by typing&gt; ?lapply_

**Code Block 2**

```
#load the dataset as a matrix
inputText = read.csv(file = "pathToFile/AirlineTweets.csv", header = TRUE, sep = ",")
input=as.matrix(inputText)
```

Before we move onto the next step, let us look at the data.

`> head(input)`

We can see that the data is made up of _**two columns - Tweets and Sentiment Class.**_

The tweets start by @AirlineName and is then followed by the rest of the tweet.

### 

### Data Pre-processing

Let us start by pre-processing the data to remove stop-words, punctuation, numbers, links, spaces and of course the @AirlineName.

##### Code Block 3

```
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
```

The  “tm" package works with a data structure called Corpus. We will first convert our pre-processed data some\_txt into a corpus. _**To know more about Corpus, type&gt; ?corpus.**_

### Feature Extraction - Bigrams

##### Code Block 4

```
#convert some_txt into a corpus and remove stopwords and punctuations
corp=Corpus(VectorSource(some_txt))
as.VCorpus(corp)
corp=tm_map(corp, removeWords, stopwords('english'))
inspect(corp)corp <- tm_map(corp, removePunctuation) 
inspect(corp) 

#create the bigrams and Term document matrix
BigramTokenizer <- function(y) NGramTokenizer(y, Weka_control(min = 2, max = 2))
tdm <- TermDocumentMatrix(corp, control = list(tokenize = BigramTokenizer))
m= inspect(tdm)
```

_We have now created the Term Document Matrix tdm using the bigrams as terms._

Let us now look at the frequently used bigrams in our tweets. Type the following,

`> v = sort(rowSums(m), decreasing = TRUE)`

`> v`

Was that list too long? Why not create a simple wordcloud?

##### Code Block 5

```
library(wordcloud)
set.seed(1234)
#you can change the frequency of the terms to a number of your choice
wordcloud(names(v), v, min.freq = 10)
```

_**You should be able to see this word cloud.**_

![](https://lh5.googleusercontent.com/ZiquFXGy648vm2t6PeCg3cg-fk22rDEVueK3lUsQQLXjmc9V-T5cp3-k4lP4-Ex4_G31imEn227_kmgkDg_wn8r7kvePXAMQj-MbQNFUsj0S8IOho_yaxe2JmA7-FXHg0MupuLE "Rplot01.png")

_**We can see that some of the words that will influence the classification are late flight, cancelled flight, great customer, flight delayed etc.**_

```
OPTIONAL: Did not like the colours in the plot? Let’s make it colorful!
> par(bg = "black")
> wordcloud(names(v), v, colors = c("tomato","wheat", "lightblue"), scale = c(6, 0.5), 
random.color = TRUE, rot.per = 0.5, min.freq = 10, font = 2, family = "serif")
```

### 

### Classification of the Bigram features

Let us now create a data frame DF, and split it into training and test sets. To these sets, let’s apply SVM.

##### **Code Block 6**

```
#create a dataframe to hold our data
DF <- as.data.frame(m, stringsAsFactors = FALSE)
nrow(DF)
DF=as.matrix(DF)
tdf=as.data.frame(t(DF))
tdf=cbind(tdf,input[,2])
len=ncol(tdf)
header=c(1:(len-1))
header=c(header,"Class")

#create svm model with train and test sets
colnames(tdf)=header
trainset <- tdf[1:1800,]
testset <- tdf[1801:2000,]
svm.model <- svm(Class ~ ., data = trainset, cost = 100, gamma = 1)
svm.pred <- predict(svm.model, testset[,-len])
pred <- factor(svm.pred)
xtab <- table(pred, testset[,len])
confusionMatrix(xtab)
```

_**Check the confusion matrix. Are you getting an accuracy of ~65%? Not happy?**_

Why not try unigrams now?

