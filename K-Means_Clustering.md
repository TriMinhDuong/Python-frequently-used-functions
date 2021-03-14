# K-Means Clustering

Assess different K values using elbow method

```python
import pylab as pl
from sklearn.cluster import KMeans

k = range(1, 15)

# Instantiate and fit KMeans for Clusters 1-14
kmeans = [KMeans(n_clusters=i) for i in k]
score = [kmeans[i].fit(df[df.columns[2:]]).score(df[df.columns[2:]]) for i in range(len(kmeans))]

# Plot the elbow method
pl.plot(k,score)
pl.xlabel('Number of Clusters')
pl.ylabel('Score')
pl.title('Elbow Curve')
pl.show()
```

After reviewing the plot, we can choose the most appropriate k value for number of clusters. We are training the data with that k value. We will predict the cluster from first patient down all the rows.

```python
# Choose cluster size of 3
cluster = KMeans(n_clusters = 3) # At least 7-times times cluster = patients

# Predict the cluster from first patient down all the rows
df["cluster"] = cluster.fit_predict(df[df.columns[2:]])
```

We will perform PCA to reduce our dimensions so we can visually see our cluster segments.

```python
from sklearn.decomposition import PCA

# Principal component separation to create a 2-dimensional picture
pca = PCA(n_components = 2)
df['x'] = pca.fit_transform(df.iloc[:,1:33])[:,0]
df['y'] = pca.fit_transform(df.iloc[:,1:33])[:,1]
df = df.reset_index()

# Plot 3 clusters with Matplotlib
kmeans_color = ['green' if c == 0 else 'blue' if c == 2 else 'red' for c in cluster.labels_]

fig = plt.figure(figsize=(10,6))
plt.scatter(x="x", y="y", data=df, alpha=0.25, color=kmeans_color)
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("KMeans Clusters")
plt.show()
```

We will merge the predictions with the raw data to implement deeper analysis.
