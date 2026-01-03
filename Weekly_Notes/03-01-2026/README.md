## Unsupervised Learning

### Core Concepts
Unlike supervised learning where data comes with target labels (e.g., "Spam" vs. "Not Spam"), **Unsupervised Learning** deals with unlabeled data. The goal is to discover hidden patterns, structures, or groupings within the dataset itself.

**Key Applications from Lecture:**
* **Clustering:** Grouping similar data points together (e.g., Customer Segmentation).
* **Dimensionality Reduction:** Reducing the number of variables while keeping the most critical information (e.g., Visualization).
* **Market Basket Analysis:** Finding associations between products (e.g., "People who buy Bread also buy Butter").

---

### 1. Clustering Algorithms
Clustering partitions data so that objects in the same group (cluster) are more similar to each other than to those in other groups.

#### **A. K-Means Clustering**
A centroid-based algorithm that partitions data into $K$ distinct clusters.

**The Algorithm Steps:**
1.  **Initialize:** Select $K$ random points as initial centroids.
2.  **Assign:** Calculate the distance (Euclidean) from every point to every centroid. Assign each point to the closest centroid.
3.  **Update:** Calculate the new centroid (mean) of all points currently in the cluster.
4.  **Repeat:** Iterate steps 2-3 until centroids stop changing (convergence).

**Evaluation Metrics:**
* **WSS (Within-Cluster Sum of Squares):** Measures how compact a cluster is. Lower is better. Also called "Distortion" when averaged.
* **BSS (Between-Cluster Sum of Squares):** Measures separation between different clusters. Higher is better.
* **TSS (Total Sum of Squares):** $TSS = WSS + BSS$.

> **Pro-Tip: Choosing 'K'**
> * **Elbow Method:** Plot $K$ vs. WSS. The "elbow" point where the drop in WSS levels off is the optimal $K$.
> * **Silhouette Score:** Ranges from -1 to +1. A score near +1 indicates points are well-matched to their own cluster and far from neighbors.

#### **B. Hierarchical Clustering**
Builds a hierarchy of clusters, visualized as a tree structure called a **Dendrogram**.
* **Agglomerative (Bottom-Up):** Starts with every point as its own cluster and merges the closest pairs iteratively.

**Linkage Methods (How to measure distance between clusters):**
* **Single Linkage:** Shortest distance between the closest points of two clusters. (Can result in long, "chain-like" clusters).
* **Complete Linkage:** Longest distance between the farthest points of two clusters. (Creates compact, spherical clusters).
* **Average Linkage:** Average distance between all pairs of points.
* **Ward’s Method:** Minimizes the increase in variance (WSS) when merging clusters.

#### **C. DBSCAN (Density-Based Spatial Clustering)**
Groups points that are closely packed together, marking points in low-density regions as outliers/noise.

**Key Parameters:**
* **Epsilon ($\epsilon$):** The maximum radius of the neighborhood around a point.
* **MinPts:** The minimum number of points required within $\epsilon$ to form a dense region (core point).

**Advantages:** Unlike K-Means, it can find arbitrarily shaped clusters (e.g., crescents) and automatically handles outliers.

---

### 2. Dimensionality Reduction
Techniques to reduce the number of input variables ($p$) to a lower number ($k$) for visualization or efficiency, while preserving structure.

| Technique | Type | Mechanism | Best For |
| :--- | :--- | :--- | :--- |
| **PCA** (Principal Component Analysis) | Linear | Projects data onto orthogonal axes (Principal Components) that maximize **variance**. | Visualizing simple, linear relationships; Noise filtering; Eigenfaces. |
| **ISOMAP** | Non-Linear | Preserves **Geodesic Distance** (distance along the curved surface) rather than straight-line Euclidean distance. | "Unrolling" curved manifolds (like a Swiss Roll). |
| **t-SNE** (t-Distributed Stochastic Neighbor Embedding) | Non-Linear | Converts similarities to **probabilities**. Minimizes divergence between probability distributions in high and low dimensions. | Visualizing complex clusters; preserving **local** neighborhood structure. |

---

### 3. Market Basket Analysis (Association Rules)
Used to discover relationships between items in large datasets, such as "If bread is bought, then butter is likely bought".

* **Algorithm:** Apriori Algorithm.
* **Key Metrics:**
    * **Support:** How frequently the itemset appears in the dataset.
    * **Confidence:** How likely item Y is purchased when item X is purchased.
    * **Lift:** The ratio of observed support to expected support if X and Y were independent.

---

### 4. Distance Metrics
Algorithms like K-Means and KNN rely heavily on how "distance" is defined.

* **Euclidean Distance:** The straight-line distance between two points $(x_1, y_1)$ and $(x_2, y_2)$.
    $$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$
   
* **Manhattan Distance (Taxicab):** The sum of absolute differences. Good for grid-like paths.
    $$d = |x_2 - x_1| + |y_2 - y_1|$$
   

---

### 5. Summary Comparison

| Feature | K-Means | Hierarchical | DBSCAN |
| :--- | :--- | :--- | :--- |
| **Type** | Partitioning (Centroid) | Tree-based | Density-based |
| **Shape** | Spherical/Convex | Arbitrary | Arbitrary |
| **Outliers** | Sensitive (Distorts mean) | Dependent on Linkage | **Robust** (Ignores noise) |
| **Parameters** | Must specify **K** | Linkage type, Cutoff | **Epsilon**, **MinPts** |