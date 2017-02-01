### TITANIC DATASET

  
Let us now run the _**NaiveBayes**_ classifier on the **Titanic dataset.**

All of us know about the fateful [ship that sank](http://www.history.com/topics/titanic) in the North Atlantic Ocean.



![](https://lh3.googleusercontent.com/ednEDRQsVBFg6-PSV1ruIzfMDwOeUa0Qgw8MvRQBNwUcwhaAFoaYn4Z-9sJX0auZlifuiMhHnDsfUd7Ic0zO5o2-46swoak8JYq0qlHyWW4QK-jet2vAcWaVoAz8gA2J-1z5A4I "tumblr_mm8fhitR3u1rwwvg9o1_500.gif")



Let us try to find the probability that a person \(based on Class, Sex and Age\) on the ship actually survived!!

The data is made up of the following attributes.

![](https://docs.google.com/drawings/d/slq46kgeIoEIJKfKT-1y32A/image?w=213&h=119&rev=22&ac=1)

* To know more about the dataset
  `> ?Titanic`



* View the Titanic Dataset
  `> View(Titanic)` 

* **Check if there were higher survival rates in children.** _The 3rd column is the index of the Age feature - Child or Adult, and the 4th column indicates the Survival - Yes / No._ `> apply(Titanic, c(3, 4), sum)`
                **Survived**
  **Age      No      Yes**
  **Child**    52       57
  **Adult** 1438     654

_**Well, they weren't lucky!**_



* **Check if there were higher survival rates in females.** _The 3rd column is the index of the Gender feature - Female or Male, and the 4th column indicates the Survival- Yes / No._ `> apply(Titanic, c(2, 4), sum)`
         **         Survived**
  **Sex        No       Yes**
  **Male **     1364   367
  **Female**  126     344

_**  
Clearly females were not as lucky as males.**_

  


