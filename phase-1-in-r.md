# Phase 1 in R

In this phase we will use the simple and popular IRIS dataset in R. We will run a Decision Tree and SVM classifier on this dataset which is available in R.

### IRIS Dataset

This dataset has the Petal and Sepal, length and width as features for three different types of flowers: Versicolor, Setosa and Virginica.

* We will first examine the dataset in R. For more details about the dataset, type the following command.  
  `> ?iris`  
  _Output will be shown in the Plots and Files area._  
  Read the file to know more about the IRIS dataset.

* We will now load the dataset, using the next command.  
  `> data(“iris”)`  
  _You can see that the dataset iris is loaded in the Environment and Workspace area._

* Let us now check the size of the dataset - number of rows and columns.
  `> nrow(iris)   [1] 150   > ncol(iris)   [1] 5`

* Let us now see the first few rows of the dataset, to understand the structure of the dataset. We can see that the dataset is made up of 5 features, namely,Sepal.Length, Sepal.Width, Petal.Length, Petal.Width and Species.
  `> head(iris)`

Sepal.Length \| Sepal.Width\| Petal.Length\| Petal.Width\| Species

-------------------\|----------------------\|---------------------\|-------------------\|--------------

5.1 \|3.5\| 1.4 \|0.2 \|setosa

4.9\| 3.0 \|1.4\| 0.2 \|setosa

4.7 \|3.2\| 1.3\| 0.2\| setosa

4.6\| 3.1\| 1.5\| 0.2\| setosa

5.0 \|3.6\| 1.4\| 0.2 \|setosa

* Let us get a summary of all the features \(each column\) in the dataset. This gives us details like minimum,median, maximum values etc. of the features. We can also see there are 50 observations of each flower under the Species tab.  
  `> summary(iris)`  
  _Output will be shown in the Console._

* Now, that we have a general idea of the dataset, let us view the entire dataset.  
  `> View(iris)`  
  _Output will be shown in the Code Editor._

_**Your IDE should like the following image, once you are done with all of the commands.**_

![](https://lh6.googleusercontent.com/ax7jYtKc9mQUzjzF-GKYdzfamXiijmZNjgd2fKXqOhxaG9gicgoAl857tNfRept9pa8E0EvzHjiTctgk4GXK-KzZSUpJa-gUP6FjNayNrcp1M17JqhxXZmnPu_kCNkjhbaOTFUA "Screenshot 2017-01-17 01.07.56.png")

#### 

#### Install a package

Let us now install the package\_** “party” **\_for creating a decision tree.

1. In the Menu bar, click on _**Tools -&gt; Install Packages.**_

2. In the dialog box that appears, type _**party**_ in the packages text box. This will install the required package along with the dependencies.

3. Repeat to install package _**“fun”**_.

4. Load the package _**fun**_ by typing the following command:

`>library(fun)`

![](https://lh4.googleusercontent.com/zF_HT7Lg_grNEm5fTpu022iTGC4MVcEaAL2OyrkO_bcG3Is2zPQiUhnDT0XdDJkkRUde3ivRVZ3dd2CZssy5SNTQ6Rrk7Ew2CHQ7Na8XgRd1BNcnw77KKpG0x02vnnA62DhPOnQ "Screenshot 2017-01-17 00.59.45.png")

_**You are now ready to take off!!**_

