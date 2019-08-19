# Does basic house information reflect house's description?

In this project we will perform a clustering analysis of house announcements in Rome from Immobiliare.it.

![alt text](https://directionscu.org/wp-content/uploads/2018/08/cashforhome.png "Logo Title Text 1")
____ 

### Goal
Implementation of two clustering methods and compare the results we get. We will need to create two datasets and each of them will be filled by data scraped by the website Immobiliare.it.

### Scraping
The website that we perform the scraping on is: [here](https://www.immobiliare.it). In particular, we retrieve more than 10k announcements starting from this [link](https://www.immobiliare.it/vendita-case/roma/?criterio=rilevanza&pag=1).
For the scraping part, [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) library is used to parse the `html`.

### Datasets 
#### 1) Information
The first matrix will have this format: <img src="https://latex.codecogs.com/gif.latex?$m_{ij}&space;=&space;value$" title="$m_{ij} = value$" /> where <img src="https://latex.codecogs.com/gif.latex?$i&space;\in&space;\{announcement_1,&space;...,&space;announcement_n\}$" title="$i \in \{announcement_1, ..., announcement_n\}$" /> and <img src="https://latex.codecogs.com/gif.latex?$j&space;\in&space;\{price,&space;locali,&space;superficie,&space;bagni,&space;piano&space;\}$" title="$j \in \{price, locali, superficie, bagni, piano \}$" />. *n* is the number of the announcements. It's possible that not all the announcements will have all the fields mentioned above, if it's the case we don't take it into account. 

#### 2) Description
The second matrix will have this format: <img src="https://latex.codecogs.com/gif.latex?$m_{ij}&space;=&space;tfIdf_{ij}$" title="$m_{ij} = tfIdf_{ij}$" /> where <img src="https://latex.codecogs.com/gif.latex?$i&space;\in&space;\{announcement_1,&space;...,&space;announcement_n\}$" title="$i \in \{announcement_1, ..., announcement_n\}$" /> and <img src="https://latex.codecogs.com/gif.latex?$j&space;\in&space;\{word_1,&space;...,word_m\}$" title="$j \in \{word_1, ...,word_m\}$" />. *n* is the number of the announcements and *m* is the cardinality of the vocabulary. WE implement the ***Tf-Idf*** by skratch (no help of libraries).

### Clustering
This step consists in clustering the house announcements using K-means++. In order to do that [sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) Python library is used. The optimal number of clusters is chosen with the [**Elbow-Method**](https://en.wikipedia.org/wiki/Elbow_method_(clustering)).

### Comparison among cluster
We expect that both datasets will lead to similar clusters. So we analyzed the results.
#### Find similar clusters
To check this, we use the ***Jaccard-Similarity*** to measure the similarity betweeen the two outputs (information clusters vs description clusters). And the 3-most similar couples of clusters are returned.
#### Word cloud of house descriptions
With this last output we also create [wordcloud](https://www.datacamp.com/community/tutorials/wordcloud-python) for each couple of clusters. The words that will be represented are those extracted from the description of the houses that are in the relative couple.


____ 

## The Files

**Final Notebook.ipynb**:

The Jupyter notebook which contains the key steps of our work and where we explain each decision we have made analyzing them. It shows our outcomes and our results with comments.

**scraping.py**:

Module which contains the functions that scrape the information from the website www.immobiliare.it. Informations are stored into a csv file with path 'data/raw_data.csv'.

**preprocessing.py**

Module which contains the functions used to preprocess the raw data. The preprocessed dataframe will be stored into the csv file under the path 'data/data_preprocessed.csv'.

**matrix_generator.py**

Module which has the functions used to compute the two matrixes.

**k_means.py**

This set of functions are responsable to compute the clustering part using the kmeans++ algorithm with sklearn library.

**Word_cloud_lib.py**

Package of functions used for the Jaccard Similarity and for rendering the wordcloud frames.

