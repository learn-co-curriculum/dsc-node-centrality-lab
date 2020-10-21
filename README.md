
# Network Dynamics: Node Centrality - Lab

## Introduction

In this lab, you'll get a chance to practice implementing and interpreting the centrality metrics discussed in the previous lesson by investigating the social network from Game of Thrones!

## Objectives
You will be able to: 
- Compare and calculate degree, closeness, betweenness, and eigenvector centrality measures
- Interpret characteristics of certain nodes based on their centrality metrics  

## Character Interaction Graph Data

A. J. Beveridge and J. Shan created a network from George R. Martin's "A song of ice and fire" by extracting relationships between characters of the story. [The dataset is available at Github](https://github.com/mathbeveridge/asoiaf). Relationships between characters were formed every time a character's name appears within 15 words of another character. This was designed as an approximate metric for character's interactions with each other. The results of this simple analysis are quite profound and produce interesting visuals such as this graph:

<img src="images/got.png" width=800>

With that, it's your turn to start investigating the most central characters!


```python
import pandas as pd
import networkx as nx
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('darkgrid')
%matplotlib inline
```

##  Load the dataset 

Start by loading the dataset as a pandas DataFrame. From this, you'll then create a network representation of the dataset using NetworkX. 

The dataset is stored in the file `'asoiaf-all-edges.csv'`.


```python
# Load edges into dataframes
df = pd.read_csv('asoiaf-all-edges.csv')

# Print the first five rows
df.head()
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
      <th>Source</th>
      <th>Target</th>
      <th>Type</th>
      <th>id</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Addam-Marbrand</td>
      <td>Brynden-Tully</td>
      <td>Undirected</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Addam-Marbrand</td>
      <td>Cersei-Lannister</td>
      <td>Undirected</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Addam-Marbrand</td>
      <td>Gyles-Rosby</td>
      <td>Undirected</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Addam-Marbrand</td>
      <td>Jaime-Lannister</td>
      <td>Undirected</td>
      <td>3</td>
      <td>14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Addam-Marbrand</td>
      <td>Jalabhar-Xho</td>
      <td>Undirected</td>
      <td>4</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



## Create a Graph

- Instantiate an empty graph 
- Iterate through the data and create appropriate edges to the empty graph you instantiated above. Be sure to add the weight to each edge 


```python
# Create an empty graph instance
G = nx.Graph()

# Read edge lists into dataframes
for row in df.index:
    source = df['Source'][row]
    target = df['Target'][row]
    weight = df['weight'][row]
    G.add_edge(source, target, weight=weight)
```

## Calculate Degree

To start the investigation of the most central characters in the books, calculate the degree centrality for each character. Then create a bar graph of the top 10 characters according to degree centrality.


```python
pd.DataFrame.from_dict(nx.degree_centrality(G), orient='index').sort_values(by=0, ascending=False).head(10).plot(kind='barh', color='#1cf0c7')
plt.title('Top 10 Characters by Degree Centrality');
```


![png](index_files/index_8_0.png)


## Closeness Centrality

Repeat the above exercise for the top 10 characters according to closeness centrality.


```python
pd.DataFrame.from_dict(nx.closeness_centrality(G), orient='index').sort_values(by=0, ascending=False).head(10).plot(kind='barh', color='#1cf0c7')
plt.title('Top 10 Characters by Closeness Centrality');
```


![png](index_files/index_10_0.png)


## Betweeness Centrality

Repeat the process one more time for betweeness centrality.


```python
pd.DataFrame.from_dict(nx.betweenness_centrality(G), orient='index').sort_values(by=0, ascending=False).head(10).plot(kind='barh', color='#1cf0c7')
plt.title('Top 10 Characters by Betweeness Centrality');
```


![png](index_files/index_12_0.png)


## Putting it All Together

Great! Now put all of these metrics together along with eigenvector centrality. Combine all four metrics into a single dataframe for each character.


```python
degrees = nx.degree_centrality(G)
closeness = nx.closeness_centrality(G)
betweeness = nx.betweenness_centrality(G)
eigs = nx.eigenvector_centrality(G)
centrality = pd.DataFrame([degrees, closeness, betweeness, eigs]).transpose()
centrality.columns = ['degrees', 'closeness', 'betweeness', 'eigs']
centrality = centrality.sort_values(by='eigs', ascending=False)
centrality.head()
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
      <th>degrees</th>
      <th>closeness</th>
      <th>betweeness</th>
      <th>eigs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Tyrion-Lannister</th>
      <td>0.153459</td>
      <td>0.476333</td>
      <td>0.162191</td>
      <td>0.251558</td>
    </tr>
    <tr>
      <th>Cersei-Lannister</th>
      <td>0.122013</td>
      <td>0.454545</td>
      <td>0.088704</td>
      <td>0.235771</td>
    </tr>
    <tr>
      <th>Jaime-Lannister</th>
      <td>0.127044</td>
      <td>0.451961</td>
      <td>0.100838</td>
      <td>0.226339</td>
    </tr>
    <tr>
      <th>Joffrey-Baratheon</th>
      <td>0.086792</td>
      <td>0.433952</td>
      <td>0.031759</td>
      <td>0.214376</td>
    </tr>
    <tr>
      <th>Sansa-Stark</th>
      <td>0.094340</td>
      <td>0.433007</td>
      <td>0.048691</td>
      <td>0.205842</td>
    </tr>
  </tbody>
</table>
</div>



## Identifying Key Players

While centrality can tell us a lot, you've also begun to see how certain individuals may not be the most central characters, but can be pivotal in the flow of information from one community to another. In the previous lesson, such nodes were labeled as 'bridges' acting as the intermediaries between two clusters. Try and identify such characters from this dataset.


```python
centrality['bridge_proxy'] = centrality['betweeness'] / centrality.degrees
centrality = centrality.sort_values(by='bridge_proxy', ascending=False)
centrality.head(10)
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
      <th>degrees</th>
      <th>closeness</th>
      <th>betweeness</th>
      <th>eigs</th>
      <th>bridge_proxy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aggar</th>
      <td>0.005031</td>
      <td>0.269036</td>
      <td>0.007997</td>
      <td>0.001665</td>
      <td>1.589358</td>
    </tr>
    <tr>
      <th>Alleras</th>
      <td>0.010063</td>
      <td>0.272915</td>
      <td>0.014199</td>
      <td>0.002928</td>
      <td>1.411040</td>
    </tr>
    <tr>
      <th>Theon-Greyjoy</th>
      <td>0.083019</td>
      <td>0.423323</td>
      <td>0.111283</td>
      <td>0.102481</td>
      <td>1.340458</td>
    </tr>
    <tr>
      <th>Jon-Snow</th>
      <td>0.143396</td>
      <td>0.445378</td>
      <td>0.192120</td>
      <td>0.144211</td>
      <td>1.339782</td>
    </tr>
    <tr>
      <th>Cutjack</th>
      <td>0.003774</td>
      <td>0.255135</td>
      <td>0.005028</td>
      <td>0.001404</td>
      <td>1.332494</td>
    </tr>
    <tr>
      <th>Red-Oarsman</th>
      <td>0.003774</td>
      <td>0.261255</td>
      <td>0.005025</td>
      <td>0.001042</td>
      <td>1.331654</td>
    </tr>
    <tr>
      <th>Daenerys-Targaryen</th>
      <td>0.091824</td>
      <td>0.383317</td>
      <td>0.118418</td>
      <td>0.063043</td>
      <td>1.289621</td>
    </tr>
    <tr>
      <th>Victarion-Greyjoy</th>
      <td>0.030189</td>
      <td>0.333753</td>
      <td>0.036451</td>
      <td>0.009395</td>
      <td>1.207431</td>
    </tr>
    <tr>
      <th>Pate-(novice)</th>
      <td>0.008805</td>
      <td>0.215097</td>
      <td>0.010042</td>
      <td>0.000175</td>
      <td>1.140428</td>
    </tr>
    <tr>
      <th>Tyrion-Lannister</th>
      <td>0.153459</td>
      <td>0.476333</td>
      <td>0.162191</td>
      <td>0.251558</td>
      <td>1.056901</td>
    </tr>
  </tbody>
</table>
</div>



## Drawing the Graph

To visualize all of these relationships, draw a graph of the network.


```python
edge_labels = nx.get_edge_attributes(G, 'weight')
plt.figure(figsize=(12,12))
nx.draw(G, with_labels=True, pos=nx.spring_layout(G),
        alpha=0.8, node_color='#1cf0c7', node_size=700);
nx.draw_networkx_edge_labels(G,pos=nx.spring_layout(G), edge_labels=edge_labels);
```


![png](index_files/index_18_0.png)


## Subsetting the Graph

As you can see, the above graph is undoubtedly noisy, making it difficult to discern any useful patterns. As such, reset the graph and only add edges whose weight is 75 or greater. From there, redraw the graph. To further help with the display, try using `nx.spring_layout(G)` for the position. To jazz it up, try and recolor those nodes which you identified as bridge or bottleneck nodes to communication.


```python
# Read edge lists into dataframes
threshold = 75
colors = []
G = nx.Graph()
for row in df.index:
    source = df['Source'][row]
    target = df['Target'][row]
    weight = df['weight'][row]
    if weight >= threshold:
        G.add_edge(source,target, weight=weight)
edge_labels = nx.get_edge_attributes(G,'weight')
for node in G.nodes:
    if node in centrality.index[:10]:
        colors.append('#ffd43d')
    else:
        colors.append('#1cf0c7')
plt.figure(figsize=(18,10))
nx.draw(G, with_labels=True, pos=nx.spring_layout(G),
        alpha=.8, node_color=colors, node_size=1500)
nx.draw_networkx_edge_labels(G,pos=nx.spring_layout(G), edge_labels=edge_labels);
```


![png](index_files/index_20_0.png)


## Summary 

In this lab, we looked at different centrality measures of the graph data for the ASIOF dataset. We also compared these measures to see how they correlate with each other. We also saw in practice, the difference between taking the weighted centrality measures and how it may effect the results. 
