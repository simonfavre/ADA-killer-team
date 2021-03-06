# How do reviews shape our experience on amazon ?

[This document has been reviewed following the first milestone. Last edited 17/12/2017]

> This project gave birth to a data story that can be found on [data-analytics.science/](http://data-analytics.science/). This website doesn't aim at explaining all details that came in the making of the project but rather to allow a non expert reader to understand the results and the different steps that were considered to come to such.

# Abstract
How do reviews shape the experience of users on Amazon? As users of this platform we have experienced ourselves how highly influenced we can be when it comes to reviews. This is mostly a consequence of the amount and diversity of products offered by the plateform. We therefore wondered many things concerning those reviews. 

As a general question we wanted to study the [Herding Effect](https://en.wikipedia.org/wiki/Herd_behavior) on reviews : that is how are reviewers influenced by past reviews. To achieve such goal, we decided to first study the effects of reviews on multiple parameters but mostly on the sales Rank of the object to see in what measure are users influenced by reviews (Indeed so far this study was done mostly on the dataset for which the herding effect was studied : similar books). Then we decided to study one category of object in particular : books. Those are the most reliable when it comes to finding similar objects. Indeed multiple products can be identified as similar when the text is the same but only the format changes (e.g. ebooks, different editions, ...). Identifiying similar books is the most challenging part of this project as the large dataset isn't easy to work with. Finaly we dive deep in the study of the Herding effect, trying to identify how the first review of a book can influence the following reviews.


All this work has as goal to emphasize to amazon customers that reviews are not the only way to asses a product and that they should always look for third parties reviews.

For our study, we use the dataset “Amazon review data”. We focus on categories of data that offer good possibilities to find similar products. We will therefore work on Books already at the center of many research, for example [here](https://www.stat.berkeley.edu/~aldous/Research/Ugrad/Timothy.Thesis.pdf)), and should we have enough time Electronics, Movies & TV and finally CDs.

We would like to emphasize to a potential reader that we have for now decided to focus on 5-core datas. Those are the products and customers that have at least 5 reviews. This allow us to first only consider a subset of the data but also to make sure that we have at least 5 reviews per product to later study the herding effect (which by itself is already not much). In further work we want to extend the amount of data that we consider to be able to observe quantitative results).


# Research questions
1. _Characteristics of reviews:_
	* Task a : How do reviews correlate to price : does cheaper means more buyers and hence more reviews, does more expensive means better products ?
	* Task b : How do reviews correlate to sales rank : (depending on the category of objects and the price range)

2. _How do reviews influence customers_: 
 	* Task a : Identify a category of product that could be used to find similar objects.
	* Task b : Get similar products (e.g. books that only differ by their format or edition)
	* Task b : Herding Effect - How does the first couple of reviews of a product influence the following reviews ?

3. _Draft for the report_ : We plan here to make a website to clearly display the result of our data analysis. Nevertheless because we aren't sure yet of what type of interesting results we will have at the end we can only make assumptions and this part will most Certainly be reshaped once we gain a bit of traction on the data exploration.
	* Task a : On the first page display the major findings about the reviews and their caracteristics (being as visual as possible)
	* Task b : We would really like to take a few products as example to extrapolate our finding on the Herding effect to be able to give a visual representation of our findings. 
	* Task c : Then we will try to explain how this happens on the entire dataset we considered.
	* Task d : Try to have a time dependent slider to show the evolution of reviews with time.

# Dataset
We decided to use first all the data available from the amazon dataset. Then because we lacked some important details we decided to extend this data with amazon API using the ASINs of products that have already been selected as similars (to reduce the number of API requests that are being done)

# A list of internal milestones up until project milestone 2

<p align="center">
  <img src="ada-milestones.png" width="750"/>
</p>

# Running
Running the notebooks will highlight which import must be perform and display in the body of the ```Import Error``` how those can be installed (using ```pip``` when possible). 

Also because a lot of tasks (specially the one that required to go over the full JSON) were very long and the results were serialized when it was possible to avoid computationally heavy piece of code. Because those files were too heavy with the dataset to be included in the repo, one can download them from our Google Drive [here](https://drive.google.com/open?id=1ga2bre3K30J4ziP6Adl6n8e-0kooNPV7). **Because of the significant size of the datasets we strongly advise someone that would like to reproduce our work to only download ```Project-Data/dump/```**. 

The location of this folder can be modified in the notebook by updating the constant ```DATA_FOLDER``` (by default it points toward ```"../../Project-Data/"```)

# Architecture
We decided to modularize the code as much as possible to improve readability and further refinement of the ressearch. Here you will find the description of our architecture :

* ```Final.ipynb``` : this jupyter notebook contains the synthesis of the work up to milestone 3. As opposed to ```Ressearch.ipynb``` it only highlights the key steps and findings.
* ```Ressearch.ipynb``` : this contains all the work that was done up to Milestone 2. Not all of it is up to date but we wanted to leave it in the repo as it allows anyone to see how we started to conduct our analysis.
* ```demo/```: contains the dumps of the dataset that is used in order to show how long it would take to compare each book pairwise without the use of LSH.
* ```assets/```: contains images used to support our claims in the final notebook
* ```scripts/```: contains all the files that are used in the notebook, with relevant names 	
	- ```amazon_api_interaction.py```: all the functions used to interact with the API and get the details that are not in the original dataset
	- ```data_import.py```: functions used to read the large JSON of the original dataset and import it in dataframes.
	- ```similarities.py``` : functions used to isolate similar books split in three phases (work on raw data, refining using the authors and finally how we can keep only the similar books using their normalized titles)
	- ```utils.py```: functions used mainly for details purposes (printing time, printing the details of books : titles, description, images and also to display the progress of the code)
	- ```analysis.py```: methods used to realize the herding effect analysis.
	- ```__init.py__```: used to be able to tell to python that this folder contains modules that can be imported (it is actually an empty file)
* ```analysis_data/```: contains the serialized version of the dataset that later allowed to conduct the analysis

*  ```report/```: for now it is simply the empty shell of a potential report that could be used to later synthesise our work.

# Work Repartition
Given the nature of such project we would like to mention that everyone worked on every single part but since we were asked to give distinct roles on each part of the project here is an attempt of a high level view of the work repartition:

- _Guillaume Raille_: Herding Effect analysis on the similar books
- _Simon Favre_: Correlation analysis and Data Story Website design 
- _Hugo Moreau_: Crawling of the data, Detection of similar books and correction on the correlation analysis following milestone 2

Everyone took part in the problem formulation. We then all participated in the building of the final data story, to provide meaningfull reporting of our results. All of us will also work on the presentation in order to obtain a comprehensive overview of the project.

# References
This ressearch was inspired by _"When Sheep Shop: Measuring Herding Effects in Product Ratings with Natural Experiments" by Anonymous Author(s)_ (provided by Pr. Robert West and for which a [blog article](https://dlab.epfl.ch/2017-08-30-of-sheep-and-beer/) has been created). 

We would also like to mention that the original dataset was provided by J. McAuley (as displayed [here](http://jmcauley.ucsd.edu/data/amazon/links.html)). They also used the data in the two following papers :

- R. He, J. McAuley. Modeling the visual evolution of fashion trends with one-class collaborative filtering. WWW, 2016
- J. McAuley, C. Targett, J. Shi, A. van den Hengel. Image-based recommendations on styles and substitutes. SIGIR, 2015