# Create a Decision Tree

Now that we have explored the IRIS dataset, let us create a decision tree.

##### We will go through this script line-by-line. Type each line in the R console as you encounter it.

* **Step 1: Load the party package.**  
  &gt; library\(party\)  
  _ You will see the ‘party’ package and a list of dependent packages loading._

* **Step 2: Let us now load the IRIS dataset that is available in R.**  
  &gt; data\(iris\)  
  _ You will see the IRIS dataset is loaded in the Environment and Workspace area._

* **Step 3: Let us create the input data frame and assign the IRIS dataset to it.**  
  `> input = iris`  
  You will see the input dataframe is loaded in the Environment and Workspace area.  The following command will give you the data structure of the variable.  
  `class(input)`  
  `[1] “data.frame”`

* **Step 4: Create the decision tree.**  
  `> output.tree <- ctree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data=iris)`  
  _** The decision tree model is now created.**_  
  Here, Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width tells R that    Species \(the class of the flowers\) is dependent on the attributes Sepal.Length,  Sepal.Width, Petal.Length and Petal.Width.

* **Step 5: Plot the tree**  
  `> plot(output.tree,type="simple")`  
  _You should be able to see the following plot in the “Files and Plots” area of the IDE._

![](https://lh4.googleusercontent.com/Wxq3juWLCn5Swg4p34Tchr0HkEIxqfTBvtexWjAd-y8FCoO0GUjUo00Qhw2RV1hmUEGOy5v7l3NhcZTJ4ukGW5bCiZUoUw80OGb20AwJpOd4ENdedSDuO9Ljk9l6_yO3u22SEgg "Rplot.png")

* `> print(output.tree)`
   This will give you the following verbose output of the tree.

![](https://docs.google.com/drawings/d/sCfSrNc_JtuTy3MSEBnTYNg/image?w=465&h=173&rev=9&ac=1)

```
FUN: Want a quick random password to satisfy the annoying Sign-ups?                                                                                           
> random_password(length = 12, replace = FALSE, extended = TRUE)
```



