# Principal Component Analysis (PCA) Assignments

## What is PCA?

Principal Component Analysis is a dimensionality reduction technique that finds the directions of maximum variance in a dataset and projects the data onto those directions.

The core idea: high-dimensional data is rarely spread uniformly across all dimensions. Most of the meaningful variation lives along a few key directions. PCA finds those directions — called **principal components** — so you can represent the data with fewer numbers without losing much information.

**How it works:**
1. **Center the data** — subtract the mean so the data is centered at the origin
2. **Standardize** (if features are on different scales) — divide by standard deviation so no feature dominates just because of its unit
3. **Compute the covariance matrix** — this captures how features vary together
4. **Eigendecomposition** — find the eigenvectors and eigenvalues of the covariance matrix
5. **Sort by eigenvalue** — the eigenvector with the largest eigenvalue is PC1 (direction of most variance), next is PC2, and so on
6. **Project** — transform the data into the new coordinate system defined by the principal components

**Why it matters:**
- Correlated features carry overlapping information; PCA consolidates that into fewer, uncorrelated components
- Reduces noise by discarding low-variance directions
- Enables visualization of high-dimensional data in 2D or 3D
- Speeds up downstream machine learning by removing redundant dimensions

---

## Assignments

### Assignment 1: Geometry of PCA
**Question:** Which direction preserves maximum variance when data is projected onto it?

Generate 200 samples from a correlated 2D distribution, manually pick a direction vector, project the data onto it, and compare the variance of the projection against different directions. Builds the intuition for why PCA seeks the direction of maximum spread.

---

### Assignment 2: Eigenvalues = Variance
**Question:** Are eigenvalues actually equal to the projected variance, or just abstract numbers?

Verify numerically that the eigenvalue of the covariance matrix equals the variance of the data when projected onto the corresponding eigenvector. Generate 300 correlated 2D points, compute the covariance matrix, perform eigendecomposition, and confirm the relationship holds empirically.

---

### Assignment 3: Building PCA from Scratch
**Question:** What does each step of PCA actually do — and can you implement it using only NumPy?

Using a real manufacturing sensor dataset (100,000 rows, 9 features) and no sklearn, implement every PCA step manually: standardization, covariance matrix construction, eigendecomposition, scree plot, and projection onto the top components. Includes covariance heatmap, scree plot, and 2D projection visualizations.

---

### Assignment 4: PCA as a Rotation
**Question:** Does PCA move the data, or does it move the axes?

Generate correlated 2D data and overlay the original coordinate axes alongside the PCA eigenvector axes to show that PCA rotates the frame of reference, not the data itself. PC1 aligns with the longest axis of the data cloud; the data in the new frame is decorrelated.

---

### Assignment 5: What Gets Lost When You Compress?
**Question:** What information is actually discarded when you drop a principal component?

Compress correlated 2D data to 1D by keeping only PC1. Reconstruct the 2D points from the 1D projection and visualize the difference between the originals and their reconstructions. Quantifies the reconstruction error and shows what "information loss" looks like geometrically.

---

### Assignment 6: Does Scale Matter?
**Question:** What happens to PCA when features are on wildly different scales?

Create a 3-feature dataset where all features share the same underlying signal but have scales differing by orders of magnitude (tens, thousands, fractions). Run PCA without scaling and with standardization, then compare which component dominates in each case. Demonstrates why standardization is essential before applying PCA.

---

### Assignment 7: Computing Explained Variance Ratio from Scratch
**Question:** How do you calculate how much information each principal component captures?

Using the manufacturing dataset, manually compute the explained variance ratio for each component using the formula `EVR[i] = λᵢ / Σλ`. Plot a bar chart and cumulative variance curve to determine how many components are needed to capture 90%+ of the total variance.

---

### Assignment 8: PCA Beyond 2D
**Question:** How does PCA extend to higher-dimensional data, and can you visualize the compression?

Generate a correlated 3D dataset (300 samples), standardize it, and reduce it to 2D using PCA. Visualize both the original 3D scatter and the 2D projected result. Confirms that the structure of the data is preserved after dropping the least informative dimension.

---

### Assignment 9: Conceptual Short Answers
**Question:** Can you explain the core ideas of PCA clearly without relying on code?

Short-answer responses covering:
- What PCA optimizes mathematically (maximizing variance via eigenvectors of the covariance matrix)
- Why variance measures information content
- Whether PCA is useful when features are uncorrelated
- Why standardization is necessary before PCA
- The difference between covariance and correlation in the PCA context
- How PCA relates to projection onto a new axis
- Why principal components are orthogonal
- What "rotating the coordinate system" means geometrically
- How PCA reduces redundancy in correlated features

---

## Dataset

`data/manufacturing_6G_dataset.csv` — Manufacturing sensor readings with 100,000 rows and 9 features including Production_Speed, Packet_Loss, and related metrics. Used in Assignments 3 and 7.

## Outputs

Generated plots are saved in `output/` covering covariance heatmaps, scree plots, rotation diagrams, reconstruction error visualizations, scaling effect comparisons, explained variance charts, and 2D/3D projections.
