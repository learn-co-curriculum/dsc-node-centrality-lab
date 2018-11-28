
# Network Dynamics: Node Centrality - Lab

## Introduction
In this lab, we shall put the node centrality measures in to practice to analyze the character interactions in graph structure from the popular series of novels called ""A Song of Ice and Fire" by George R. R. Martin. The of famous HBO series "Game of Thrones" is derived from this saga. In this lab, we shall calculate different centrality measures to identify the the importance of characters as the story progresses.  


## Objectives
You will be able to:
- Understand and explain network centrality and its importance in graph analysis
- Understand and calculate Degree, Closeness, Betweenness and Eigenvector centrality measures
- Describe the use case for several centrality measures

## ASIOF (A Song of Ice and Fire) Character Interaction Graph Data

A. J. Beveridge, and J. Shan  created a network from books "A song of ice and fire" by extracting relationships between characters of the story. [The dataset is available at Github](https://github.com/mathbeveridge/asoiaf)
as an interaction network which was built as
> Parse the text and build a graph by connecting (creating an edge) two characters (nodes of the graph) whenever their names appear within 15 words. The edge weight corresponds to the number of interactions.

<img src="parse.png" width=300>

The datasets have been made available for you in the repo. You are encouraged to [visit A. J. Beveridge's blog](https://networkofthrones.wordpress.com) to see how this dataset is created, and different network analysis activities which are being performed with this dataset. The image you see below, has been created using same datasets. The blog gives you information on this and more experiments. For this lab, we shall focus more on graph analysis than visualizations.

<img src="got.png" width=800>

Let's get on with it. 

## Load necessary libraries

- Let's give you a head start by loading the libraries that you might need for this experiment. 


```python
import pandas as pd
import networkx as nx
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings('ignore')

%matplotlib inline
```

##  Load the dataset 

The dataset is available for all 5 books, with two CSV files for each book. One contains nodes data as adjacency matrix and other carries edges data as edge list, e.g. for book 1, `asoiaf-book1-edges.csv` and `asoiaf-book1-nodes.csv`. So we have 10 files in total. 

- Read edge data for all books into pandas dataframe:  book1_df .. book5_df. 

How about using a for loop to do this in one go - optional.


```python
# Load edges into dataframes

```

## Create Empty graph instances for each book


```python
# Create empty instances for each book above

```

## Create Graph
- Read the edge lists from the dataframes above into relevant graphs. 
- inspect the contents of graph to get an idea about the data structures contained within 


```python
# Read edge lists into dataframes

```

## Finding important nodes (characters) 

Let's use and compare different centralities measures we saw earlier to identify importance of nodes in this network. There is no one right way of calaculating it, every approach has a different meaning.

## Calculate Degree Centrality 
Degree centrality which is defined by degree of a node (number of neighbors) divided by a noramlizing factor n-1 where n is the number of nodes.

- __Find the neighbours of '**Catelyn-Stark**' from book 1.__


```python
# Neighbors for catelyn stark

```




    ['Arya-Stark',
     'Bran-Stark',
     'Bronn',
     'Brynden-Tully',
     'Cersei-Lannister',
     'Colemon',
     'Donnel-Waynwood',
     'Eddard-Stark',
     'Edmure-Tully',
     'Eon-Hunter',
     'Hallis-Mollen',
     'Hoster-Tully',
     'Jaime-Lannister',
     'Joffrey-Baratheon',
     'Jon-Arryn',
     'Jon-Snow',
     'Jon-Umber-(Greatjon)',
     'Luwin',
     'Lysa-Arryn',
     'Marillion',
     'Masha-Heddle',
     'Moreo-Tumitis',
     'Mya-Stone',
     'Mychel-Redfort',
     'Nestor-Royce',
     'Petyr-Baelish',
     'Rickard-Karstark',
     'Rickon-Stark',
     'Robb-Stark',
     'Robert-Arryn',
     'Robert-Baratheon',
     'Rodrik-Cassel',
     'Sansa-Stark',
     'Stevron-Frey',
     'Theon-Greyjoy',
     'Tyrion-Lannister',
     'Tytos-Blackwood',
     'Tywin-Lannister',
     'Vardis-Egen',
     'Varys',
     'Walder-Frey',
     'Wendel-Manderly',
     'Willis-Wode']



 `nx.degree_centrality(graph)` returns a dictionary where keys are the nodes and values are the corresponding degree centrality. 
 
- __Find the five most and least important characters from book 1 according to degree centrality__


```python
# Five most important characters from book 1 according to degree centrality

```




    [('Eddard-Stark', 0.3548387096774194),
     ('Robert-Baratheon', 0.2688172043010753),
     ('Tyrion-Lannister', 0.24731182795698928),
     ('Catelyn-Stark', 0.23118279569892475),
     ('Jon-Snow', 0.19892473118279572)]




```python
# Five least important characters from book 1 according to degree centrality

```




    [('Clydas', 0.005376344086021506),
     ('Arthur-Dayne', 0.005376344086021506),
     ('Arys-Oakheart', 0.005376344086021506),
     ('Mance-Rayder', 0.005376344086021506),
     ('Thoros-of-Myr', 0.005376344086021506)]



- __Plot and explain histogram from degree centrality values, calculated from book 1, and comment on the output__


```python
# Plot a histogram of degree centrality

```


![png](index_files/index_16_0.png)



```python
# Your observations here 


```

##  Weighted Degree Centrality

- Create a new centrality measure as a function, `weighted_degree_centrality(Graph)` which takes in Graph and the returns a weighted degree centrality dictionary. 

[Refer to this paper to get an insight into this approacj](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0165781)

Weighted degree is calculated by:

1) __Sum the weight of the all edges of a node__

2) __Normalize the weighted degree by the total weight of the graph i.e. sum of weighted degrees of all nodes__  

3) __Calculated weighted degree centrality for book 1 using this function__


```python
def weighted_degree_centrality(G):
    
    pass
```


```python
# Uncomment below to run


#plt.hist(list(weighted_degree_centrality(G1).values()))
#plt.show()
```


![png](index_files/index_20_0.png)


- __Get the top 10 characters from book 1, based on weighted degree centrality and compare with the results of simple degree centrality. Record your observations below__


```python
# Weighted DC

```




    [('Eddard-Stark', 0.08715720879717621),
     ('Robert-Baratheon', 0.06387455878360032),
     ('Jon-Snow', 0.05321748574531632),
     ('Tyrion-Lannister', 0.044121639967417865),
     ('Sansa-Stark', 0.03699429812652729),
     ('Bran-Stark', 0.03604398588107521),
     ('Catelyn-Stark', 0.03529731197393429),
     ('Robb-Stark', 0.03502579418951941),
     ('Daenerys-Targaryen', 0.030070594623947868),
     ('Arya-Stark', 0.02918816182459951)]




```python
# Un-weighted DC

```




    [('Eddard-Stark', 0.3548387096774194),
     ('Robert-Baratheon', 0.2688172043010753),
     ('Tyrion-Lannister', 0.24731182795698928),
     ('Catelyn-Stark', 0.23118279569892475),
     ('Jon-Snow', 0.19892473118279572),
     ('Robb-Stark', 0.18817204301075272),
     ('Sansa-Stark', 0.18817204301075272),
     ('Bran-Stark', 0.17204301075268819),
     ('Cersei-Lannister', 0.16129032258064518),
     ('Joffrey-Baratheon', 0.16129032258064518)]




```python
# Your observations here 


```

- __ Confirm that sum of weighted degree centralitity value for all nodes sum up to 1 i.e. normalization__


```python
# Uncomment to run 

#sum(list(weighted_degree_centrality(G1).values()))
```




    1.0000000000000002



## Betweenness centrality 

- __Calculate the weighted and un-weighted "Betweenness" centrality for book 2, and compare top ten characters as above__
- __Comment on the results__


```python
# Unweighted Betweenness Centrality

```




    [('Eddard-Stark', 0.2696038913836117),
     ('Robert-Baratheon', 0.21403028397371796),
     ('Tyrion-Lannister', 0.1902124972697492),
     ('Jon-Snow', 0.17158135899829566),
     ('Catelyn-Stark', 0.1513952715347627),
     ('Daenerys-Targaryen', 0.08627015537511595),
     ('Robb-Stark', 0.07298399629664767),
     ('Drogo', 0.06481224290874964),
     ('Bran-Stark', 0.05579958811784442),
     ('Sansa-Stark', 0.03714483664326785)]




```python
# Weighted Betweenness similarity 

```




    [('Robert-Baratheon', 0.23341885664466297),
     ('Eddard-Stark', 0.18703429235687297),
     ('Tyrion-Lannister', 0.15311225972516293),
     ('Robb-Stark', 0.1024018949825402),
     ('Catelyn-Stark', 0.10169012330302643),
     ('Jon-Snow', 0.09027684366394043),
     ('Jaime-Lannister', 0.07745109164464009),
     ('Rodrik-Cassel', 0.07667992877670296),
     ('Drogo', 0.06894355184677767),
     ('Jorah-Mormont', 0.0627085149665795)]




```python
# Your observations here

```

## Is there a correlation between node centrality measures?

Well, lets find out. 


- __Find the correlation between following:__
    - Weighted Degree 
    - Closeness
    - Weighted Betweenness
    - Weighted Eigenvector
- __Use book 1 for the analysis (You may choose other books as well)__
- __Calculate correlation matrix and visualize the results for all characters__
- __Comment on the results__


```python
# Create a dataframe with 4 centrality measures, for all characters

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Degree</th>
      <th>Closeness</th>
      <th>Betweenness</th>
      <th>Eigenvector</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Addam-Marbrand</th>
      <td>0.000611</td>
      <td>0.323478</td>
      <td>0.000000</td>
      <td>0.001551</td>
    </tr>
    <tr>
      <th>Aegon-I-Targaryen</th>
      <td>0.000611</td>
      <td>0.376518</td>
      <td>0.000000</td>
      <td>0.005096</td>
    </tr>
    <tr>
      <th>Aemon-Targaryen-(Maester-Aemon)</th>
      <td>0.005023</td>
      <td>0.336957</td>
      <td>0.010753</td>
      <td>0.013992</td>
    </tr>
    <tr>
      <th>Aerys-II-Targaryen</th>
      <td>0.002512</td>
      <td>0.385892</td>
      <td>0.007183</td>
      <td>0.027406</td>
    </tr>
    <tr>
      <th>Aggo</th>
      <td>0.002444</td>
      <td>0.292913</td>
      <td>0.000450</td>
      <td>0.000852</td>
    </tr>
    <tr>
      <th>Albett</th>
      <td>0.000747</td>
      <td>0.332143</td>
      <td>0.007169</td>
      <td>0.001875</td>
    </tr>
    <tr>
      <th>Alliser-Thorne</th>
      <td>0.005430</td>
      <td>0.363281</td>
      <td>0.026584</td>
      <td>0.015771</td>
    </tr>
    <tr>
      <th>Alyn</th>
      <td>0.002172</td>
      <td>0.380368</td>
      <td>0.002693</td>
      <td>0.019102</td>
    </tr>
    <tr>
      <th>Arthur-Dayne</th>
      <td>0.000272</td>
      <td>0.275964</td>
      <td>0.000000</td>
      <td>0.000071</td>
    </tr>
    <tr>
      <th>Arya-Stark</th>
      <td>0.029188</td>
      <td>0.458128</td>
      <td>0.028114</td>
      <td>0.143378</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot the measures as lines to see if they correlate

```


![png](index_files/index_33_0.png)



```python
# calculate Correlation matrix

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Degree</th>
      <th>Closeness</th>
      <th>Betweenness</th>
      <th>Eigenvector</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Degree</th>
      <td>1.000000</td>
      <td>0.713617</td>
      <td>0.857222</td>
      <td>0.922520</td>
    </tr>
    <tr>
      <th>Closeness</th>
      <td>0.713617</td>
      <td>1.000000</td>
      <td>0.675276</td>
      <td>0.697500</td>
    </tr>
    <tr>
      <th>Betweenness</th>
      <td>0.857222</td>
      <td>0.675276</td>
      <td>1.000000</td>
      <td>0.805318</td>
    </tr>
    <tr>
      <th>Eigenvector</th>
      <td>0.922520</td>
      <td>0.697500</td>
      <td>0.805318</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Your observations here 


```

## Character Evolution : Bring the the rest of series 

By Studying the change in centrality throughout the series, we can create an evolution of characters as the story progresses. 

- __Calculate the weighted degree centrality for all five books (edge lists), and save your results in a dataframe__

Hint: Fill nans with zero for values that can not be calculated  due to being extremely small


```python
# Create a character evolution dataframe based on weighted degree centrality from all books


# Fill Nans and view contents

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Addam-Marbrand</th>
      <th>Aegon-Frey-(son-of-Stevron)</th>
      <th>Aegon-I-Targaryen</th>
      <th>Aegon-Targaryen-(son-of-Rhaegar)</th>
      <th>Aegon-V-Targaryen</th>
      <th>Aemon-Targaryen-(Dragonknight)</th>
      <th>Aemon-Targaryen-(Maester-Aemon)</th>
      <th>Aenys-Frey</th>
      <th>Aeron-Greyjoy</th>
      <th>Aerys-I-Targaryen</th>
      <th>...</th>
      <th>Yellow-Dick</th>
      <th>Yezzan-zo-Qaggaz</th>
      <th>Ygritte</th>
      <th>Yohn-Royce</th>
      <th>Yoren</th>
      <th>Yorko-Terys</th>
      <th>Ysilla</th>
      <th>Yurkhaz-zo-Yunzak</th>
      <th>Zei</th>
      <th>Zollo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000611</td>
      <td>0.000000</td>
      <td>0.000611</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.005023</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00224</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.001336</td>
      <td>0.000000</td>
      <td>0.000236</td>
      <td>0.000000</td>
      <td>0.002673</td>
      <td>0.000472</td>
      <td>0.001730</td>
      <td>0.000236</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.001887</td>
      <td>0.000000</td>
      <td>0.00684</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.001711</td>
      <td>0.001062</td>
      <td>0.000649</td>
      <td>0.000177</td>
      <td>0.000000</td>
      <td>0.000177</td>
      <td>0.009083</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.007314</td>
      <td>0.000177</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000177</td>
      <td>0.000472</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.001908</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000318</td>
      <td>0.000318</td>
      <td>0.000000</td>
      <td>0.009752</td>
      <td>0.000000</td>
      <td>0.012932</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.003922</td>
      <td>0.00000</td>
      <td>0.000636</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000636</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000350</td>
      <td>0.011386</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.003591</td>
      <td>0.001139</td>
      <td>0.000613</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.001314</td>
      <td>0.004204</td>
      <td>0.001489</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.004029</td>
      <td>0.00035</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 796 columns</p>
</div>



- __Identify top 10 characters i.e. having 10 highest degree centrality values, from `evol_degree_df` and create a new dataframe with their names and centrality value__


```python

```




    Eddard-Stark          0.087157
    Cersei-Lannister      0.082998
    Jon-Snow              0.066649
    Tyrion-Lannister      0.065173
    Robert-Baratheon      0.063875
    Daenerys-Targaryen    0.063146
    Jaime-Lannister       0.059148
    Joffrey-Baratheon     0.049450
    Bran-Stark            0.038208
    Sansa-Stark           0.036994
    dtype: float64



- __Plot the evolution of weighted degree centrality of the above characters over the 5 books__
- __Comment on your answer__


```python

```


![png](index_files/index_41_0.png)



```python
# Your observations here 


```

#### Repeat Above for Weighted Betweenness Centrality


```python

```


![png](index_files/index_44_0.png)



```python
# Record Your observations here 
```

## Level Up: Visualize the Graphs (optional)

- Use the techniques seen so far to visualize and customize the graphs 
- Study the shapes of the graphs in terms of spread , clusters etc and see if you can identify any links to the actual books (or the TV series)

## Summary 

In this lab, we looked at different centrality measures of the graph data for the ASIOF dataset. We also compared these measures to see how they correlate with each other. We also saw in practice, the difference between taking the weighted centrality measures and how it may effect the results. 
